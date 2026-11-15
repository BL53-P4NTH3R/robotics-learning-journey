# Week 1 Study Guide — Python, Vectors, Matrices, and Coordinate Frames

**Dates:** Monday, 16 November to Sunday, 22 November 2026  
**Target effort:** 15–20 hours (use 18 hours as the planning target)  
**Roadmap phase:** Phase 1, Mathematical and robotics foundations

## Why this week comes first

Robotics depends on representing positions, directions, measurements, and coordinate frames precisely. This week establishes the Python and mathematical vocabulary needed for later work in transformations, kinematics, computer vision, and SLAM.

This is not a ROS 2 week. Do not spend this week configuring ROS, Gazebo, or robot bringup.

## Learning outcomes

By the end of the week, you should be able to:

1. Create and manipulate Python lists and NumPy arrays.
2. Explain the difference between a scalar, vector, and matrix.
3. Identify the shape and dimensions of a NumPy array.
4. Perform vector addition, scalar multiplication, dot products, and matrix multiplication.
5. Explain what a coordinate frame is and why a point's coordinates depend on the chosen frame.
6. Convert a 2D point between two coordinate frames whose axes are parallel but whose origins differ.
7. Write and test a small Python program that performs these operations.

## Required study resources

### 1. Mathematics reading

**ROB 101 — Mathematics for Robotics**, University of Michigan:

- Read Chapter 2, **Vectors, Matrices, and Determinants**.
- Prioritise vector notation, row and column vectors, matrix dimensions, matrix-vector multiplication, and the meaning of a determinant.
- Work through examples with pencil and paper. Do not spend the whole week trying to master every proof or abstract detail.

[Open the textbook PDF](https://grizzle.robotics.umich.edu/files/ROB_101_Textbook_W_23_Grizzle_linked_to_GitHub.pdf)

### 2. Python and NumPy

- [Official Python tutorial](https://docs.python.org/3/tutorial/): use the relevant sections on data structures, control flow, functions, and modules as a refresher.
- [NumPy Quickstart](https://numpy.org/doc/stable/user/quickstart.html): focus on array creation, shape, indexing, basic operations, and matrix multiplication.

### 3. Robotics context

- [Modern Robotics](https://modernrobotics.org/): use this as the main robotics reference throughout the programme. It assumes prior mathematical preparation, so this week use it only to understand why coordinate frames and vectors matter. The deeper treatment of rotations and homogeneous transformations belongs to Week 2.
- [Modern Robotics chapter videos](https://modernrobotics.northwestern.edu/nu-gm-book-resource/): optional orientation material. Do not try to complete the full course this week.

## Study plan

The following schedule totals approximately 18 hours. Move sessions around if necessary, but complete the learning outcomes and evidence by the end of the week.

| Day | Time | Study and implementation |
|---|---:|---|
| Monday, 16 Nov | 2 h | Set up or verify Python; review functions, lists, loops, imports, and writing/running a script. |
| Tuesday, 17 Nov | 3 h | Read the relevant parts of ROB 101 Chapter 2. Work through scalar, vector, matrix, dimensions, and matrix-vector examples by hand. |
| Wednesday, 18 Nov | 3 h | Complete the NumPy Quickstart sections on array creation, shape, indexing, and basic operations. Reproduce examples without copying line by line. |
| Thursday, 19 Nov | 3 h | Practise vector addition, subtraction, scaling, dot products, matrix multiplication, transpose, and shape checking in NumPy. |
| Friday, 20 Nov | 3 h | Study coordinate frames. Draw two 2D frames with parallel axes and different origins. Derive and implement the coordinate conversion described below. |
| Saturday, 21 Nov | 3 h | Complete the programming exercises, test normal and edge cases, and write explanations in your notebook or README. |
| Sunday, 22 Nov | 1 h | Complete the self-assessment, record blockers, and write the next week's measurable deliverable. |

## Practical exercises

Complete these in a Python file or Jupyter notebook. Suggested filename: `week_01_foundations.ipynb` or `week_01_foundations.py`.

### Exercise 1: Vectors

Create NumPy vectors and implement:

- Vector addition and subtraction
- Scalar multiplication
- Euclidean magnitude (norm)
- Dot product

Explain in your own words what the dot product tells you about the relationship between two vectors.

### Exercise 2: Matrices

Create at least two 2×2 matrices and:

- Inspect their `shape` and `ndim`
- Add and subtract them
- Multiply them element by element
- Multiply them using the matrix multiplication operator `@`
- Transpose one matrix
- Check the dimensions before multiplying

In your notes, explain why `A * B` and `A @ B` are not generally the same operation in NumPy.

### Exercise 3: Coordinate frames with parallel axes

Draw two 2D coordinate frames, A and B. Their x-axes point in the same direction and their y-axes point in the same direction, but their origins are different.

Let the position of B's origin expressed in frame A be:

`t_AB = [3, 2]`

Let a point P have coordinates in frame B:

`p_B = [1, 4]`

Because the axes are parallel, calculate the point's coordinates in frame A using:

`p_A = p_B + t_AB`

Implement this as a reusable Python function. Test it with at least three points and explain what changes if the origin of B moves.

**Scope boundary:** this first exercise uses aligned axes and translation only. Rotation matrices, rotated coordinate frames, and homogeneous transformation matrices are introduced in Week 2. This keeps the first week focused while still establishing the meaning of a coordinate frame.

### Exercise 4: Verification

Add tests that check:

- Adding a zero vector leaves a vector unchanged.
- Subtracting a vector from itself gives the zero vector.
- The magnitude of the zero vector is zero.
- Your coordinate conversion returns the expected result for the example above.
- Inputs with unexpected dimensions are rejected or clearly reported.

## Suggested project setup

Use a virtual environment so the learning dependencies remain separate from system Python.

```bash
mkdir -p robotics-foundations/week-01
cd robotics-foundations/week-01

python3 -m venv .venv
source .venv/bin/activate

python -m pip install --upgrade pip
python -m pip install numpy matplotlib

python -c "import numpy, matplotlib; print('NumPy:', numpy.__version__)"
```

If the virtual-environment command fails because the venv module is not installed, install the matching Python venv package for your Linux distribution or use an existing Python environment you already understand. Do not use `sudo pip install`.

## Required evidence by Sunday

- [ ] A runnable Python script or notebook containing all four exercises.
- [ ] Hand-worked examples of vector and matrix operations.
- [ ] A labelled drawing of frames A and B.
- [ ] A tested 2D coordinate conversion function.
- [ ] Short explanations of vector, matrix, array shape, matrix multiplication, and coordinate frames.
- [ ] A short record of errors encountered and how they were resolved.
- [ ] A Git commit containing the work.

## Self-assessment

Score each area from 0 to 5 and add one sentence of evidence:

| Area | Score (0–5) | Evidence |
|---|---:|---|
| Python fundamentals |  |  |
| Vector and matrix concepts |  |  |
| NumPy implementation |  |  |
| Coordinate-frame understanding |  |  |
| Testing and debugging |  |  |
| Documentation |  |  |

A low score is useful information, not a failure. Revisit unclear concepts before moving on.

## Week 1 completion test

Without copying a tutorial, can you:

1. Create a 2D vector and a 2×2 matrix in NumPy?
2. Explain their shapes?
3. Compute a dot product and a matrix product?
4. Explain why the same physical point can have different coordinates in different frames?
5. Convert a point between the two aligned frames in Exercise 3?
6. Run your tests and explain the results?

If any answer is no, record what needs more practice and carry it into the next study session.

## Next week's direction

Week 2 builds on this work with linear algebra, 2D and 3D rotations, quaternions, and homogeneous transformations. The next measurable deliverable will be a tested transformation module that composes and inverts rigid transformations.
