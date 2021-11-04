# Arm Move Package: Flexin' Trajectories

Author and Maintainer: **Ryan King-Shepard**

## **Description**
A package that connects to a px100 and sends it commands for the 
end-effector position and gripper state.

This package contains:

- nodes:
    1. `mover` ~ 
- config:
    * `waypoints.yaml` ~ 
- launch 
    * `arm_box.launch` ~ 
    * `arm.launch` ~ 
- `package.xml`
    * Package configuration
- `CMakeLists.tx`
    * Build configuration
- test
    * Test directory
- worlds
    * `arm_and_box.world` ~ 
- `README.md`
    * We have to stop meeting like this. 


## **Dependencies and Installation**

### *ROS Dependencies*
This package was developed and tested in ros-noetic. Arm_move was designed and built using catkin. This package also requires the turtlesim package to run. This should usually come with your ros installation, but to check this run: 

This should result a little screen with a turtle in the center. If the window doesn't pop up, refer to [ROS wiki](http://wiki.ros.org) to install turtlesim on your machine.

The full list of ros package dependencies can be found in `package.xml`.

### *Python Dependencies*
All code for this package was developed and test in Python 3 (specfically 3-8-10).  
This package requires `numpy` in order to run. The version used was 1-17.4, however there is no 
strong attachment to this version; other versions should work fine as long as they compatitble with
the python version. Refer to [Numpy docs](https://numpy.org/install/) for installation information. 

## **Execution**

### px100


Example of simulation video:

https://user-images.githubusercontent.com/90436131/140406922-dec6063c-ba8d-451f-aa84-5ba80fb92d45.mp4


Example of actual video:

https://user-images.githubusercontent.com/90436131/140404939-a1520204-1151-4a4c-bd6e-3956a6bae7e8.mp4




