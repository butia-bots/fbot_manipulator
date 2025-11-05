<div align="center">
<img width="5848" height="719" alt="fbot_manipulator" src="https://github.com/user-attachments/assets/c73b64f3-05bf-47c7-bb67-3e38c7f4161a"/>

![UBUNTU](https://img.shields.io/badge/UBUNTU-22.04-orange?style=for-the-badsge&logo=ubuntu)
![python](https://img.shields.io/badge/python-3.10-blue?style=for-the-badsge&logo=python)
![ROS2](https://img.shields.io/badge/ROS2-Humble-blue?style=for-the-badsge&logo=ros)

[Overview](#overview) • [Architecture](#architecture) • [Installation](#installation) • [Usage](#usage) • [fbot_manipulator topics and services](#fbot_manipulator-topics-and-services) • [Contributing](#contributing)

</div>

## Overview

`fbot_manipulator` This repository contains all the necessary packages for controlling and performing manipulation tasks with the WX200 manipulator.  It includes everything required to interface with, configure, and execute manipulation routines using the WX200 arm, ensuring full compatibility with the Interbotix framework.

---

## Architecture

### Package Structure
```
fbot_manipulator/
├── 📝config/ #Custom arm manipulator positions are recorded here
├── ⚙️fbot_manipulator_tools/ #This package contains the manipulator tools developed by FBOT
├── interbotix_ros_core/ #Interbotix Packages that contain the actuator for all the interbotix arms
├── interbotix_ros_manipulators/ #Packages to control the various types of arms sold at Trossen Robotics
├── interbotix_ros_toolboxes #Contains support level ROS wrappers and robot interface modules that are used in many robotic platforms at Trossen Robotics.
├── moveit_visual_tools #Helper functions for displaying and debugging MoveIt data in Rviz via published markers, trajectories, and MoveIt collision objects.
├── LICENSE 
├── 📝README.md #This short summary
 
```

---

## Installation

### Prerequisites

- ROS2 Humble
- Python 3.10+
- Ubuntu 22.04
- ROS2 Interbotix Packages > [Interbotix Installation](https://docs.trossenrobotics.com/interbotix_xsarms_docs/ros_interface/ros2/software_setup.html#amd64-architecture)

### Initial Setup

1. **Clone the repository into your ROS workspace:**
   ```bash
   cd ~/fbot_ws/src
   git clone https://github.com/fbotathome/fbot_manipulator.git
   ```

2. **Install dependencies:**
   ```bash
   cd ~/fbot_ws
   sudo rosdep init  # Skip if already initialized
   rosdep update
   rosdep install --from-paths src --ignore-src -r -y
   # No requirements.txt for this package
   ```

3. **Build the workspace:**
   ```bash
   cd ~/fbot_ws
   colcon build
   source install/setup.bash
   ```
   
---

## Usage
### fbot_manipulator_tools

### [save_wx200_arm_pose.py](https://github.com/fbotathome/fbot_manipulator/tree/main/fbot_manipulator_tools/fbot_manipulator_tools)

   ```bash
   #Launch wx200 in rviz
   ros2 launch interbotix_xsarm_control xsarm_control.launch.py robot_model:=wx200

   #Run the node to save the arm position
   ros2 run fbot_manipulator_tools manipulator_saver
   ```
## fbot_manipulator topics and services 


### Topics

| Topic | Type | Description |
|-------|------|-------------|
| `/wx200/commands/joint_group` | [`JointGroupCommand.msg`](interbotix_ros_core/interbotix_ros_xseries/interbotix_xs_msgs/msg/JointGroupCommand.msg) | Command Group Joints |
| `/wx200/commands/joint_single` | [`JointSingleCommand.msg`](interbotix_ros_core/interbotix_ros_xseries/interbotix_xs_msgs/msg/JointSingleCommand.msg) | Command Single Joint |
| `/wx200/commands/joint_trajectory` | [`JointTrajectoryCommand.msg`](interbotix_ros_core/interbotix_ros_xseries/interbotix_xs_msgs/msg/JointTrajectoryCommand.msg) | Trajectory to The Desired Joint(s) |
| `/wx200/joint_states` | [`JointState.msg`](https://docs.ros.org/en/noetic/api/sensor_msgs/html/msg/JointState.html) |Describe Controlled Joints |
| `/wx200/robot_description` | [`String.msg`](https://docs.ros.org/en/melodic/api/std_msgs/html/msg/String.html) | wx200 Arm Description |

### Services

| Service | Type | Description |
|---------|------|-------------|
| `/wx200/torque_enable` | [`interbotix_xs_msgs/srv/TorqueEnable`](https://docs.trossenrobotics.com/interbotix_xsarms_docs/ros_interface/ros2/overview/xs_msgs.html) | Disable Arm Torque |
| `/wx200/reboot_motors` | [`interbotix_xs_msgs/srv/Reboot`](https://docs.trossenrobotics.com/interbotix_xsarms_docs/ros_interface/ros2/overview/xs_msgs.html) | Restart Arm Motors |

---

## Contributing

1. Create a feature branch (`git checkout -b feat/amazing-feature`)
2. Commit your changes (`git commit -m 'Add amazing feature'`)
3. Push to the branch (`git push origin feat/amazing-feature`)
4. Open a Pull Request
