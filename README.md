# Gazebo LiDAR Obstacle Avoidance

A Gazebo simulation project demonstrating **LiDAR-based obstacle detection and obstacle avoidance** using a mobile robot.

This project was developed by following and implementing the sensor concepts from the official Gazebo Sensors tutorial. The simulation uses a **GPU LiDAR sensor** to detect obstacles around the robot, while a C++ node processes the LiDAR data.

## Project Overview

The robot is simulated in Gazebo with a LiDAR sensor attached to it.

The LiDAR continuously scans the surroundings and publishes distance measurements. The C++ node receives these measurements and uses them to detect obstacles in the robot's path.

```text
        Gazebo Simulation
               │
               ▼
          Mobile Robot
               │
               ▼
           GPU LiDAR
               │
               ▼
          /lidar topic
               │
               ▼
         lidar_node.cc
               │
               ▼
       Obstacle Detection
               │
               ▼
        Avoidance Decision
```

## Features

* Mobile robot simulation in Gazebo
* GPU LiDAR sensor
* Real-time LiDAR range measurements
* C++ LiDAR data processing
* Obstacle detection
* Distance-based obstacle avoidance
* Gazebo Transport communication
* CMake-based project

## Technologies Used

* **Gazebo Sim 6.18.0**
* **SDF**
* **C++**
* **CMake**
* **Gazebo Transport**
* **GPU LiDAR**
* **Ubuntu Linux**

## Project Structure

```text
gazebo-lidar-obstacle-avoidance/
│
├── main.sdf
├── lidar_node.cc
├── CMakeLists.txt
└── README.md
```

### `main.sdf`

Contains the Gazebo simulation environment, robot model, obstacles, and LiDAR sensor configuration.

The LiDAR sensor is attached to the robot and publishes its measurements to the `/lidar` topic.

### `lidar_node.cc`

A C++ program that subscribes to the LiDAR data and processes the sensor measurements.

The node is used to identify obstacles based on the distance returned by the LiDAR.

### `CMakeLists.txt`

Contains the build configuration required to compile `lidar_node.cc` and link it with the required Gazebo Transport libraries.

## How It Works

The LiDAR scans the environment around the robot and returns the distance between the sensor and surrounding objects.

When an obstacle is far away:

```text
Obstacle
    │
    │  Large distance
    │
    ▼
  Robot
```

When the robot approaches an obstacle:

```text
Obstacle
    │
    │  Small distance
    │
    ▼
  Robot
```

The LiDAR measurements are processed by `lidar_node.cc`. If an obstacle is detected within a predefined distance, the robot can make an avoidance decision.

## Building the Project

First, create a build directory:

```bash
mkdir build
cd build
```

Run CMake:

```bash
cmake ..
```

Compile the project:

```bash
make
```

After successful compilation, the LiDAR node executable will be created inside the `build` directory.

## Running the Simulation

From the project directory, launch the Gazebo simulation:

```bash
ign gazebo main.sdf
```

Start the simulation using the **Play** button in Gazebo.

In another terminal, the LiDAR topic can be monitored using:

```bash
ign topic -e -t /lidar
```

This displays the LiDAR sensor messages being published by the simulation.

## Testing

The project can be tested by moving the robot toward an obstacle.

During the test:

1. Start the Gazebo simulation.
2. Start the simulation using the Play button.
3. Run the LiDAR node.
4. Monitor the `/lidar` topic.
5. Move the robot toward an obstacle.
6. Observe the LiDAR distance measurements.
7. When the obstacle becomes closer, the node detects it.
8. The robot can then perform an avoidance movement.

## Example Obstacle Detection Logic

The basic idea of the obstacle detection system is:

```text
if detected_distance < safety_distance
        ↓
Obstacle detected
        ↓
Change robot movement
else
        ↓
Continue moving
```

## What I Learned

This project helped me understand:

* Gazebo simulation environments
* SDF world and robot configuration
* LiDAR sensor configuration
* GPU LiDAR in Gazebo
* Gazebo Transport topics
* C++ sensor-data processing
* CMake project configuration
* Real-time obstacle detection
* Basic autonomous obstacle avoidance

## Future Improvements

Possible extensions to this project include:

* Improve the obstacle avoidance algorithm
* Add left and right obstacle detection
* Add multiple obstacles
* Add dynamic obstacles
* Visualize LiDAR point-cloud data
* Integrate the project with ROS 2
* Connect Gazebo with ROS 2 using `ros_gz_bridge`
* Implement SLAM
* Integrate Nav2
* Build a larger autonomous navigation environment

## Reference

This project is based on concepts from the official Gazebo Sensors tutorial:

**Gazebo Sensors Tutorial**

https://github.com/gazebosim/docs/tree/master/jetty/tutorials/sensors

The tutorial covers sensor simulation in Gazebo, including LiDAR and other sensors.

## Author

Developed as a robotics simulation and learning project using Gazebo, C++, and LiDAR.

