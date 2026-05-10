---
title: "Machine Vision"
description: "FPGA-based machine vision solutions from Gidel — VCANUS Official Korean distributor"
date: 2019-10-03
weight: 2
header_transparent: false
thumbnail: "/assets/images/gen/projects/machine-vision-thumbnail.webp"
image: "/assets/images/gen/projects/machine-vision-large.webp"

hero:
  enabled: true
  heading: "Machine Vision Solutions"
  sub_heading: "FPGA-based machine vision solutions from Gidel"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: false
  background_image: "/assets/images/gen/projects/machine-vision-large.webp"
  background_image_blend_mode: false
  fullscreen_mobile: false
  fullscreen_desktop: false
  height: "660px"
  buttons:
    enabled: false
    list:
      - text: "Buy Now"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: true
        style: "primary"
---

## FPGA-Based Machine Vision Solutions from Gidel — Delivered in Korea by VCANUS

**Gidel** (Israel) is a global specialist with over 30 years of focus on FPGA-based machine vision. Their portfolio spans the entire vision pipeline — **PCIe frame grabbers**, **FPGA + NVIDIA Jetson integrated edge computers**, **camera simulators**, and **imaging IP core libraries**.

**VCANUS is the official Korean distributor of Gidel**, providing product supply, technical support, and custom integration services to Korean customers across industrial vision, UAV, defense, medical, sports AR, and ATE applications.

**Key Characteristics of the Gidel Product Line**

- **FPGA-based deterministic processing** — Hardware-level real-time performance, no OS jitter, Zero Frame Loss
- **Multi-camera interfaces** — GigE Vision · CoaXPress-12 · Camera Link supported on a single platform
- **Real-time FPGA compression** — JPEG · Lossless · Quality+ · HDR IP cores
- **Multi-camera synchronization (InfiniVision)** — Nanosecond-level synchronization across 100+ cameras
- **AI edge computing integration** — FPGA + NVIDIA Jetson combined edge computer
- **Development tools & customization** — ProcVision Suite · GIL · CamSim · SkyBoost SDK

---

## Frame Grabber — HawkEye Series

**PCIe slot-mounted frame grabbers.** Industrial camera interfaces unified on a single card, with FPGA on-board image processing including compression, HDR, and debayering.

**Key Features**
- **Multi-interface lineup** — GigE Vision · CoaXPress-12 · Camera Link models
- **Zero Frame Loss · Zero CPU usage** — direct hardware DMA transfer
- **FPGA on-board processing** — real-time image processing, compression, HDR
- **PoCXP / PoCL** — power and data on the same cable, simplifying wiring
- **InfiniVision compatible** — multi-camera synchronization extension

### GigE Vision Models

Multi-channel concurrent ingestion of industrial GigE Vision cameras on a single card.

<img src="/assets/images/gen/projects/gidel-hawkeye-gige.png" alt="HawkEye GigE Vision Frame Grabber" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### CoaXPress Models

High-bandwidth industrial camera connectivity with CoaXPress-12.

<img src="/assets/images/gen/projects/gidel-hawkeye-cxp.png" alt="HawkEye CoaXPress Frame Grabber" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### Camera Link Models

Camera Link Deca / Full / Medium / Base interface support.

<img src="/assets/images/gen/projects/gidel-hawkeye-cl.png" alt="HawkEye Camera Link Frame Grabber" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## FantoVision — IoT Edge Computer (FPGA + Jetson)

**An edge computer that integrates FPGA-based image acquisition and NVIDIA Jetson AI inference into a single compact device.** Image acquisition, compression, preprocessing, and AI inference complete on-site without a server — making it ideal for **UAV / drones, industrial robotics, medical devices, and embedded vision systems** where SWaP (size, weight, power) constraints matter.

**Key Features**
- **FPGA + NVIDIA Jetson** integrated edge computer (Xavier NX · Orin NX options)
- **Compact form factor** — approx. 13.4 × 9 × 6 cm, ~750 g
- **FPGA on-board processing** — compression, HDR, image enhancement
- **CUDA-based AI inference** — concurrent acquisition and inference
- **Ruggedized options** — I option (extended temperature range), R option (vibration / dust / humidity protection)
- Suitable for outdoor, defense, and aerospace deployments

### FantoVision 20 Series

Compact edge computer based on GigE Vision · Camera Link interfaces.

<img src="/assets/images/gen/projects/gidel-fantovision20.png" alt="FantoVision 20 Series" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### FantoVision 40 Series

High-performance edge computer with CoaXPress-12 interfaces and 10GigE option.

<img src="/assets/images/gen/projects/gidel-fantovision40.png" alt="FantoVision 40 Series" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## Camera Simulator — CamSim

**A PCIe-based camera simulator that lets you verify the entire frame grabber and vision pipeline without a physical camera.** Deterministic testing enables algorithm development and reproducible multi-camera pipeline validation.

**Model Lineup**
- **CamSim-CL** — Camera Link (Deca / Full / Medium / Base support)
- **CamSim-X** — Multi-channel CoaXPress

**Use Cases**
- Algorithm development and verification
- Multi-camera pipeline reproduction
- Deterministic testing for root-cause isolation
- Pre-hardware development and testing

<img src="/assets/images/gen/projects/gidel-camsim.png" alt="CamSim Camera Simulator" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

<img src="/assets/images/gen/projects/gidel-camsim-diagram.png" alt="CamSim System Diagram" style="display:block; width:100%; max-width:560px; height:auto; margin:1rem auto;">

---

## Imaging Library — GIL & Development Tools

**A unified development toolchain tailored to Gidel hardware.** Reuse verified IP cores for reliability, and build custom vision algorithms even without deep FPGA expertise.

**GIL (Gidel Imaging Library)**
- Vision and imaging IP core library built on 30 years of FPGA development experience
- **CPU offloading** — FPGA handles heavy computation, freeing system resources
- **Diverse IP cores** — system (Multiport · MultiFIFO), camera I/F, image processing (debayer · histogram · morphology), debug
- **Compression IP cores** — JPEG · Lossless · Quality+
- **FPGA virtualization** — multiple applications share the FPGA concurrently
- **GenICam standard support**

**ProcVision Suite**
- C/C++ based custom FPGA IP core development and compilation
- Algorithm implementation accessible to non-FPGA experts → faster development
- Rapid OEM/ODM customization

**SkyBoost SDK**
- High-speed RAW → JPEG API
- Hardware-accelerated, faster than software equivalents

---

## Application Areas

Gidel products are deployed across industries where deterministic real-time performance and multi-camera synchronization are critical.

<img src="/assets/images/gen/projects/machine-vision-applications.svg" alt="Gidel application areas — 8 industries" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

---

## Integrated Solutions with VCANUS

Beyond simply distributing Gidel products, VCANUS combines them with our own **data platform (TSLoom)** and **AI vision platform (DeepVi)** to deliver **end-to-end industrial vision solutions**.

<img src="/assets/images/gen/projects/machine-vision-solutions.svg" alt="VCANUS + Gidel integrated solution scenarios" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">
