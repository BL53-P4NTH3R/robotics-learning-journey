# Week 2 Study Guide — Rotations, Quaternions, and Homogeneous Transformations

**Dates:** Monday, 23 November to Sunday, 29 November 2026  
**Target effort:** 15–20 hours (use 18 hours as the planning target)  
**Roadmap phase:** Phase 1, Mathematical and robotics foundations  
**Prerequisite:** Week 1 concepts: Python/NumPy, vectors, matrices, and the meaning of coordinate frames.

> This is the planned Week 2 guide. It does not imply that Week 1 has been completed. If Week 1 concepts are still unclear, spend the first sessions reviewing them before progressing.

## Why this week matters

A robot operates in multiple coordinate frames: the world, its base, individual links, cameras, depth sensors, and tools. Rotations and rigid transformations let us describe how these frames are oriented and positioned relative to one another.

This week extends the translation-only coordinate conversion from Week 1 to rotated 2D and 3D frames. You will implement the mathematics in Python and verify it with tests and visualisations.

This is still a mathematics and programming week. Do not move on to ROS 2, TF2, URDF, or robot bringup yet.

## Learning outcomes

By the end of the week, you should be able to:

1. Explain the difference between a position, orientation, and pose.
2. Construct 2D and 3D rotation matrices.
3. Explain and verify the key properties of a valid rotation matrix.
4. Apply a rotation matrix to a vector and compose rotations in a stated order.
5. Explain the purpose of Euler angles and why rotation order matters.
6. Represent a 3D rotation with a unit quaternion using a clearly stated component convention.
7. Combine rotation and translation in a homogeneous transformation matrix.
8. Compose and invert rigid transformations.
9. Transform a point between coordinate frames using consistent frame notation.
10. Implement and test these operations in Python/NumPy.

## Required resources

### Main textbook

**Modern Robotics — Lynch and Park**

Use Chapter 3, especially:
- §3.1: Rotations
- §3.2: Angular velocities (skim for context; detailed velocity work comes later)
- §3.3.1: Homogeneous Transformation Matrices

Start with the rotation and transformation sections that support this week's outcomes. Work through the examples rather than reading passively.

- [Modern Robotics textbook and course resources](https://modernrobotics.org/)
- [Chapter video: Homogeneous Transformation Matrices](https://modernrobotics.northwestern.edu/nu-gm-book-resource/3-3-1-homogeneous-transformation-matrices/)
- [Modern Robotics code library](https://github.com/NxRLab/ModernRobotics)

### Supporting references

- [NumPy Quickstart](https://numpy.org/doc/stable/user/quickstart.html): revisit matrix multiplication, transpose, array shape, and numerical operations.
- [MATLAB: Coordinate Transformations in Robotics](https://www.mathworks.com/help/robotics/ug/coordinate-transformations-in-robotics.html): use the explanations and diagrams as a second reference for rotation matrices, quaternions, and homogeneous transforms. The implementation this week remains Python/NumPy.

## Conventions used in this guide

Notation matters. Keep the same convention in your notes and code:

- `A` and `B` denote coordinate frames.
- `p_B` is a point expressed using coordinates in frame B.
- `R_AB` rotates coordinates expressed in B into coordinates expressed in A.
- `t_AB` is the position of frame B's origin expressed in frame A.
- `T_AB` maps a point represented in B into a representation in A.

Therefore:

`p_A = R_AB @ p_B + t_AB`

Using homogeneous coordinates:

`T_AB = [[R_AB, t_AB], [0, 0, 0, 1]]`

and:

`[p_A, 1]ᵀ = T_AB @ [p_B, 1]ᵀ`

For a 2D transform, use a 3×3 homogeneous matrix. For a 3D transform, use a 4×4 matrix.

**Important:** a transform's subscripts tell you what it maps. If `T_AB` maps B coordinates to A coordinates and `T_BC` maps C coordinates to B coordinates, then:

`T_AC = T_AB @ T_BC`

The order is not interchangeable.

## Study plan

This schedule totals approximately 18 hours.

| Day | Time | Study and implementation |
|---|---:|---|
| Monday, 23 Nov | 2 h | Review Week 1 matrix operations and coordinate frames. Read the introduction to rotations in Modern Robotics. |
| Tuesday, 24 Nov | 3 h | Derive and implement 2D rotation matrices. Rotate points by 0°, 90°, 180°, and 270°. Plot the original and rotated points. |
| Wednesday, 25 Nov | 3 h | Implement 3D rotations about the x-, y-, and z-axes. Check orthogonality, determinant, and preservation of vector length. |
| Thursday, 26 Nov | 3 h | Study rotation composition and Euler-angle ordering. Compare two different rotation orders and explain why they produce different results. |
| Friday, 27 Nov | 3 h | Study unit quaternions and implement conversion between a unit quaternion and a rotation matrix. State the component ordering in every function and note. |
| Saturday, 28 Nov | 3 h | Implement homogeneous transformations, composition, inversion, and point transformation. Add tests and visualisations. |
| Sunday, 29 Nov | 1 h | Complete the self-assessment, clean up the notebook, document limitations, and record any concepts to revisit. |

## Core concepts and exercises

Suggested notebook or script: `week_02_rotations_transforms.ipynb` or `week_02_rotations_transforms.py`.

### Exercise 1: 2D rotation matrices

Implement:

`R(θ) = [[cos(θ), -sin(θ)], [sin(θ), cos(θ)]]`

Tasks:
- Write a function that accepts an angle in radians and returns a 2×2 rotation matrix.
- Rotate the vector `[1, 0]` by 0°, 90°, 180°, and 270°.
- Plot the original and rotated vectors using Matplotlib.
- Explain why the trigonometric functions in Python expect radians.

Expected checks:
- A 90° counter-clockwise rotation maps `[1, 0]` to approximately `[0, 1]`.
- A 180° rotation maps `[1, 0]` to approximately `[-1, 0]`.
- Floating-point results may contain very small numerical errors; use a tolerance in tests.

### Exercise 2: 3D rotation matrices

Implement the elementary rotations:

`R_x(θ) = [[1,0,0], [0,cosθ,-sinθ], [0,sinθ,cosθ]]`

`R_y(θ) = [[cosθ,0,sinθ], [0,1,0], [-sinθ,0,cosθ]]`

`R_z(θ) = [[cosθ,-sinθ,0], [sinθ,cosθ,0], [0,0,1]]`

Tasks:
- Implement one function per axis.
- Rotate the unit vectors about each axis.
- Test 90° rotations and explain which coordinates change.
- Compare rotating a vector around x then z with rotating it around z then x.

For a valid rotation matrix `R`, verify:

- `R.T @ R` is approximately the identity matrix.
- `det(R)` is approximately +1.
- Rotating a vector preserves its Euclidean length.

Use `numpy.allclose` for numerical checks.

### Exercise 3: Rotation order and Euler angles

A sequence of rotations must state both the axes and the convention being used. Rotations generally do not commute.

Tasks:
- Choose one 3D vector.
- Apply a 90° rotation about x followed by a 90° rotation about z.
- Reverse the order and compare the results.
- Write down the matrix multiplication order you used.
- Explain why the results differ.

You do not need to implement every Euler-angle convention. Your goal is to understand that roll, pitch, and yaw are meaningful only when the rotation order and intrinsic/extrinsic convention are specified.

### Exercise 4: Unit quaternions

Use the scalar-first convention:

`q = [w, x, y, z]`

A unit quaternion has norm 1. For a rotation by angle `θ` around a unit axis `[u_x, u_y, u_z]`:

`q = [cos(θ/2), u_x sin(θ/2), u_y sin(θ/2), u_z sin(θ/2)]`

Tasks:
- Implement a function that constructs a quaternion from a unit axis and angle.
- Validate that the axis is non-zero and normalise it.
- Implement conversion from a scalar-first unit quaternion to a 3×3 rotation matrix.
- Test a 90° rotation around the z-axis and compare its effect with the equivalent rotation matrix.
- Explain why a quaternion and its negation represent the same orientation.

Do not mix scalar-first `[w, x, y, z]` and scalar-last `[x, y, z, w]` conventions. Some software libraries use different conventions; always check the API before exchanging quaternion values.

### Exercise 5: Homogeneous transformations

A 3D homogeneous transform has this structure:

`T_AB = [[R_AB, t_AB], [0, 0, 0, 1]]`

Tasks:
- Implement a function that accepts a 3×3 rotation matrix and a 3D translation vector and returns a 4×4 transform.
- Convert a 3D point to homogeneous coordinates by appending a 1.
- Transform the point from frame B into frame A.
- Construct two transforms, `T_AB` and `T_BC`, and calculate `T_AC = T_AB @ T_BC`.
- Verify the composed transform by applying the two transforms sequentially to a point.
- Implement the inverse using the rigid-transform structure:

`T_BA = [[R_AB.T, -R_AB.T @ t_AB], [0, 0, 0, 1]]`

- Check that `T_AB @ T_BA` is approximately the 4×4 identity matrix.

Also implement a 2D homogeneous transform using a 3×3 matrix. This connects the 2D rotation work to the 3D representation.

## Testing requirements

Include tests for the following:

- A zero-angle rotation leaves a vector unchanged.
- A 90° 2D rotation maps the positive x-axis to the positive y-axis.
- A rotation matrix is orthogonal and has determinant approximately +1.
- Rotation preserves vector length.
- Rotation order is demonstrated with a non-trivial example.
- The quaternion for a unit axis has unit norm.
- A quaternion-derived rotation matrix agrees with the equivalent axis-angle rotation matrix.
- Applying a transform and its inverse returns the original point.
- Composing two transforms gives the same result as applying them sequentially.
- Invalid shapes and zero-length rotation axes are handled clearly.

Use tolerances for floating-point comparisons; do not compare floating-point arrays with exact equality.

## Suggested project setup

Continue using the Week 1 Python virtual environment if it is available. Install Matplotlib if it is not already installed:

```bash
python -m pip install numpy matplotlib
```

Keep the work in a clearly named folder, for example:

```text
robotics-foundations/
└── week-02/
    ├── week_02_rotations_transforms.ipynb
    ├── README.md
    └── figures/
```

Your notebook should contain short explanations, readable functions, test cases, and plots. Avoid putting the entire implementation in one large cell.

## Required evidence by Sunday

- [ ] A runnable Python notebook or script implementing 2D and 3D rotations.
- [ ] Plots showing the effect of selected 2D and 3D rotations.
- [ ] Tests for rotation-matrix properties.
- [ ] A comparison showing that rotation order matters.
- [ ] A scalar-first unit-quaternion implementation and a comparison with a rotation matrix.
- [ ] 2D and 3D homogeneous transformation implementations.
- [ ] Tests for transform composition and inversion.
- [ ] Notes defining the frame convention used in the code.
- [ ] A short debugging log and a Git commit.

## Self-assessment

Score each area from 0 to 5 and provide evidence.

| Area | Score (0–5) | Evidence |
|---|---:|---|
| 2D and 3D rotation matrices |  |  |
| Rotation-matrix properties |  |  |
| Rotation composition and ordering |  |  |
| Quaternion representation |  |  |
| Homogeneous transformations |  |  |
| Transform composition and inversion |  |  |
| Testing, debugging, and documentation |  |  |

A score is a prompt for reflection, not a reason to rush. Revisit any concept you cannot explain or verify.

## Week 2 completion test

Without copying a tutorial, can you:

1. Rotate a 2D vector by 90° using a matrix?
2. Construct a 3D rotation matrix about each principal axis?
3. Check that a matrix is a valid rotation matrix?
4. Demonstrate why rotation order matters?
5. Construct a unit quaternion using the scalar-first convention?
6. Build a homogeneous transform from rotation and translation?
7. Compose two transforms using the frame labels correctly?
8. Invert a rigid transform and verify the result numerically?

If not, note the exact gap and revisit it before treating the week as complete.

## Next week's direction

Week 3 moves from describing poses to describing robot motion: rigid-body motion and introductory forward and inverse kinematics. The next deliverable will be a tested planar robot-arm model with a clear explanation of its joint variables and end-effector position.
