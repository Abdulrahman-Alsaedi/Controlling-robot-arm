# Controlling the Robot Arm

This repository provides instructions on how to control a robot arm using `joint_state_publisher` and MoveIt with kinematics.

## Prerequisites

1. Source the ROS setup file:
   
   ```sh

   source /opt/ros/noetic/setup.bash

2. Create and initialize the catkin workspace:
   
   ```sh

   mkdir -p ~/catkin_ws/src
   cd ~/catkin_ws/
   catkin_make

3. Source the catkin workspace setup file and add it to your .bashrc:
   ```sh
   
    source devel/setup.bash
    echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc

## Installation
   
1. Add the arduino_robot_arm package to the src folder:
   
   ```sh
   
   cd ~/catkin_ws/src
   sudo apt install git
   git clone https://github.com/smart-methods/arduino_robot_arm

2. Install all dependencies:
   
   ```sh
   
   cd ~/catkin_ws
   rosdep install --from-paths src --ignore-src -r -y
   sudo apt-get install ros-noetic-moveit
   sudo apt-get install ros-noetic-joint-state-publisher ros-noetic-joint-state-publisher-gui
   sudo apt-get install ros-noetic-gazebo-ros-control joint-state-publisher
   sudo apt-get install ros-noetic-ros-controllers ros-noetic-ros-control

3. Compile the package:
   
   ```sh

   catkin_make

## Usage

1. Launch the robot arm package:

   ```sh

   roslaunch robot_arm_pkg check_motors.launch

![Capture](https://github.com/user-attachments/assets/b1222d89-0cd0-4029-8b5f-1dfa8f6e246c)

2. Check the joint states:

   ```sh

   rostopic echo /joint_states

3. Launch in Gazebo:

   ```sh

   roslaunch robot_arm_pkg check_motors_gazebo.launch
   rosrun robot_arm_pkg joint_states_to_gazebo.py

![Gazebo](https://github.com/user-attachments/assets/bb472278-4473-4faa-ac53-f704bda917b2)

4. You may need to change the permission of the script:

   ```sh

   cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
   sudo chmod +x joint_states_to_gazebo.py

5. Launch MoveIt:

   ```sh

   roslaunch moveit_pkg demo.launch
   roslaunch moveit_pkg demo_gazebo.launch

![moveit](https://github.com/user-attachments/assets/82b5e64e-46e2-4696-acd9-e033f6fc0c06)
