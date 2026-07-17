# Two-Wheeled Robot URDF Description 

## 📖 Project Overview
This repository contains a complete ROS 2 robot description package for a custom two-wheeled differential drive mobile robot. The robot model is built entirely from scratch using URDF and Xacro macros to ensure clean, reusable, and modular code. It features a box-style chassis, two main drive wheels, a balancing caster wheel, and integrates custom STL meshes for an onboard LiDAR sensor and a ZED camera.

## 📂 Folder Structure
The package is organized according to standard ROS 2 conventions:

```text
robot_description_youssef_ahmed/
├── meshes/
│   ├── lidar.stl       # Custom 3D mesh for the top-mounted LiDAR
│   └── zed.stl         # Custom 3D mesh for the front-mounted camera
├── urdf/
│   └── robot.urdf.xacro # Core robot description file with Xacro macros
├── CMakeLists.txt      # Build configuration and install directives
├── package.xml         # Package metadata and ROS 2 dependencies
└── README.md           # Project documentation

```

## 🏗️ Robot Structure & Kinematic Hierarchy
The robot is constructed with accurate visual, collision, and inertial properties for every physical link. The kinematic chain is explicitly defined by the following parent-child joint relationships:

* **Link: `base_footprint`** (Root Link - 2D ground projection)
  * **Joint:** `base_footprint_joint` (Type: `fixed`)
    * **Parent:** `base_footprint`
    * **Child:** `base_link` (The main box chassis)

* **Link: `base_link`** (Main body) acts as the parent for all subsequent components:
  * **Joint:** `left_wheel_joint` (Type: `continuous`)
    * **Parent:** `base_link`
    * **Child:** `left_wheel`
  * **Joint:** `right_wheel_joint` (Type: `continuous`)
    * **Parent:** `base_link`
    * **Child:** `right_wheel`
  * **Joint:** `caster_wheel_joint` (Type: `fixed`)
    * **Parent:** `base_link`
    * **Child:** `caster_wheel`
  * **Joint:** `lidar_joint` (Type: `fixed`)
    * **Parent:** `base_link`
    * **Child:** `lidar_link` (Holds `lidar.stl` mesh)
  * **Joint:** `camera_joint` (Type: `fixed`)
    * **Parent:** `base_link`
    * **Child:** `camera_link` (Holds `zed.stl` mesh)




## ⚙️ Build Instructions

To build this package, clone the repository into your ROS 2 workspace and compile using `colcon`:

```bash
# Navigate to your workspace source directory
cd ~/ros2_ws/src

# Clone the repository
git clone [https://github.com/youssefradwan/robot_description_youssef_ahmed.git](https://github.com/youssefradwan/robot_description_youssef_ahmed.git)

# Navigate back to the workspace root
cd ~/ros2_ws

# Build the package
colcon build --packages-select robot_description_youssef_ahmed

# Source the overlay workspace
source install/setup.bash

```

## 🔍 How to Preview the Robot
This robot model can be visualized directly inside Visual Studio Code using the URDF Visualizer extension. To ensure the custom STL meshes for the LiDAR and camera load correctly, you must map the package path in your VS Code settings.

### 1. Configure VS Code Package Paths
1. Open Visual Studio Code.
2. Open Settings (`Ctrl + ,` on Windows/Linux or `Cmd + ,` on macOS).
3. Search for `urdf-visualizer.packages` and click **Edit in settings.json**.
4. Add the absolute path to this package on your local machine. It should look like this (be sure to replace the path with your actual directory structure):

```json
"urdf-visualizer.packages": {
    "robot_description_youssef_ahmed": "/absolute/path/to/your/workspace/src/robot_description_youssef_ahmed"
}
Save the settings.json file.

---

## 📸 Previews

### Full Robot Structure

<img width="463" height="331" alt="image" src="https://github.com/user-attachments/assets/8f059542-ebd4-412b-aebd-399cb7c9e6f6" />
<img width="394" height="291" alt="image" src="https://github.com/user-attachments/assets/00f2c3da-8495-4dcc-886c-f177632878e0" />
<img width="407" height="322" alt="image" src="https://github.com/user-attachments/assets/f90eedfe-c3f0-45af-ba25-2a97ba6c93c3" />
<img width="648" height="271" alt="image" src="https://github.com/user-attachments/assets/9b68a942-f571-4888-88c4-2e55cb067593" />
<img width="457" height="352" alt="image" src="https://github.com/user-attachments/assets/9e4c9033-b656-4a27-b552-41f98c33f81e" />

### Collision Boundaries

<img width="422" height="274" alt="image" src="https://github.com/user-attachments/assets/df8382ac-03d3-4b8c-9db2-ffec3dcf12ff" />


```

```
