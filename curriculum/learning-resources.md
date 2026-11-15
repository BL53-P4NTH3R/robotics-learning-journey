# Robotics Learning Resources

Use the official documentation for APIs and version-specific setup. Use textbooks for fundamentals, then validate concepts through implementation. Read actively: solve exercises, write small programs, and record assumptions and results.

## Mathematics and robotics

### Foundations (Weeks 1–4)
- [ROB 101 — Mathematics for Robotics (University of Michigan)](https://grizzle.robotics.umich.edu/files/ROB_101_Textbook_W_23_Grizzle_linked_to_GitHub.pdf). Use Chapter 2, **Vectors, Matrices, and Determinants**, as the introductory reading for Week 1. This is a mathematics bridge, not a complete substitute for a full linear algebra course.
- [NumPy Quickstart](https://numpy.org/doc/stable/user/quickstart.html). Focus on array creation, shape, indexing, elementwise operations, matrix multiplication with `@`, and basic linear algebra.
- [Python Tutorial](https://docs.python.org/3/tutorial/). Use the relevant sections as a refresher if functions, loops, lists, and imports are not comfortable yet.
- [Modern Robotics — textbook, videos, and course material](https://modernrobotics.org/). The book assumes prior linear algebra, calculus, introductory mechanics, and programming. Use it progressively; do not rush into the advanced chapters before the mathematical prerequisites are in place.
- [Modern Robotics chapter videos](https://modernrobotics.northwestern.edu/nu-gm-book-resource/). Use the videos alongside the matching textbook sections, not as a replacement for working through examples.
- [Modern Robotics code repository](https://github.com/NxRLab/ModernRobotics).
- [Probabilistic Robotics](https://mitpress.mit.edu/9780262201629/probabilistic-robotics/). A later reference for Weeks 4 and 31–36; it is not required as the first mathematics text.

### How to sequence the foundations
1. Week 1: Python/NumPy fluency, vectors, matrices, coordinate-frame meaning, and a basic 2D coordinate conversion.
2. Week 2: matrix operations, rotation matrices, quaternions, and homogeneous transformations.
3. Week 3: rigid-body motion and introductory forward/inverse kinematics.
4. Week 4: probability, Bayes' rule, Gaussian noise, and simple motion/measurement models.

## ROS 2 and simulation
- [ROS 2 tutorials](https://docs.ros.org/en/lyrical/Tutorials.html) — select the documentation matching your installed ROS 2 distribution.
- [Gazebo Jetty tutorials](https://gazebosim.org/docs/jetty/tutorials/) — check compatibility with your ROS/Gazebo installation.
- [ros_gz integration](https://github.com/gazebosim/ros_gz)
- [Nav2 documentation](https://docs.nav2.org/)
- [Nav2 source](https://github.com/ros-navigation/navigation2)
- [MoveIt 2 documentation](https://moveit.picknik.ai/)
- [MoveIt 2 source](https://github.com/ros-planning/moveit2)

## CAD and robot description
- Use the official SolidCraft documentation/help materials for the exact version installed.
- Learn sketches, constraints, parametric features, assemblies, coordinate systems, and mesh/export workflows.
- [ROS URDF tutorials](https://docs.ros.org/en/lyrical/Tutorials/Intermediate/URDF/URDF-Main.html)

## Computer vision
- [Szeliski — Computer Vision: Algorithms and Applications](https://szeliski.org/Book/)
- [OpenCV documentation](https://docs.opencv.org/)
- [vision_opencv](https://github.com/ros-perception/vision_opencv)
- [image_pipeline](https://github.com/ros-perception/image_pipeline)
- [perception_pcl](https://github.com/ros-perception/perception_pcl)

## Geometry, visual odometry, and SLAM
- [Multiple View Geometry](https://www.robots.ox.ac.uk/~vgg/hzbook/)
- [ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3)
- [RTAB-Map](https://github.com/introlab/rtabmap)
- [RTAB-Map ROS](https://github.com/introlab/rtabmap_ros)
- [OpenVINS](https://github.com/rpng/open_vins)

## Datasets for perception and SLAM
- [TUM RGB-D dataset](https://cvg.cit.tum.de/data/datasets/rgbd-dataset)
- [KITTI Vision Benchmark Suite](https://www.cvlibs.net/datasets/kitti/)
- [ETH3D](https://www.eth3d.net/)

## Neural scene representations and multimodal perception
- [3D Gaussian Splatting paper](https://arxiv.org/abs/2308.04079)
- [3D Gaussian Splatting reference implementation](https://github.com/graphdeco-inria/gaussian-splatting)
- [CLIP](https://github.com/openai/CLIP)
- [GroundingDINO](https://github.com/IDEA-Research/GroundingDINO)
- [Segment Anything](https://github.com/facebookresearch/segment-anything)

## Video learning
- [Articulated Robotics](https://www.youtube.com/@ArticulatedRobotics)
- [The Construct](https://www.youtube.com/@TheConstruct)
- [ROS Developers](https://www.youtube.com/@ROSDevelopers)
- [OpenCV](https://www.youtube.com/@OpenCV)
- [NVIDIA Developer](https://www.youtube.com/@NVIDIADeveloper)

## How to use these resources
1. Start with the relevant textbook section or official tutorial.
2. Reproduce the smallest working example.
3. Change one variable or component and observe the effect.
4. Record commands, versions, expected output, and errors.
5. Move to a research paper or advanced repository only after understanding the baseline.
