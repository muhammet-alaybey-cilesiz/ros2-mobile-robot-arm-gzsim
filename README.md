# ROS2 Mobile Robot Arm Simulation with Gazebo

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ROS2](https://img.shields.io/badge/ROS-2-blue)](https://docs.ros.org/en/humble/)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://www.python.org/)
[![Gazebo](https://img.shields.io/badge/Simulator-Gazebo%20(GZ%20Sim)-orange)](https://gazebosim.org/)

**Advanced robotic simulation platform for mobile manipulation systems**

[Features](#features) • [Installation](#installation) • [Quick Start](#quick-start) • [Documentation](#documentation) • [Contributing](#contributing)

</div>

---

## 📋 Overview

This project provides a comprehensive ROS2-based simulation environment for a mobile robot equipped with a robotic arm. The system utilizes modern robotics standards including URDF/Xacro for robot description, ROS2 for middleware, and Gazebo (GZ Sim) for physics-realistic simulation.

### Key Capabilities
- 🤖 **Mobile Base Control**: Differential drive or omnidirectional locomotion
- 🦾 **Robotic Arm Manipulation**: Multi-DOF arm with gripper support
- 🌍 **Realistic Physics**: Gazebo physics engine for accurate simulation
- 📡 **ROS2 Integration**: Full integration with ROS2 ecosystem
- 🎯 **Parameter Configuration**: Xacro-based parametric descriptions
- 🔄 **Launch System**: Automated startup scripts and configurations

---

## 🎯 Features

### Robot Components
- **Mobile Base**: Configurable wheel setup and dynamics
- **Robotic Arm**: 6-DOF or configurable joint manipulator
- **End-Effector**: Gripper or tool interface
- **Sensors**: Camera, LiDAR, IMU support (extensible)

### Simulation Capabilities
- Physics-realistic motion and collisions
- Environmental interaction
- Multi-robot simulation support
- Custom world environments
- Parameter sweeping for experimentation

### Development Features
- Modular package architecture
- ROS2 standard conventions
- URDF/Xacro parametric design
- Launch file orchestration
- Extensible plugin system

---

## 📦 Project Structure

```
ros2-mobile-robot-arm-gzsim/
├── src/
│   ├── my_robot_description/          # Robot URDF and model definitions
│   │   ├── urdf/                      # URDF files
│   │   ├── xacro/                     # Xacro parametric files
│   │   ├── meshes/                    # 3D mesh models
│   │   ├── launch/                    # Launch files
│   │   └── package.xml                # Package manifest
│   │
│   └── robot_bringup/                 # Startup and configuration
│       ├── launch/                    # Bringup launch files
│       ├── config/                    # Configuration files
│       ├── params/                    # Parameter files
│       └── package.xml                # Package manifest
│
├── LICENSE                            # MIT License
├── .gitignore                         # Git ignore rules
└── README.md                          # This file
```

---

## 🛠️ Installation

### Prerequisites
- **OS**: Ubuntu 20.04 LTS or later (Ubuntu 22.04 LTS recommended)
- **ROS2**: Humble Hawksbill or later
- **Gazebo**: Gazebo Sim (GZ Sim) - Latest version
- **Python**: 3.8 or higher
- **Build System**: Colcon

### System Dependencies

```bash
# Update package manager
sudo apt update

# Install ROS2 (if not already installed)
# Follow: https://docs.ros.org/en/humble/Installation.html

# Install Gazebo
sudo apt install gazebo libgazebo-dev

# Install additional ROS2 packages
sudo apt install ros-humble-gazebo-* ros-humble-xacro
sudo apt install python3-colcon-common-extensions
```

### Clone Repository

```bash
# Create ROS2 workspace (if not exists)
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

# Clone the repository
git clone https://github.com/muhammet-alaybey-cilesiz/ros2-mobile-robot-arm-gzsim.git
cd ..

# Install dependencies
rosdep update
rosdep install --from-paths src --ignore-src -y
```

### Build the Project

```bash
# Build packages
colcon build

# Setup environment
source install/setup.bash
```

---

## 🚀 Quick Start

### 1. Launch the Simulation

```bash
# Source the environment
source ~/ros2_ws/install/setup.bash

# Launch the robot in Gazebo
ros2 launch robot_bringup spawn.launch.py
```

### 2. Control the Robot

#### Mobile Base Control
```bash
# Publish velocity commands
ros2 topic pub /cmd_vel geometry_msgs/Twist '{linear: {x: 0.5, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.1}}'
```

#### Arm Control
```bash
# Move arm joints (example for 6-DOF arm)
ros2 topic pub /arm_controller/joint_trajectory_controller/joint_trajectory \
  trajectory_msgs/JointTrajectory '{
    header: {frame_id: "world"},
    joint_names: ["joint_1", "joint_2", "joint_3", "joint_4", "joint_5", "joint_6"],
    points: [{
      time_from_start: {sec: 2},
      positions: [0.5, 0.5, 0.5, 0.5, 0.5, 0.5]
    }]
  }'
```

### 3. View Robot State

```bash
# Display ROS2 nodes
ros2 node list

# Display ROS2 topics
ros2 topic list

# Check published data
ros2 topic echo /tf
```

---

## 📚 Documentation

### Configuration

Edit the Xacro files in `src/my_robot_description/xacro/` to customize:
- Robot dimensions and mass properties
- Joint limits and dynamics
- Sensor configurations
- Materials and colors

Example:
```bash
# Generate URDF from Xacro
xacro src/my_robot_description/xacro/robot.xacro > /tmp/robot.urdf
```

### Launch Files

#### Main Launch
- **`spawn.launch.py`**: Launches Gazebo and spawns the robot

#### Parameters
Modify `src/robot_bringup/config/` for:
- Controller parameters
- Sensor settings
- Simulation parameters

### ROS2 Topics

**Standard Topics:**
| Topic | Type | Description |
|-------|------|-------------|
| `/cmd_vel` | `geometry_msgs/Twist` | Mobile base velocity commands |
| `/tf` | `tf2_msgs/TFMessage` | Transform frames |
| `/joint_states` | `sensor_msgs/JointState` | Robot joint positions |
| `/odom` | `nav_msgs/Odometry` | Odometry estimate |

---

## 🔧 Configuration Guide

### Modify Robot Parameters

Edit `src/my_robot_description/xacro/robot.xacro`:

```xacro
<!-- Example: Change wheel radius -->
<xacro:arg name="wheel_radius" default="0.05"/>

<!-- Example: Change arm link length -->
<xacro:arg name="link_length" default="0.3"/>
```

### Add New Sensors

1. Create sensor definition in Xacro
2. Update launch files
3. Configure controller plugins in launch

---

## 🎮 Advanced Usage

### Custom Environments

Create new world files in `src/robot_bringup/worlds/`:

```xml
<?xml version="1.0" ?>
<sdf version="1.6">
  <world name="custom_world">
    <!-- World definition -->
  </world>
</sdf>
```

### Multi-Robot Simulation

Launch multiple robots by modifying launch files:

```python
# In launch file
def generate_launch_description():
    return LaunchDescription([
        Node(package='robot_bringup',
             executable='spawn_robot',
             arguments=['--x', '0', '--y', '0', '--robot_name', 'robot1']),
        Node(package='robot_bringup',
             executable='spawn_robot',
             arguments=['--x', '2', '--y', '0', '--robot_name', 'robot2']),
    ])
```

### Recording and Playback

```bash
# Record bag file
ros2 bag record -a -o my_recording

# Playback
ros2 bag play my_recording
```

---

## 🐛 Troubleshooting

### Common Issues

#### Issue: Gazebo fails to launch
```bash
# Solution: Update Gazebo
sudo apt upgrade gazebo libgazebo-dev
```

#### Issue: Colcon build fails
```bash
# Solution: Clean and rebuild
colcon clean packages --select my_robot_description robot_bringup
colcon build
```

#### Issue: Robot falls through ground
- Check collision geometries in URDF
- Verify physics parameters
- Ensure proper frame definitions

### Debug Mode

```bash
# Launch with verbose output
ros2 launch robot_bringup spawn.launch.py debug:=true

# View ROS2 graph
ros2 run rqt_graph rqt_graph
```

---

## 📖 Additional Resources

### ROS2 Documentation
- [ROS2 Official Docs](https://docs.ros.org/)
- [ROS2 Humble Documentation](https://docs.ros.org/en/humble/)

### Gazebo Documentation
- [Gazebo Sim Official](https://gazebosim.org/)
- [SDF Format Reference](https://sdformat.org/)

### URDF and Xacro
- [URDF Documentation](http://wiki.ros.org/urdf)
- [Xacro Tutorial](http://wiki.ros.org/xacro)

### Related Projects
- [MoveIt2](https://moveit.ros.org/) - Motion planning
- [Nav2](https://navigation.ros.org/) - Navigation stack
- [Isaac Sim](https://developer.nvidia.com/isaac-sim) - Alternative simulator

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Contributions are welcome! Here's how to contribute:

### 1. Fork the Repository
```bash
# Create a fork on GitHub
# Clone your fork
git clone https://github.com/your-username/ros2-mobile-robot-arm-gzsim.git
cd ros2-mobile-robot-arm-gzsim
```

### 2. Create a Branch
```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Make changes and commit
git add .
git commit -m "Add: description of your changes"
```

### 3. Submit a Pull Request
- Push to your fork
- Create a Pull Request with detailed description
- Ensure all tests pass

### Development Guidelines
- Follow PEP 8 for Python code
- Write descriptive commit messages
- Update documentation for new features
- Add tests for new functionality

---

## 📮 Contact & Support

- **Repository**: [ros2-mobile-robot-arm-gzsim](https://github.com/muhammet-alaybey-cilesiz/ros2-mobile-robot-arm-gzsim)
- **Issues**: [GitHub Issues](https://github.com/muhammet-alaybey-cilesiz/ros2-mobile-robot-arm-gzsim/issues)
- **Discussions**: [GitHub Discussions](https://github.com/muhammet-alaybey-cilesiz/ros2-mobile-robot-arm-gzsim/discussions)

---

## 🌟 Acknowledgments

- ROS2 Community
- Gazebo Development Team
- Open source robotics enthusiasts

---

<div align="center">

**Made with ❤️ for the robotics community**

If you find this project helpful, please consider giving it a ⭐ star!

</div>
