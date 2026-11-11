# VisionBot — Integrated Robotics Capstone

## Objective
Build a simulation-first mobile robot that uses camera and range sensing to perceive its environment, estimate its motion, and navigate to goals while documenting system behaviour and limitations.

## Proposed system components
- Robot model: differential-drive mobile base described with URDF/Xacro.
- Simulation: Gazebo world with static and dynamic obstacles.
- ROS 2 integration: bringup launch files, TF2, sensor topics, and rosbag2.
- Perception: camera processing and object detection; depth or lidar-based obstacle information.
- State estimation: wheel odometry with optional IMU fusion.
- Mapping/localisation: a suitable 2D or visual SLAM baseline.
- Navigation: Nav2 planning, costmaps, and recovery behaviours.
- Visualisation: RViz2 displays for frames, sensors, maps, and planned paths.

## Milestones
1. Spawn and teleoperate the robot in a simple world.
2. Validate the robot's TF tree and sensor data.
3. Implement and test a perception node.
4. Generate a map and localise the robot.
5. Navigate to a sequence of goals.
6. Evaluate performance with repeatable scenarios.
7. Publish a technical report and demonstration.

## Evaluation ideas
- Successful goal completion across repeated trials
- Navigation time and path length
- Collision/near-collision events in simulation
- Detection quality on a labelled test set
- Localisation or trajectory error where ground truth is available
- Robustness to lighting, occlusion, sensor noise, and dynamic obstacles

## Required deliverables
- Source code and reproducible setup instructions
- Architecture and TF-tree diagrams
- Simulation world and robot description
- Recorded sensor data or short demonstration video
- Evaluation table and failure analysis
- Final report describing limitations and future work

Keep the scope achievable. A reliable, well-evaluated baseline is more valuable than an unfinished collection of advanced features.
