# SolidCraft CAD Learning Track

This track supports the robot-description and simulation phases of the robotics roadmap.

## Skills to develop
1. Sketching and geometric constraints
2. Parametric features and dimension-driven modelling
3. Extrusion, revolution, fillets, chamfers, and patterns
4. Part organisation and assemblies
5. Coordinate systems, origins, and joint axes
6. Simplifying geometry for simulation
7. Exporting meshes using formats supported by the installed SolidCraft version

## Suggested practice sequence
- Model a wheel and axle.
- Model a rectangular chassis with mounting holes.
- Design a camera or lidar mounting bracket.
- Assemble the chassis, wheels, and sensor mounts.
- Create a simplified robot assembly suitable for a URDF-based simulation workflow.

## CAD-to-robot workflow
1. Choose a consistent unit system.
2. Set meaningful part origins and local coordinate frames.
3. Keep visual meshes separate from simplified collision geometry where practical.
4. Check dimensions, mass properties, and joint axes.
5. Verify SolidCraft's supported export formats and conversion requirements.
6. Import the resulting geometry into the robot description and inspect it in RViz2/Gazebo.

## Learning log
For each model, save screenshots, dimensions, export settings, known limitations, and the related URDF/Xacro changes.

**Important:** menu names and export options vary by SolidCraft version. Consult the documentation for the exact version installed rather than assuming a particular menu path or file format.
