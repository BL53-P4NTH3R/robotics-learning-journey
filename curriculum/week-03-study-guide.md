# Week 3 Study Guide — Rigid-Body Motion and Robot-Arm Kinematics

**Dates:** Monday, 30 November to Sunday, 6 December 2026  
**Target effort:** 15–20 hours (18 hours recommended)  
**Roadmap phase:** Phase 1, Mathematical and robotics foundations  
**Prerequisites:** Week 1 vectors, matrices, and coordinate frames; Week 2 rotations and homogeneous transformations.

> This is a planned guide. It does not imply that Weeks 1 or 2 have been completed. If transformation composition or rotation matrices are still unclear, review them before proceeding.

## Why this week matters

Kinematics connects joint motion to the movement of a robot's links and end-effector. It is foundational for robot-arm control, manipulation, and later motion planning.

You will start with a two-link planar arm because its geometry is accessible and its forward and inverse kinematics can be checked analytically. You will then represent the same arm as a chain of rigid transformations.

This is still a foundations week. Do not move on to ROS 2, URDF, Gazebo, or robot bringup yet.

## Learning outcomes

By the end of the week, you should be able to:

1. Explain configuration, degrees of freedom (DoF), joint variables, links, and end-effectors.
2. Distinguish configuration space from reachable workspace.
3. Calculate a two-link planar arm's end-effector position using forward kinematics.
4. Derive and implement the two-link planar inverse-kinematics equations.
5. Explain why an inverse-kinematics target can have zero, one, or multiple solutions.
6. Identify unreachable targets and describe singular configurations geometrically.
7. Represent a simple serial chain using homogeneous transformations.
8. Verify geometric forward kinematics against a matrix-based implementation.
9. Visualise the arm and its reachable workspace in Python.

## Required resources

### Modern Robotics

Use these sections selectively:

- Chapter 2 — Configuration Space: degrees of freedom, robot configurations, and workspace.
- Chapter 4 — Forward Kinematics: the forward-kinematics problem and product-of-exponentials perspective. Begin with the direct geometric derivation for this week's two-link planar arm.
- Chapter 6 — Inverse Kinematics: introductory material on the inverse problem. Numerical methods are optional enrichment, not a core requirement this week.

Resources:
- [Modern Robotics book and course resources](https://modernrobotics.org/)
- [Modern Robotics book pages and chapter videos](https://modernrobotics.northwestern.edu/nu-gm-book-resource/)
- [Chapter 4: Forward Kinematics](https://modernrobotics.northwestern.edu/nu-gm-book-resource/foundations-of-robot-motion/)
- [Modern Robotics code library](https://github.com/NxRLab/ModernRobotics)
- [Matplotlib documentation](https://matplotlib.org/stable/)

The official Modern Robotics course materials list forward kinematics in Chapter 4 and inverse kinematics in Chapter 6. <https://modernrobotics.northwestern.edu/nu-gm-book-resource/> 

## Conventions for the two-link planar arm

Use a two-revolute-joint (2R) arm:

- Link 1 has length L1.
- Link 2 has length L2.
- Joint 1 angle theta1 is measured from the positive x-axis.
- Joint 2 angle theta2 is measured relative to link 1.
- Positive angles are counter-clockwise.
- The base is at (0, 0).
- Python functions accept angles in radians.

The end-effector position is:

    x = L1*cos(theta1) + L2*cos(theta1 + theta2)
    y = L1*sin(theta1) + L2*sin(theta1 + theta2)

For inverse kinematics, given target (x, y), calculate:

    c2 = (x*x + y*y - L1*L1 - L2*L2) / (2*L1*L2)
    theta2 = atan2(±sqrt(1 - c2*c2), c2)
    theta1 = atan2(y, x) - atan2(L2*sin(theta2), L1 + L2*cos(theta2))

The two signs represent the two common elbow branches. A target is reachable only when:

    abs(L1 - L2) <= sqrt(x*x + y*y) <= L1 + L2

Handle boundary cases and small floating-point errors explicitly. Do not allow invalid square roots or divisions to silently produce incorrect answers.

## Study plan

This schedule totals approximately 18 hours.

| Day | Time | Study and implementation |
|---|---:|---|
| Monday, 30 Nov | 2 h | Review homogeneous transforms. Read about configuration, DoF, and workspace. |
| Tuesday, 1 Dec | 3 h | Study links, joints, and joint variables. Derive the two-link planar forward-kinematics equations by resolving each link into x/y components. |
| Wednesday, 2 Dec | 3 h | Implement forward kinematics. Test configurations and plot the arm and end-effector. |
| Thursday, 3 Dec | 3 h | Derive and implement inverse kinematics. Return both elbow branches and handle unreachable targets. |
| Friday, 4 Dec | 3 h | Compare forward and inverse kinematics. Explore workspace boundaries and singular configurations. |
| Saturday, 5 Dec | 3 h | Implement the arm as a chain of homogeneous transforms. Compare it with the geometric implementation and add tests. |
| Sunday, 6 Dec | 1 h | Complete self-assessment, document gaps, and commit your work. |

## Practical exercises

Suggested notebook or script: `week_03_planar_arm_kinematics.ipynb` or `week_03_planar_arm_kinematics.py`.

### Exercise 1: Configuration and degrees of freedom

Tasks:
- Draw and label the base, links, joints, and end-effector.
- Identify the two joint variables and explain why this model has two DoF.
- Choose link lengths, for example L1 = 2.0 and L2 = 1.5.
- Explain the difference between a configuration (joint angles) and an end-effector position.
- Describe configuration space versus workspace.

### Exercise 2: Forward kinematics

Implement a function called `forward_kinematics(theta1, theta2, L1, L2)`. It should return the elbow position and end-effector position.

Tasks:
- Derive the x and y equations before coding.
- Test (0, 0), (pi/2, 0), (0, pi/2), and (pi/4, -pi/2).
- Plot the links as line segments and mark the joints.
- Label axes and use equal scaling so the geometry is not distorted.
- Explain how each joint angle affects the end-effector.

### Exercise 3: Inverse kinematics

Implement `inverse_kinematics(x, y, L1, L2)`. It should:
- Check target reachability.
- Return both elbow-up and elbow-down solutions when distinct.
- Clearly report an unreachable target.
- Return radians and document the angle convention.
- Reject invalid link lengths.

Tasks:
- Choose several reachable targets.
- Calculate joint angles using inverse kinematics.
- Pass each solution into forward kinematics.
- Confirm that the recovered end-effector position matches the target within a numerical tolerance.
- Plot both configurations for a target with two distinct solutions.

Do not assume every target has exactly two distinct solutions. At workspace boundaries, branches can merge.

### Exercise 4: Workspace exploration

Tasks:
- Sample a range of valid joint angles.
- Plot the resulting end-effector positions.
- Compare the sampled region with the theoretical reach limits.
- Test a target outside maximum reach.
- If the link lengths differ, investigate the inner unreachable region near the base.

Explain why the workspace is not necessarily every point inside a circle, especially when link lengths differ or joints have limits.

### Exercise 5: Homogeneous-transform chain

Use 3x3 homogeneous matrices for this planar exercise. A link transform can be represented as:

    T_i = [[cos(theta_i), -sin(theta_i), L_i*cos(theta_i)],
           [sin(theta_i),  cos(theta_i), L_i*sin(theta_i)],
           [0,             0,            1]]

Be explicit about what each transform maps. Keep the convention consistent when composing them.

Tasks:
- Construct the transform for link 1 and link 2.
- Compose them in the correct order.
- Transform the end-effector origin into the base frame.
- Compare the result with your geometric forward-kinematics function.
- Test agreement across several configurations.

### Exercise 6: Singular configurations

Explore the arm when fully extended and when folded back along itself, where the geometry permits.

Tasks:
- Plot these configurations.
- Explain why small changes in end-effector targets can require large or poorly determined joint changes near some configurations.
- Identify the workspace boundary associated with a fully extended arm.
- Distinguish a geometrically reachable target from one that is well-conditioned for motion.

A full Jacobian derivation is not required this week; velocity kinematics and Jacobians come later.

## Testing requirements

Include tests for:

- With both angles zero, the end-effector is at (L1 + L2, 0).
- The elbow position is correct for a 90-degree first-joint angle.
- Forward kinematics returns finite coordinates for valid inputs.
- Inverse kinematics identifies a clearly unreachable target.
- Every returned inverse-kinematics solution reproduces its target through forward kinematics.
- Both elbow branches are represented for a suitable target.
- Boundary cases do not produce invalid square roots from floating-point error.
- Geometric and homogeneous-transform implementations agree.
- Invalid link lengths and malformed inputs are rejected clearly.

Use `numpy.allclose` or equivalent tolerance-based comparisons. Do not compare floating-point arrays using exact equality.

## Suggested project structure

Continue using your existing Python environment with NumPy and Matplotlib.

    robotics-foundations/
    └── week-03/
        ├── week_03_planar_arm_kinematics.ipynb
        ├── README.md
        └── figures/
            ├── arm_configurations.png
            └── reachable_workspace.png

Keep functions small and documented. Separate derivations, implementation, tests, and visualisations in the notebook.

## Required evidence by Sunday

- [ ] Labelled diagram of the two-link planar arm.
- [ ] Written derivation of the forward-kinematics equations.
- [ ] Tested forward-kinematics function.
- [ ] Tested inverse-kinematics function with both elbow branches.
- [ ] Explicit handling of unreachable targets and boundary cases.
- [ ] Workspace plot with a short explanation.
- [ ] Homogeneous-transform implementation of the same arm.
- [ ] Tests showing agreement between geometric and matrix-based forward kinematics.
- [ ] Explanation of configuration space, workspace, DoF, and singular configurations.
- [ ] Debugging log and Git commit.

## Self-assessment

Score each area from 0 to 5 and provide evidence.

| Area | Score (0–5) | Evidence |
|---|---:|---|
| Configuration and degrees of freedom |  |  |
| Forward-kinematics derivation |  |  |
| Forward-kinematics implementation |  |  |
| Inverse-kinematics derivation and branches |  |  |
| Workspace and reachability |  |  |
| Homogeneous-transform chain |  |  |
| Testing, debugging, and documentation |  |  |

A low score identifies what needs more practice. Do not move forward simply to stay on the calendar.

## Week 3 completion test

Without copying a tutorial, can you:

1. Explain the configuration of a two-joint planar arm?
2. Calculate its end-effector position from two joint angles?
3. Recover possible joint angles from a reachable target?
4. Explain why some targets are unreachable?
5. Demonstrate two elbow configurations for one target?
6. Represent the arm as a chain of homogeneous transforms?
7. Verify that both forward-kinematics implementations agree?
8. Explain what happens at a fully extended configuration?

If not, record the exact gap and revisit it before treating the week as complete.

## Next week's direction

Week 4 introduces probability, Bayes' rule, Gaussian noise, and simple robot motion and measurement models. You will simulate noisy measurements and reason about uncertainty before the ROS 2 phase begins in Week 5.
