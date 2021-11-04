# Arm Move Package: Flexin' Trajectories

Author and Maintainer: **Ryan King-Shepard**

## **Description**
A package that connects to a px100 and sends it commands for the 
end-effector position and gripper state.

This package contains:

- nodes:
    1. `mover` ~ Contains services that enable the node to set the px100's end
        effector and gripper state.
- config:
    * `waypoints.yaml` ~ A configuration with the initial set of waypoints the 
        px100's end effector should hit     
- launch 
    * `arm_box.launch` ~ A launchfile that links to the interbotix launchfiles
        for different types of runs
    * `arm.launch` ~ The main launchfile which serves as a simplier interface 
        to the px100 than arm_box
- srv
    * `PxKinStep.srv` ~ srv defintion for the `step` service in `mover` node
    * `ResetBox.srv` ~ srv defintion for the `reset` service in `mover` node
    * `SimpleBool.srv` ~ srv defintion for the `follow` service in `mover` node
- `package.xml`
    * Package configuration
- `CMakeLists.tx`
    * Build configuration
- test
    * `motion_test` ~ A testfile asserting proper error codes from valid/invalid
    end effector points
    * `arm.test` ~ Launch testfile for testing.
- worlds
    * `arm_and_box.world` ~ World file for gazebo testing
- `README.md`
    * We have to stop meeting like this. 


## **Dependencies and Installation**

### *ROS Dependencies*
This package was developed and tested in ros-noetic. Arm_move was designed and built using catkin. This package also requires the turtlesim package to run. This should usually come with your ros installation, but to check this run: 

This should result a little screen with a turtle in the center. If the window doesn't pop up, refer to [ROS wiki](http://wiki.ros.org) to install turtlesim on your machine.

The full list of ros package dependencies can be found in `package.xml`. Two big dependencies to note are the interbotix_xsarm_moveit and the moveit packages. To set up the proper environment, do the following:
1. Set up your moveit_ws; run `catkin_make` and `source devel/setup.[terminal_file]` where terminal_file is the type of terminal you are running (e.g bash). Instructions to assist with moveit can be found [here](https://ros-planning.github.io/moveit_tutorials/doc/getting_started/getting_started.html)
2. Set up a custom_ws with [interbotix](https://github.com/Interbotix/interbotix_ros_manipulators) and `catkin_make` and `source devel/setup.[terminal_file]` for the *interbotix_xasrm_moveit* package.
3. Ensure that you have the other dependencies found in `package.xml`.

### *Python Dependencies*
All code for this package was developed and test in Python 3 (specfically 3-8-10).  
This package requires `numpy` in order to run. The version used was 1-17.4, however there is no 
strong attachment to this version; other versions should work fine as long as they compatitble with
the python version. Refer to [Numpy docs](https://numpy.org/install/) for installation information. 

## **Execution**

### px100 launch (Connecting to the robot)
The main launch file for the arm_move package is `arm.launch`.
```bash
roslaunch arm_move arm.launch [use_gazebo | use_fake | use actual]
```
The launchfile allows you to run the mover in 3 different setups. The first is the `use_gazebo` configuration. By setting the argument to `true`, the package will run the mover node with gazebo and rviz. Gazebo will load the px100 in the custom world file, `arm_and_box.world`, which contains a small grey box and a larger blue realsense box. The grey box is small target for the robot to pick up and move, while the blue box acts as an obstacle to impede the robot. After inspecting the world, hit play to complete setup and have rviz pop-up. Rviz will show a rectanglar table with a green realsense box in a similar location as the gazebo realsense box. 

The `use_fake` configuration will run a 'headless' controller to respond to control input while rviz still displaying the current configuration of the robot. Finally, the `use_actual` should be used in order to send commands to a real px100; simply plug in the px100 and run the launchfile with `use_actual` as true. Note, whenever running `arm.launch` always set one, and only one, of the possible configurations to `true`

### ROS Services (Commanding the robot)
Once one of the configurations is chosen and running, there are 3 services used to interact with the robot: `reset`, `step`, and `follow`. 

The `reset` service uses the ResetBoxRequest to set the position and orientation of the realsense box in Rviz, reset the px100 to the home position, and clear the current waypoints. If only the waypoints need to be cleared, then only set the "clear" bool in the request. A request with x, y, z, roll, pitch, and yaw as 0 will not effect the position of the box, under the assumptions that the box cannot be at the origin(where the robot is) and that only clear was set. Note: the units for x, y, z are in meters and the radians are used for the angles.

The `step` service uses the PxKinStep (Px100 Kinematic Step) to request the px100 move the end effector to a certain x,y,z and have gripper open or close. The services returns an error code to 
indicate if the point is reachable or not. The definitions of the error code are found in [moveit_msgs.MoveItErrorCodes](http://docs.ros.org/en/noetic/api/moveit_msgs/html/msg/MoveItErrorCodes.html). If the point is reachable, the waypoint is added to an internal list of waypoints. 

The `follow` service uses the SimpleBool to request the robot follow the internal list of waypoints by setting the end effector's position and gripper state for each point. The SimpleBool has only one boolean in it; if set to true, the robot will cycle through the path indefinity until one of other services are used or the node shuts down. The service acquires waypoints from two sources: the waypoints.yaml and any point added by the `step` service. Note: during initialization, every point in waypoints.yaml is checked for reachability. If the point is not reachable, it is ignored. 

Example of simulation video: setting `use_gazebo:=true` and then using the `follow` service


https://user-images.githubusercontent.com/90436131/140406922-dec6063c-ba8d-451f-aa84-5ba80fb92d45.mp4


Example of actual video: setting `use_actual:=true` and then using the `follow` service

https://user-images.githubusercontent.com/90436131/140404939-a1520204-1151-4a4c-bd6e-3956a6bae7e8.mp4




