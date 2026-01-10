# Reachy2 Isaac Sim Robot Model

This repository contains the complete robot model for Reachy2 humanoid robot, optimized for NVIDIA Isaac Sim simulation.

## Overview

Reachy2 is a humanoid robot with:
- Mobile base with 3 drive wheels
- Dual arms with 7-DOF manipulation capability
- Articulated head with Orbita neck mechanism
- Stereo cameras and LiDAR sensor
- Left and right grippers (Pincette)

**Robot Specifications:**
- 100 links
- 99 joints
- Complete visual and collision meshes
- Physics properties optimized for Isaac Sim

## Repository Structure

```
reachy2_isaac_repo/
├── meshes/                           # Robot mesh files (29 MB)
│   ├── *_visual.dae                  # High-detail visual meshes
│   └── *_collider.dae                # Collision meshes for physics
├── reachy2_isaac/                    # Isaac Sim optimized configuration
│   ├── reachy2_isaac.usd             # Main USD entry point
│   └── configuration/
│       ├── reachy2_isaac_base.usd    # Geometry definitions
│       ├── reachy2_isaac_physics.usd # Physics properties
│       ├── reachy2_isaac_robot.usd   # Robot structure
│       └── reachy2_isaac_sensor.usd  # Sensor configurations
├── usd/
│   ├── reachy2.usd                   # Scene with environment setup
│   └── reachy2_robot_1.usd           # Alternative robot model
├── reachy2_isaac.urdf                # URDF version (alternative)
└── README.md
```

## Getting Started

### Prerequisites

- NVIDIA Isaac Sim (tested with Isaac Sim 2023.1 or later)
- NVIDIA Omniverse

### Loading the Robot in Isaac Sim

**Method 1: Load USD directly (Recommended)**

1. Open Isaac Sim
2. Go to `File → Open`
3. Navigate to `reachy2_isaac/reachy2_isaac.usd`
4. Click Open

**Method 2: Load from URDF**

1. Open Isaac Sim
2. Go to `Isaac Utils → URDF Importer`
3. Select `reachy2_isaac.urdf`
4. Configure import settings (use default for best results)
5. Click Import

**Method 3: Load Scene with Environment**

1. Open Isaac Sim
2. Go to `File → Open`
3. Navigate to `usd/reachy2.usd`
4. This includes the robot with basic lighting and camera setup

## File Descriptions

### Essential Files

- **reachy2_isaac.usd**: Main entry point for loading the robot
- **reachy2_isaac.urdf**: URDF version with mesh references
- **meshes/*.dae**: All visual and collision mesh files (required)
- **configuration/*.usd**: Physics, sensor, and geometry configurations

### Mesh Files

All mesh files are in COLLADA (.dae) format:
- Visual meshes: High-polygon count for rendering
- Collision meshes: Simplified geometry for physics simulation

Total mesh size: ~29 MB

## Current Status

- ✅ Complete robot geometry and meshes
- ✅ Physics properties configured
- ✅ Sensor definitions (cameras, LiDAR)
- ⚠️ Control system: Not yet implemented
- ⚠️ Behavior scripts: Not yet implemented

This repository serves as a base model for further development of control algorithms and robot behaviors.

## Robot Components

### Mobile Base
- 3 omnidirectional drive wheels
- Base link with stabilization

### Arms (Left & Right)
- Shoulder: 3-DOF (pitch, roll, yaw)
- Elbow: 1-DOF
- Wrist: 3-DOF
- Gripper (Pincette): Multi-link articulated gripper

### Head
- Orbita neck mechanism (3-DOF ball joint)
- Stereo cameras (left/right)
- Depth camera
- ToF camera
- LiDAR sensor
- Antenna left/right

## Usage Examples

### Basic Loading (Python API)

```python
from omni.isaac.kit import SimulationApp
simulation_app = SimulationApp({"headless": False})

from omni.isaac.core import World
from omni.isaac.core.utils.stage import add_reference_to_stage

# Create world
world = World()

# Load Reachy2 robot
add_reference_to_stage(
    usd_path="reachy2_isaac/reachy2_isaac.usd",
    prim_path="/World/Reachy2"
)

# Run simulation
world.reset()
while simulation_app.is_running():
    world.step(render=True)

simulation_app.close()
```

## Contributing

This is currently a backup and reference repository. Future contributions for control systems, behavior implementations, and improvements are welcome.

## License

Please add appropriate license information based on your requirements.

## Acknowledgments

Robot model and meshes created for Isaac Sim simulation environment.

## Support

For issues or questions about using this model in Isaac Sim, please open an issue in this repository.

## Version History

- **v1.0** (Initial Release): Complete robot geometry and physics setup for Isaac Sim
  - 100 links, 99 joints
  - Full mesh library (32 files)
  - Optimized physics configuration
  - Basic sensor definitions
