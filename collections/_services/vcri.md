---
title: "VCRI"
description: "VCANUS's Common Robot Interface"
date: 2019-10-03
weight: 2
header_transparent: true
fa_icon: false
icon: "assets/images/icons/icons8-color-palette-100.png"
thumbnail: "/assets/images/gen/services/service-2-thumbnail.webp"
image: "/assets/images/gen/services/service-2.webp"

hero:
  enabled: true
  heading: "VCRI"
  sub_heading: "Common Robot Interface"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: true
  background_image_blend_mode: false" # "overlay", "multiply", "screen"
  background_image: "/assets/images/gen/services/service-2.webp"
  fullscreen_mobile: false
  fullscreen_desktop: false
  height: 660px
  buttons:
    enabled: false
    list:
      - text: "Buy Now"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: false
        style: "primary"
---

# VCANUS Common Robot Interface (VCRI)

VCRI is a universal robot interface designed for virtual simulation and real-time control of industrial and collaborative robots. It provides a unified platform to manage multiple robot brands—such as KUKA, Stäubli, FANUC, ABB, and Neuromeka—through a single, common interface, eliminating the need for brand-specific programming. Additionally, VCRI integrates Beckhoff PLC functionality, enabling seamless I/O signal control (lamps, switches, buttons, etc.) essential for automation systems.
For large-scale manufacturers managing diverse robot fleets, VCRI simplifies setup, reduces programming time, and enhances system integration, making robot deployment and management faster, more efficient, and systematic.

## Why common robot interface is needed?

Traditional robot programming relies on teach pendants to manually embed teaching points—a time-consuming and labor-intensive process, especially when deploying multiple robots for identical tasks. VCRI streamlines this workflow by enabling:
- Virtual simulation for path verification and collision detection.
- Centralized control of multi-brand robots via a user-friendly GUI, eliminating the need for individual pendants.
- Synchronized motion between robots and external systems.
- Real-time monitoring and 3D visualization of robot status.
VCRI transforms robot management from a fragmented, brand-dependent process into a unified, efficient, and scalable solution.

## What you can do with VCRI

With VCRI, users can:
- Simulate and verify motion paths and detect collisions with obstacles in a virtual environment.
- Operate robots directly via an intuitive GUI, without relying on teach pendants.
- Synchronize robot and external system movements for precise, coordinated tasks.
- Monitor robot status in real time with 3D visualization.
- Create, simulate, and execute sequences—including point-to-point motion and custom tasks (e.g., pick-and-place, inspection, packaging, labeling).
- Program and utilize an embedded PLC for advanced automation logic.

## Key Features

### Robot Compatibility
- Industrial Robots: KUKA, Stäubli, FANUC, ABB, etc.
- Collaborative Robot: Rainbow Robotics, Doosan Robotics, Neuromeka

### Virtual Simulation
- User-defined 3D model management (tools, targets, obstacles).
- Motion feasibility verification and collision detection.
- Sequence simulation and validation.

### Direct Operation
- Manual/Auto operation modes.
- Jogging, rapid traverse, linear, and joint motion.
- Point-to-point and joint-angle motion control.

### Real-time Control & Synchronized Motion
- Data exchange with external systems (EtherCAT, TCP/IP, Beckhoff ADS).
- Cycle time: 4–10 ms (varies by robot and protocol).
- Velocity and position synchronization for multi-axis coordination.

### Real-time Monitoring & 3D Visualization
- Live monitoring of robot status (joint angles, positions, etc.).
- Real-time PLC value tracking.

### Sequence Control & Task Management
- Sequence control (start, stop, pause, reset).
- Task creation, registration, and management (point-to-point motion, PLC-linked custom tasks).

### Error Management
- Error compensation (setup error: coordinate compensation; position error: 3D table-based compensation).
- Error table management (registration, unregistration, updates).

### High Extensibility 
- Automatic path/sequence generation via CAM software integration (VC2AM).
- Compatibility with measurement devices (3D vision, ToF cameras, stereo cameras, etc.).

### PLC Programming & Utilization
- Supported languages: LD (Ladder Diagram), FBD (Function Block Diagram), ST (Structured Text), SFC (Sequential Function Chart), C/C++.
- Read/write PLC parameters for seamless automation logic integration.

### Centralized control of robot systems (Option)
- 
