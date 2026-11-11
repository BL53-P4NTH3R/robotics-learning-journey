# 48-Week Robotics Learning Roadmap

**Target effort:** 15–20 hours/week  
**Approach:** theory + implementation + simulation + documentation  
**Long-term direction:** robotics research and practical robotics engineering, especially robot perception and vision.

## Phase 1 — Mathematical and robotics foundations (Weeks 1–4)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 1 | Python scientific stack; vectors, matrices, coordinate frames | NumPy exercises; transform points between frames |
| 2 | Linear algebra, rotations, quaternions, homogeneous transforms | Implement 2D/3D transforms and visualise coordinate frames |
| 3 | Rigid-body motion, forward and inverse kinematics | Work through planar-arm examples; implement forward kinematics |
| 4 | Probability, Bayes' rule, Gaussian noise, robot motion models | Simulate noisy range/odometry measurements and estimate state |

**Core reference:** [Modern Robotics](https://modernrobotics.org/).

## Phase 2 — ROS 2 fundamentals (Weeks 5–10)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 5 | Linux terminal, workspaces, packages, nodes, executors | Create and run a Python ROS 2 package |
| 6 | Topics, publishers, subscribers, message types | Build a sensor publisher and data logger |
| 7 | Services, clients, actions | Implement a service and a long-running action |
| 8 | Parameters, YAML, launch files | Configure and launch a multi-node system |
| 9 | Custom interfaces, QoS, rosbag2 | Define a custom message; record and replay sensor topics |
| 10 | Debugging, lifecycle concepts, testing | Add launch tests and document common CLI workflows |

**Evidence:** a small ROS 2 package with nodes, launch configuration, custom interface, tests, and a README.

## Phase 3 — Frames, robot description, and visualisation (Weeks 11–14)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 11 | TF2 concepts and coordinate-frame trees | Publish and inspect a frame tree |
| 12 | URDF fundamentals: links, joints, inertial and collision properties | Describe a simple differential-drive robot |
| 13 | Xacro, reusable robot descriptions, meshes | Parameterise the robot model |
| 14 | RViz2, robot_state_publisher, joint states | Visualise the robot and validate its transforms |

## Phase 4 — CAD and simulation (Weeks 15–19)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 15 | SolidCraft interface, sketches, constraints, dimensions | Model simple mechanical parts |
| 16 | Extrusions, revolutions, patterns, fillets, assemblies | Build a wheel, chassis, and sensor mount |
| 17 | Robot assembly and export workflow | Prepare a simplified robot assembly for simulation |
| 18 | Gazebo worlds, physics, collision and inertial properties | Create a basic indoor world and spawn the robot |
| 19 | Simulated sensors: camera, depth, lidar, IMU | Publish and inspect simulated sensor data |

**Note:** verify SolidCraft's supported export formats and your installed Gazebo version before choosing a CAD-to-URDF conversion workflow.

## Phase 5 — ROS 2 computer vision (Weeks 20–25)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 20 | Images, colour spaces, filtering, edges | Build an OpenCV image-processing node |
| 21 | ROS image messages, cv_bridge, image_transport | Subscribe to a camera topic and publish processed images |
| 22 | Camera models, intrinsic calibration, distortion | Calibrate a camera and document reprojection error |
| 23 | Feature detection, descriptors, matching | Compare ORB feature matches across views |
| 24 | Object detection and tracking | Integrate a detector and track objects over time |
| 25 | Segmentation and visual perception pipeline design | Publish detections/masks with timestamps and frame IDs |

## Phase 6 — Depth, point clouds, and 3D perception (Weeks 26–30)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 26 | Stereo geometry and depth estimation | Estimate depth from a stereo pair |
| 27 | RGB-D cameras and depth-image processing | Convert depth pixels to 3D points |
| 28 | Point-cloud representations and PCL concepts | Filter and visualise a point cloud |
| 29 | 3D geometry, clustering, plane fitting | Segment a tabletop or ground plane |
| 30 | 3D object localisation and sensor fusion | Estimate object position in the robot frame |

## Phase 7 — Visual odometry and SLAM (Weeks 31–36)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 31 | Image geometry, epipolar constraints, triangulation | Implement a small two-view geometry exercise |
| 32 | Visual odometry pipeline | Track features and estimate relative camera motion |
| 33 | Odometry, IMU models, EKF fundamentals | Fuse simulated wheel odometry and IMU data |
| 34 | Occupancy grids and 2D SLAM | Run a ROS 2-compatible SLAM package in simulation |
| 35 | Visual/inertial SLAM and graph optimisation concepts | Run and evaluate a visual or visual-inertial SLAM system |
| 36 | SLAM evaluation and failure analysis | Compare trajectories and document drift/failure cases |

## Phase 8 — Navigation, control, and manipulation (Weeks 37–41)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 37 | Differential-drive control and ros2_control concepts | Control simulated wheel joints |
| 38 | Localisation and map-based navigation | Localise the robot in a known map |
| 39 | Nav2 behaviour trees, planners, costmaps | Navigate between multiple goals |
| 40 | Obstacle avoidance and recovery behaviours | Test dynamic obstacles and recovery cases |
| 41 | Manipulation foundations and MoveIt 2 overview | Model a simple arm and plan a basic motion |

## Phase 9 — Advanced perception and research directions (Weeks 42–45)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 42 | 3D scene representations and multi-view geometry | Review and reproduce a small scene-reconstruction experiment |
| 43 | Neural scene representations and 3D Gaussian Splatting | Run an available 3DGS baseline on a suitable small dataset |
| 44 | Vision-language models and grounded perception | Test image-text querying on a controlled dataset |
| 45 | Semantic mapping and visual servoing concepts | Prototype semantic labels in a map or image-based control demo |

## Phase 10 — Integrated capstone (Weeks 46–48)
| Week | Focus | Practical work / evidence |
|---|---|---|
| 46 | System architecture and integration | Define interfaces, frames, sensors, and acceptance tests |
| 47 | End-to-end implementation and evaluation | Integrate simulation, perception, localisation, and navigation |
| 48 | Final evaluation and communication | Publish code, architecture diagram, results, limitations, and demo |

## Weekly time budget
A practical 18-hour target:
- 4 hours: mathematics, concepts, and reading
- 5 hours: guided tutorials and implementation
- 6 hours: independent coding and simulation
- 2 hours: debugging and evaluation
- 1 hour: notes, Git commits, and weekly review

## Completion standard
For each major topic, be able to explain the underlying idea, implement or configure a working example, test it, diagnose at least one failure mode, and document the result. Extend a phase when these criteria are not yet met.
