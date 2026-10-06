---
lang: zh
title: "机器视觉"
description: "Gidel 基于 FPGA 的机器视觉解决方案 — VCANUS 为韩国官方代理商"
date: 2019-10-03
weight: 2
header_transparent: false
thumbnail: "/assets/images/gen/projects/machine-vision-thumbnail.webp"
image: "/assets/images/gen/projects/machine-vision-large.webp"

hero:
  enabled: true
  heading: "机器视觉解决方案"
  sub_heading: "Gidel 基于 FPGA 的机器视觉解决方案"
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
      - text: "立即购买"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: true
        style: "primary"
---

## Gidel 基于 FPGA 的机器视觉解决方案 — 由 VCANUS 在韩国提供

**Gidel**（以色列）是一家专注于 FPGA 机器视觉 30 余年的全球专业企业。其产品组合覆盖整个视觉流水线 — **PCIe 图像采集卡**、**FPGA + NVIDIA Jetson 一体化边缘计算机**、**相机模拟器**以及**成像 IP 核库**。

**VCANUS 是 Gidel 的韩国官方代理商**，为韩国客户提供产品供应、技术支持和定制集成服务，应用领域涵盖工业视觉、无人机、国防、医疗、体育 AR 和 ATE。

**Gidel 产品线的主要特点**

- **基于 FPGA 的确定性处理** — 硬件级实时性能，无操作系统抖动，零丢帧（Zero Frame Loss）
- **多相机接口** — 单一平台支持 GigE Vision · CoaXPress-12 · Camera Link
- **FPGA 实时压缩** — JPEG · Lossless · Quality+ · HDR IP 核
- **多相机同步（InfiniVision）** — 100 台以上相机间的纳秒级同步
- **AI 边缘计算集成** — FPGA + NVIDIA Jetson 组合边缘计算机
- **开发工具与定制** — ProcVision Suite · GIL · CamSim · SkyBoost SDK

---

## 图像采集卡 — HawkEye 系列

**插入 PCIe 插槽的图像采集卡。** 单卡统一支持多种工业相机接口，板载 FPGA 可完成压缩、HDR 和去马赛克等图像处理。

**主要功能**
- **多接口产品线** — GigE Vision · CoaXPress-12 · Camera Link 型号
- **零丢帧 · 零 CPU 占用** — 硬件 DMA 直接传输
- **FPGA 板载处理** — 实时图像处理、压缩、HDR
- **PoCXP / PoCL** — 电源与数据共用一根线缆，简化布线
- **兼容 InfiniVision** — 多相机同步扩展

### GigE Vision 型号

单卡多通道同时接入工业 GigE Vision 相机。

<img src="/assets/images/gen/projects/gidel-hawkeye-gige.png" alt="HawkEye GigE Vision 图像采集卡" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### CoaXPress 型号

通过 CoaXPress-12 实现高带宽工业相机连接。

<img src="/assets/images/gen/projects/gidel-hawkeye-cxp.png" alt="HawkEye CoaXPress 图像采集卡" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### Camera Link 型号

支持 Camera Link Deca / Full / Medium / Base 接口。

<img src="/assets/images/gen/projects/gidel-hawkeye-cl.png" alt="HawkEye Camera Link 图像采集卡" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## FantoVision — IoT 边缘计算机（FPGA + Jetson）

**一款将基于 FPGA 的图像采集与 NVIDIA Jetson AI 推理集成于单一紧凑设备的边缘计算机。** 图像采集、压缩、预处理和 AI 推理均可在现场完成，无需服务器，非常适合对 SWaP（尺寸、重量、功耗）有严格要求的**无人机、工业机器人、医疗设备和嵌入式视觉系统**。

**主要功能**
- **FPGA + NVIDIA Jetson** 一体化边缘计算机（可选 Xavier NX · Orin NX）
- **紧凑外形** — 约 13.4 × 9 × 6 cm，约 750 g
- **FPGA 板载处理** — 压缩、HDR、图像增强
- **基于 CUDA 的 AI 推理** — 采集与推理同时进行
- **加固选项** — I 选项（宽温范围）、R 选项（防振 / 防尘 / 防潮）
- 适用于户外、国防和航空航天部署

### FantoVision 20 系列

基于 GigE Vision · Camera Link 接口的紧凑型边缘计算机。

<img src="/assets/images/gen/projects/gidel-fantovision20.png" alt="FantoVision 20 系列" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### FantoVision 40 系列

配备 CoaXPress-12 接口并可选 10GigE 的高性能边缘计算机。

<img src="/assets/images/gen/projects/gidel-fantovision40.png" alt="FantoVision 40 系列" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## 相机模拟器 — CamSim

**一款基于 PCIe 的相机模拟器，无需实体相机即可验证整个图像采集卡与视觉流水线。** 借助确定性测试，可进行算法开发并实现可复现的多相机流水线验证。

**型号阵容**
- **CamSim-CL** — Camera Link（支持 Deca / Full / Medium / Base）
- **CamSim-X** — 多通道 CoaXPress

**应用场景**
- 算法开发与验证
- 多相机流水线复现
- 用于问题根因隔离的确定性测试
- 硬件到位前的开发与测试

<img src="/assets/images/gen/projects/gidel-camsim.png" alt="CamSim 相机模拟器" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

<img src="/assets/images/gen/projects/gidel-camsim-diagram.png" alt="CamSim 系统框图" style="display:block; width:100%; max-width:560px; height:auto; margin:1rem auto;">

---

## 成像库 — GIL 与开发工具

**专为 Gidel 硬件打造的统一开发工具链。** 复用经过验证的 IP 核以确保可靠性，即使不具备深厚的 FPGA 经验也能构建定制视觉算法。

**GIL（Gidel Imaging Library）**
- 基于 30 年 FPGA 开发经验的视觉与成像 IP 核库
- **CPU 卸载** — 由 FPGA 承担繁重计算，释放系统资源
- **丰富的 IP 核** — 系统（Multiport · MultiFIFO）、相机接口、图像处理（去马赛克 · 直方图 · 形态学）、调试
- **压缩 IP 核** — JPEG · Lossless · Quality+
- **FPGA 虚拟化** — 多个应用同时共享 FPGA
- **支持 GenICam 标准**

**ProcVision Suite**
- 基于 C/C++ 的定制 FPGA IP 核开发与编译
- 非 FPGA 专家也可实现算法 → 加快开发
- 快速实现 OEM/ODM 定制

**SkyBoost SDK**
- 高速 RAW → JPEG API
- 硬件加速，速度优于软件实现

---

## 应用领域

Gidel 产品广泛部署于对确定性实时性能和多相机同步要求严格的行业。

<img src="/assets/images/gen/projects/machine-vision-applications.svg" alt="Gidel 应用领域 — 8 大行业" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

---

## VCANUS 集成解决方案

VCANUS 不仅代理 Gidel 产品，还将其与自有的**数据平台（TSLoom）**和 **AI 视觉平台（DeepVi）**相结合，提供 **End-to-End 工业视觉解决方案**。

<img src="/assets/images/gen/projects/machine-vision-solutions.svg" alt="VCANUS + Gidel 集成解决方案场景" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">
