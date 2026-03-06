# 🤖 ROS 2 Mobile Robot Arm Simulation

![ROS2](https://img.shields.io/badge/ROS2-Jazzy-blue)
![Gazebo](https://img.shields.io/badge/Gazebo-Harmonic-orange)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04-E95420)
![Status](https://img.shields.io/badge/Status-Active-success)

</div>

---

## 📌 Project Overview

This project utilizes **ROS 2 (Jazzy)** and **Gazebo (Harmonic)** to create a differential drive mobile robot equipped with an arm. The robot is designed for simulation in various environments with a focus on ease of operation and versatility.

---

## 🛠️ Technologies Used

| Technology | Version / Details |
|---|---|
| 🔵 **ROS 2** | Jazzy |
| 🟠 **Gazebo** | Harmonic |
| 📄 **Robot Description** | Xacro / URDF |
| 🌉 **Communication Bridge** | ros_gz_bridge |
| 🐧 **Operating System** | Ubuntu 24.04 |

---

## 📁 Directory Structure

```
src/
├── .vscode/
├── my_robot_description/
│   ├── launch/
│   │   ├── display.launch.py
│   │   ├── display.launch.xml
│   │   └── for_arm.launch.xml
│   ├── rviz/
│   │   └── my_robot.rviz
│   ├── urdf/
│   │   ├── camera.xacro
│   │   ├── common_properties.xacro
│   │   ├── main.urdf.xacro
│   │   ├── mobile_base_gazebo.xacro
│   │   ├── mobile_base.xacro
│   │   ├── robot_arm_gazebo.xacro
│   │   └── robot_arm.xacro
│   ├── CMakeLists.txt
│   └── package.xml
└── robot_bringup/
    ├── config/
    │   └── gazebo_bridge.yaml
    ├── launch/
    │   └── robot_gazebo_launch.xml
    ├── world/
    │   └── world1.1.sdf
    ├── CMakeLists.txt
    └── package.xml
```

---

## 🖼️ Visuals

### 1️⃣ ROS 2 Node and Topic Communication (rqt_graph)
<img width="1851" height="974" alt="image" src="https://github.com/user-attachments/assets/654f24e8-21ee-4790-aac5-16ce5b5f99d5" />

### 2️⃣ Simulation Environment (Gazebo World)
<img width="1854" height="1014" alt="Screenshot from 2026-03-05 21-02-34" src="https://github.com/user-attachments/assets/ceb91f6c-c3b3-4fde-b43c-7d4e78d89857" />

### 3️⃣ Teleop Control and Camera Display
<img width="1853" height="1000" alt="image" src="https://github.com/user-attachments/assets/fe42aea0-54b0-43ff-9bf8-367a6c3313ff" />

### 4️⃣ Robot Arm Visualization (Gazebo + Terminal + RViz2)
<img width="1854" height="1014" alt="image" src="https://github.com/user-attachments/assets/1ccd41b5-b45a-4176-b30a-7a6745595dfa" />

---

## 🚀 Installation & Quick Start

**1. Build the workspace:**
```bash
colcon build
source install/setup.bash
```

**2. Launch the simulation:**
```bash
ros2 launch robot_bringup robot_gazebo_launch.xml
```

---

## 🔭 Future Plans

- [ ] 📷 Develop plugins for enhanced camera integration
- [ ] 🚗 Implement driving plugins for improved mobility control

---

<div align="center">
  <sub>Built with ❤️ using ROS 2 & Gazebo</sub>
</div>
