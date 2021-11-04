# Differential Drive Package: Madbot's flipping adventure

Author and Maintainer: **Ryan King-Shepard**

## **Description**
A package that demonstrates a  custom cart robot with differential drive 
called madbot moving forward and backward, flipping in the process. 

This package contains:

- nodes:
    1. `flip` ~ Publishes a commanded linear velocity for madbot
- config:
    * `madbot_dim.yaml` ~ Contains the dimensions of the main rectangular chassis, the casters, 
    and the wheels of the robot
- launch 
    * `ddrive.launch` ~ The main launch file of the package. Opens gazebo and rviz to demonstrate 
    forward and backward motion. **Note**: Gazebo is paused on start-up; don't forget to hit play in order to view motion
    * `ddrive_rviz.launch` ~ A debugging launch file used to verify design of cart. Use *ddrive.launch* instead of this launch file
    * `madbot.rviz` ~ Rviz configuration of madbot
- `package.xml`
    * Package configuration
- `CMakeLists.tx`
    * Build configuration
- urdf
    * `ddrive.urdf.xacro` ~ URDF for differential drive robot with frictionless caster
    * `ddrive.gazebo` ~ Gazebo extensions of the URDF in order to provide gazebo-specfic properties
    to the bot in gazebo.
- worlds
    * `ddrive.world` ~ 'Junkyard' world file define the environment of madbot. 
- `README.md`
    * Oh...that's me!


## **Dependencies and Installation**

### *ROS Dependencies*
This package was developed and tested in ros-noetic. Diff_drive is designed and should be built using catkin. The full list of ros package dependencies can be found in `package.xml`.

### *Python Dependencies*
All code for this package was developed and test in Python 3 (specfically 3-8-10).  

## **Execution**

### Madbot's reckless drive
The `ddrive.launch` is a simple launch file to pulls up gazebo and rviz to show madbot's 
movement.  
```bash
roslaunch diff_drive ddrive.launch
```
*Note:* The launch file will open gazebo in a paused state.  Hit play near the bottom to see the 
robot in action

Below is an example of madbot's drive:

https://user-images.githubusercontent.com/90436131/140323429-7af1633f-78d7-427a-b103-6a25365f2083.mp4


