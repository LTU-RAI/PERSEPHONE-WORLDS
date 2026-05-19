
<p align="center">
  <img src="assets/persephone_blue_2.webp" alt="PERSEPHONE Project" width="100%">
</p>

<p align="center">
  <strong>Simulation world environments for mining robotics</strong><br>
  Compatible with ROS 2 Humble and Ubuntu 22.04
</p>

---

## Overview

PERSEPHONE-WORLDS is a collection of high-fidelity Gazebo simulation environments developed within the [PERSEPHONE project](https://www.persephone-mining.eu) — a European initiative focused on robotic inspection and monitoring of underground mining infrastructure.

The repository provides eleven ready-to-launch SDF world files and their corresponding Gazebo model packages, covering realistic underground mine geometries (including hazard variants), a navigation benchmark maze, and indoor logistics environments.

> This project has received funding from the European Union's Horizon Europe Research and Innovation Programme under Grant Agreement No. 101138451.

## World Environments

### Underground Mine Environments

Based on the real abandoned Koutzi magnesite mine in Greece. All mine worlds use textured OBJ meshes with realistic cave-wall materials.

<p align="center">
  <img src="assets/remesh-showcase.png" alt="Koutzi Mine Mesh Showcase" width="100%">
</p>

| World File | Description |
|---|---|
| `Koutzi-UG-Mine.sdf` | Full-scale baseline mine — clean tunnel geometry |
| `Koutzi-UG-Mine-small.sdf` | Rescaled variant with ~2 m × 2 m cross-section for narrow-corridor testing |
| `Koutzi-UG-Mine-deformed.sdf` | Baseline mine with tunnel deformation (structural hazard scenario) |
| `Koutzi-UG-Mine-rockfall.sdf` | Baseline mine with rockfall debris obstacles |
| `Koutzi-UG-Mine-deformed-and-rockfall.sdf` | Combined deformation and rockfall — worst-case hazard scenario |
| `GM-KUM.sdf` | Grecian Magnesite – Koutzi Underground Mine in alternative STL/OBJ mesh format |
| `mines.sdf` | Generic mine tunnel with cave-wall texture |
| `mines_with_magnesite.sdf` | Generic mine with embedded magnesite mineral deposit geometry |

**Example texture:**

<p align="center">
  <img src="assets/pngtree-cave-wall-texture-the-perfect-backdrop-for-an-archeological-concept-background-image_13636444.png" alt="Cave Wall Texture" width="80%">
</p>


## Usage with ROS 2 Humble

### Requirements

- [ROS 2 Humble](https://docs.ros.org/en/humble/Installation.html)
- [Ignition Fortress](https://gazebosim.org/docs/fortress/install)


```bash
sudo apt install ros-humble-ros-gz
```

### 1. Set the Gazebo model path

The worlds reference meshes via `model://` URIs. Set the resource path once per session (or add to your `.bashrc`):

```bash
export IGN_GAZEBO_RESOURCE_PATH=$IGN_GAZEBO_RESOURCE_PATH:/path/to/PERSEPHONE-WORLDS/meshes
```

### 2. Launch standalone (Ignition Gazebo)

```bash
ign gazebo /path/to/PERSEPHONE-WORLDS/worlds/<world_file>.sdf
```

### 3. Launch with ROS 2 Humble

```bash
source /opt/ros/humble/setup.bash

ros2 launch ros_gz_sim gz_sim.launch.py \
  gz_args:="/path/to/PERSEPHONE-WORLDS/worlds/<world_file>.sdf"
```

**Quick-reference — replace `<world_file>` with any of the following:**

| Environment | World file |
|---|---|
| Koutzi Mine (baseline) | `Koutzi-UG-Mine.sdf` |
| Koutzi Mine (small) | `Koutzi-UG-Mine-small.sdf` |
| Koutzi Mine (deformed) | `Koutzi-UG-Mine-deformed.sdf` |
| Koutzi Mine (rockfall) | `Koutzi-UG-Mine-rockfall.sdf` |
| Koutzi Mine (deformed + rockfall) | `Koutzi-UG-Mine-deformed-and-rockfall.sdf` |
| GM-KUM | `GM-KUM.sdf` |
| Generic mine | `mines.sdf` |
| Mine with magnesite | `mines_with_magnesite.sdf` |
| Maze | `maze.sdf` |
| Depot | `depot.sdf` |
| Warehouse | `warehouse.sdf` |

### 4. ROS–Gazebo bridge (optional)

To synchronise the simulation clock with ROS 2:

```bash
ros2 run ros_gz_bridge parameter_bridge \
  /clock@rosgraph_msgs/msg/Clock[ignition.msgs.Clock
```

---

## Mesh Customization

The OBJ and STL meshes can be remeshed in [Blender](https://www.blender.org) to achieve any desired level of detail:

<p align="center">
  <img src="assets/remesh-config.png" alt="Blender Remesh Configuration" width="80%">
</p>

1. Import the target mesh (`meshes/<model>/meshes/*.obj` or `*.stl`) into Blender.
2. Apply the **Remesh** modifier and adjust the voxel size or octree depth to the desired resolution.
3. Export as OBJ and update the corresponding `model.sdf` geometry URI if the filename changes.


## Contributors

| Name | Affiliation |
|---|---|
| Theodoros Antonios Frantzis | University of Patras |
| Akash Patel | Luleå University of Technology |
| Vignesh Kottayam Viswanathan | Luleå University of Technology |


<p align="center">
  <sub>Funded by the European Union's Horizon Europe Research and Innovation Programme · Grant Agreement No. 101138451</sub>
</p>
