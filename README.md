# ROS 2 Mobile Robot Arm Simulation

## Project Overview
This project utilizes ROS 2 (Jazzy) and Gazebo (Harmonic) to create a differential drive mobile robot equipped with an arm. The robot is designed for simulation in various environments with a focus on ease of operation and versatility.

## Technologies Used  
- **ROS 2 Version:** Jazzy  
- **Gazebo Version:** Harmonic  
- **Robot Description:** Xacro/URDF  
- **Communication Bridge:** ros_gz_bridge  
- **Operating System:** Ubuntu 24.04  

## Directory Structure
```
ros2-mobile-robot-arm-gzsim/
│
├── .vscode/                # VS Code configuration files
├── my_robot_description/   # Description files for robot modeling
│   ├── urdf/               # URDF files
│   └── xacro/              # Xacro files
├── robot_bringup/          # Launch files for starting up the robot
└── ...                     # Other project-related files
```  

## Visuals
- ![VS Code File Tree](<link_to_file_tree_image>)  
- ![Gazebo Robot and Pallets](<link_to_gazebo_image>)  
- ![Teleop and Camera View](<link_to_teleop_camera_image>)  
- ![Fullscreen Gazebo/Terminal/RViz2](<link_to_fullscreen_image>)  

## Future Plans
- Develop plugins for enhanced camera integration.  
- Implement driving plugins for improved mobility control.

## Note
Please refrain from including exaggerated features such as Nav2 or MoveIt2, as the focus is on the essential functionalities of the robot arm and mobile platform.