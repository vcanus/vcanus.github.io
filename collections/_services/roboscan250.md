---
title: "RoboScan250"
description: "Mobile robot-based 3D shape & deformation measurement automation system"
date: 2025-06-10
weight: 5
header_transparent: false
fa_icon: false
icon: "assets/images/icons/deepvi-icon.svg"
thumbnail: "/assets/images/gen/services/service-11-thumbnail.webp"
image: "/assets/images/gen/services/service-11.webp"

hero:
  enabled: true
  heading: "RoboScan250"
  sub_heading: "3D shape & deformation measurement automation<br> — powered by a mobile robot and a digital measurement sensor"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: true
  background_image_blend_mode: false # "overlay", "multiply", "screen"
  background_image: "/assets/images/gen/services/service-11.webp"
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

## Mobile Robot-Based 3D Shape & Deformation Measurement Automation System

**RoboScan250** integrates an **autonomous mobile robot (AMR)**, a **6-axis articulated robot**, and the **ZEISS ARAMIS digital measurement sensor (Germany)** into a single platform for **automated 3D shape and deformation measurement**. The robot autonomously travels to the measurement target, the articulated robot positions the measurement pose, and high-precision 3D displacement, motion, and strain are measured automatically. Measurement sequences are validated in advance within a **digital-twin virtual environment**, while **web-based integrated monitoring and control** manages the status of robots and measurement devices in real time.

---

## Key Features

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### High-Precision 3D Shape Measurement
- **ZEISS ARAMIS** measurement system (Germany)
- Resolution **4096 x 3000 pixel**
- Frame Rate **25 Hz ~ 100 Hz**
- Measurement area **20 x 15 ~ 1800 x 1500 mm²**
- **3D displacement and motion** measurement
- **Strain** measurement
- **LED Illumination**

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Measurement Path Generation & Sequence Management

<ul>
<li><strong>Robot measurement position & pose adjustment</strong>
<ul style="list-style:circle;">
<li>Direct teaching of the cobot</li>
<li>Teaching pendant</li>
<li>Virtual environment</li>
</ul>
</li>
<li><strong>Measurement sequence creation & management</strong>
<ul style="list-style:circle;">
<li>Task creation for robot movement and measurement</li>
<li>Detailed settings per task</li>
<li>Add, move, and delete tasks</li>
<li>Sequence management such as save and load</li>
</ul>
</li>
</ul>

</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Digital Twin & Virtual Environment Element Management

<ul>
<li><strong>Sequence validation in the virtual environment</strong>
<ul style="list-style:circle;">
<li>Verify robot position and pose</li>
<li>Verify measurement area</li>
</ul>
</li>
<li><strong>Virtual environment element management</strong>
<ul style="list-style:circle;">
<li>Import target CAD data and register on screen</li>
<li>Robot data management</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Real-Time Monitoring & Integrated Control

<ul>
<li><strong>Web-based integrated equipment status monitoring</strong>
<ul style="list-style:circle;">
<li>Real-time monitoring of robot and measurement device status</li>
</ul>
</li>
<li><strong>Sequence execution status monitoring</strong>
<ul style="list-style:circle;">
<li>Management of movement, pose, and measurement tasks</li>
<li>Task list and execution status display</li>
<li>Root-cause analysis via log messages</li>
</ul>
</li>
<li><strong>Web-based robot control</strong></li>
<li><strong>AMR position & path planning → autonomous driving</strong></li>
</ul>

</div>
</div>

---

## System Configuration

### Mobile Robot (AMR)
- **Dimension**: 870 x 600 x 265 mm
- **Speed**: 1.5 m/s (Max)
- **Weight**: 130 kg
- **Payload**: 250 kg
- **Accuracy**: Global ±30 mm / Docking ±5 mm
- **Battery**: 48V output x 1, 24V output x 1 (8 hr full-load runtime, 90 min charging)
- **Charging station**: Input AC 90~264 V, max power consumption 2200 W
- Manual charging unit included

### 6-Axis Articulated Robot

One of the following two 6-axis cobot models can be selected according to customer requirements.

**Type A**
- **Axis**: 6-axis / **Payload**: 9 kg / **Reach**: 1,200 mm / **Repeatability**: ±0.05 mm
- **DC controller included**: no DC converter required
- **PDB board**: circuit protection, power input 24~48V, up to 80A
- **Accessories**: universal adapter, AMR mounting frame and cover

**Type B**
- **Axis**: 6-axis / **Payload**: 7 kg / **Reach**: 1,210 mm / **Repeatability**: ±0.1 mm
- **DC-AC inverter**: AMR DC power → robot AC power conversion, input 48V DC / output 220V AC, rated 3kW
- **PDB board**: circuit protection, power input 24~48V, up to 80A
- **Accessories**: universal adapter, AMR mounting frame and cover

### Digital Measurement Sensor (ZEISS ARAMIS)
- **Manufacturer**: ZEISS
- **Camera resolution**: 4096 x 3000 pixel (25 Hz, full) ~ up to 100 Hz with binning
- **Frame Rate**: 25 Hz ~ 100 Hz
- **Strain measurement range**: 0.02% ~ over 100%
- **Measurement area**: 20 x 15 ~ 1800 x 1500 mm² / **Weight**: 1.0 kg / **Illumination**: LED
- **Processing computer**: Intel Core i9-13950HX, RAM 64GB DDR5, NVIDIA RTX 3500 Ada 12GB, 17" display, 1TB SSD, Windows 11
- USB 3m cable, one single macro lens included

**ARAMIS Use Case — Full-field strain measurement of a tensile specimen**

<img src="/assets/images/gen/services/roboscan-aramis-usage.webp" alt="ARAMIS use case — full-field strain measurement of a tensile specimen and visualization of strain concentration" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

ARAMIS computes surface displacement and strain on a per-pixel basis and visualizes strain-concentration areas as color maps. Under static and dynamic loading tests, it quantitatively analyzes cracking, necking, and localized deformation behavior.

### Integrated Operation Computer
- **CPU**: Ultra7-265 (20 Core / 20 Threads) / **Memory**: 32GB DDR5 / **Storage**: 1TB SSD
- **Power**: 80+ 700W ATX
- **OS**: Linux (the ARAMIS processing computer runs Windows)
- **Monitor**: 27", 1920 x 1080, HDMI / Keyboard·Mouse included

---

## Measurement Product Lineup Expansion

Beyond the standard **ZEISS ARAMIS** configuration, the RoboScan250's digital measurement sensor can be expanded by selecting between the **ARAMIS 3D series** and the **ATOS 5 series** according to the measurement purpose and target. ARAMIS 3D is applied for dynamic deformation and motion measurement, while ATOS 5 is applied for precise 3D shape scanning — configuring the measurement lineup to match field requirements.

### ARAMIS 3D Series — 3D Deformation & Dynamic Behavior Measurement

An optical measurement system that performs **full-field measurement of dynamic behavior** such as displacement, strain, and vibration of a target. The model can be selected according to measurement volume and frame rate.

<img src="/assets/images/gen/services/roboscan-aramis3d.webp" alt="ARAMIS 3D series — spec comparison of ARAMIS 3D Camera 12M and ARAMIS SRX" style="display:block; width:100%; height:auto; max-width:1000px; margin:1.5rem auto;">

- **ARAMIS 3D Camera 12M**: 4096 x 3000 pixel, up to 150 fps, measurement volume 35 x 25 mm ~ 5000 x 4000 mm
- **ARAMIS SRX**: 4096 x 3068 pixel, high-speed measurement up to ~2000 fps using camera-internal RAM (8GB), measurement volume 70 x 50 mm ~ 5100 x 4200 mm

### ATOS 5 Series — High-Precision 3D Shape Scanning

A structured-light system that **scans the surface shape of a target into high-density 3D data**. The model can be selected according to measurement volume and detail requirements.

<img src="/assets/images/gen/services/roboscan-atos5.webp" alt="ATOS 5 series — spec comparison of ZEISS ATOS LRX, ATOS 5 for Airfoil, ATOS 5, ATOS 5X" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

- **ZEISS ATOS LRX**: 3D scanning of very large volumes (LASER), working distance 1810 mm
- **ATOS 5 for Airfoil**: precise scanning of fine details (LED), working distance 530 mm
- **ATOS 5**: high-speed 3D scanning system (LED), working distance 880 mm
- **ATOS 5X**: automated scanning of large volumes (LASER), working distance 880 mm

---

## Integrated Operation Software

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Robot Control

<ul>
<li><strong>Mobile robot control</strong>
<ul style="list-style:circle;">
<li>Map generation</li>
<li>Path generation</li>
<li>Autonomous movement</li>
</ul>
</li>
<li><strong>Articulated robot control</strong>
<ul style="list-style:circle;">
<li>Motion & pose control (per-axis / end point)</li>
<li>Teaching control (pendant-based / direct teaching)</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Integrated Control & Measurement

<ul>
<li><strong>Web-based real-time monitoring & display</strong>
<ul style="list-style:circle;">
<li>Robot position & pose</li>
<li>Equipment & sequence status</li>
</ul>
</li>
<li><strong>Task & sequence control</strong>
<ul style="list-style:circle;">
<li>Create / save / load</li>
<li>Start / stop / cancel</li>
<li>Parameter settings</li>
<li>Add / move / delete</li>
</ul>
</li>
<li><strong>Measurement</strong>
<ul style="list-style:circle;">
<li>3D displacement, motion, and strain</li>
<li>Full-field surface analysis and point-based dynamic analysis</li>
<li>ZEISS CORRELATE / Inspect integration</li>
<li>Measurement data acquisition & project management</li>
<li>External measurement signal synchronization</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Virtual Environment

<ul>
<li><strong>Virtual environment setup</strong>
<ul style="list-style:circle;">
<li>Robot configuration</li>
<li>Import & load target CAD (glTF)</li>
<li>Display robot & target</li>
</ul>
</li>
<li><strong>Measurement device & area setup</strong>
<ul style="list-style:circle;">
<li>Measurement device configuration</li>
<li>Frustum area configuration</li>
<li>Measurement area display</li>
</ul>
</li>
<li><strong>Virtual simulation</strong>
<ul style="list-style:circle;">
<li>Set & move robot position</li>
<li>Change pose (per-axis / IK / Gizmo)</li>
<li>Zoom in/out & pan the view</li>
</ul>
</li>
<li><strong>Sequence validation</strong>
<ul style="list-style:circle;">
<li>Add movement, pose, and measurement tasks</li>
<li>Simulate and validate the task sequence</li>
</ul>
</li>
</ul>

</div>
</div>

---

## RoboScan250 in One Line

> **The robot moves and measures on its own — fully automated 3D shape & deformation measurement.**

RoboScan250 integrates an autonomous mobile robot, a 6-axis articulated robot, and the ZEISS ARAMIS digital measurement sensor to automate the entire process of **movement → pose control → high-precision 3D measurement**. It validates measurement sequences in advance within a digital-twin virtual environment and operates robots and measurement devices in real time through web-based integrated control, ensuring measurement accuracy and repeatability.
