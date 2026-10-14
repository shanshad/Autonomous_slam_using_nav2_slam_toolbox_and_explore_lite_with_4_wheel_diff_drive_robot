# Autonomous SLAM using Nav2, SLAM Toolbox and explore_lite with a 4-Wheel Differential Drive Robot

Autonomous frontier-based exploration and mapping with a 4-wheel differential drive robot in Gazebo Harmonic, using ROS 2 Jazzy on Ubuntu 24.04.

## Demo

[Watch the demo video](https://github.com/shanshad/Autonomous_slam_using_nav2_slam_toolbox_and_explore_lite_with_4_wheel_diff_drive_robot/blob/main/Screencast%20from%202026-10-14%2023-31-40.mp4)

## Requirements

- Ubuntu 24.04
- ROS 2 Jazzy
- Gazebo Harmonic

## Install Dependencies

```bash
sudo apt update
sudo apt install -y \
  ros-jazzy-desktop \
  ros-jazzy-ros-gz \
  ros-jazzy-xacro \
  ros-jazzy-robot-state-publisher \
  ros-jazzy-joint-state-publisher \
  ros-jazzy-rviz2 \
  ros-jazzy-nav2-bringup \
  ros-jazzy-nav2-map-server \
  ros-jazzy-slam-toolbox \
  ros-jazzy-explore-lite \
  python3-colcon-common-extensions
```

If `ros-jazzy-explore-lite` is not available, build it from source:

```bash
mkdir -p ~/explore_ws/src && cd ~/explore_ws/src
git clone https://github.com/robo-friends/m-explore-ros2.git
cd ~/explore_ws
rosdep install --from-paths src -yi
colcon build --symlink-install
echo "source ~/explore_ws/install/setup.bash" >> ~/.bashrc
```

## Build

```bash
git clone https://github.com/shanshad/Autonomous_slam_using_nav2_slam_toolbox_and_explore_lite_with_4_wheel_diff_drive_robot.git
cd Autonomous_slam_using_nav2_slam_toolbox_and_explore_lite_with_4_wheel_diff_drive_robot/ws
rosdep install --from-paths src -yi
colcon build --symlink-install
source install/setup.bash
```

## Run

Open each command in a new terminal and source `/opt/ros/jazzy/setup.bash` and `ws/install/setup.bash` in each.

**1. Gazebo, robot and RViz**
```bash
ros2 launch my_robot_bringup robot.launch.xml
```

**2. SLAM Toolbox**
```bash
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=true
```

**3. Nav2** (wait until all nodes are active)
```bash
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=true
```

**4. explore_lite**
```bash
ros2 launch explore_lite explore.launch.py use_sim_time:=true
```

The robot will now explore the environment on its own.

## Save the Map

```bash
ros2 run nav2_map_server map_saver_cli -f ~/my_map
```

## Repository Structure

```
ws/src/
├── my_robot_description/   # URDF/Xacro robot model
└── my_robot_bringup/       # Launch files
```
