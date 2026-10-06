---
lang: zh
title: "RoboScan250"
description: "基于移动机器人的 3D 形貌与变形测量自动化系统"
date: 2025-06-10
weight: 5
header_transparent: false
fa_icon: false
icon: "assets/images/icons/deepvi-icon.svg"
thumbnail: "/assets/images/gen/services/roboscan250-thumb.webp"
image: "/assets/images/gen/services/roboscan250-hero.webp"

hero:
  enabled: true
  heading: "RoboScan250"
  sub_heading: "3D 形貌与变形测量自动化<br> — 由移动机器人与数字测量传感器驱动"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: true
  background_image_blend_mode: false # "overlay", "multiply", "screen"
  background_image: "/assets/images/gen/services/roboscan250-hero.webp"
  fullscreen_mobile: false
  fullscreen_desktop: false
  height: 660px
  buttons:
    enabled: false
    list:
      - text: "立即购买"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: false
        style: "primary"
---

## 基于移动机器人的 3D 形貌与变形测量自动化系统

**RoboScan250** 将**自主移动机器人（AMR）**、**六轴关节机器人**和**德国 ZEISS ARAMIS 数字测量传感器**集成于同一平台，实现**3D 形貌与变形测量自动化**。机器人自主移动至测量对象，关节机器人调整测量姿态，自动完成高精度 3D 位移、运动和应变测量。测量序列可预先在**数字孪生虚拟环境**中验证，并通过**基于 Web 的集成监控与控制**实时管理机器人和测量设备的状态。

---

## 主要功能

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 高精度 3D 形貌测量
- **ZEISS ARAMIS** 测量系统（德国）
- 分辨率 **4096 x 3000 pixel**
- 帧率 **25 Hz ~ 100 Hz**
- 测量范围 **20 x 15 ~ 1800 x 1500 mm²**
- **3D 位移与运动**测量
- **应变**测量
- **LED 照明**

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 测量路径生成与序列管理

<ul>
<li><strong>机器人测量位置与姿态调整</strong>
<ul style="list-style:circle;">
<li>协作机器人直接示教</li>
<li>示教器</li>
<li>虚拟环境</li>
</ul>
</li>
<li><strong>测量序列创建与管理</strong>
<ul style="list-style:circle;">
<li>创建机器人移动与测量任务</li>
<li>各任务的详细设置</li>
<li>任务的添加、移动和删除</li>
<li>保存、加载等序列管理</li>
</ul>
</li>
</ul>

</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 数字孪生与虚拟环境要素管理

<ul>
<li><strong>在虚拟环境中验证序列</strong>
<ul style="list-style:circle;">
<li>确认机器人位置与姿态</li>
<li>确认测量区域</li>
</ul>
</li>
<li><strong>虚拟环境要素管理</strong>
<ul style="list-style:circle;">
<li>导入测量对象 CAD 数据并在画面中注册</li>
<li>机器人数据管理</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 实时监控与集成控制

<ul>
<li><strong>基于 Web 的设备状态集成监控</strong>
<ul style="list-style:circle;">
<li>实时监控机器人与测量设备状态</li>
</ul>
</li>
<li><strong>序列执行状态监控</strong>
<ul style="list-style:circle;">
<li>管理移动、姿态与测量任务</li>
<li>显示任务列表与执行状态</li>
<li>通过日志消息进行原因分析</li>
</ul>
</li>
<li><strong>基于 Web 的机器人控制</strong></li>
<li><strong>AMR 位置与路径规划 → 自主行驶</strong></li>
</ul>

</div>
</div>

---

## 系统配置

### 移动机器人（AMR）
- **尺寸**：870 x 600 x 265 mm
- **速度**：1.5 m/s（最大）
- **重量**：130 kg
- **负载**：250 kg
- **精度**：全局 ±30 mm / 对接 ±5 mm
- **电池**：48V 输出 x 1，24V 输出 x 1（满载运行 8 小时，充电 90 分钟）
- **充电站**：输入 AC 90~264 V，最大功耗 2200 W
- 含手动充电装置

### 六轴关节机器人

可根据客户需求，从以下两款六轴协作机器人中选择其一。

**Type A**
- **轴数**：6 轴 / **负载**：9 kg / **臂展**：1,200 mm / **重复精度**：±0.05 mm
- **内置 DC 控制器**：无需 DC 转换器
- **PDB 板**：电路保护，电源输入 24~48V，最高 80A
- **附件**：通用适配器、AMR 安装框架及外罩

**Type B**
- **轴数**：6 轴 / **负载**：7 kg / **臂展**：1,210 mm / **重复精度**：±0.1 mm
- **DC-AC 逆变器**：将 AMR 直流电源转换为机器人交流电源，输入 48V DC / 输出 220V AC，额定 3kW
- **PDB 板**：电路保护，电源输入 24~48V，最高 80A
- **附件**：通用适配器、AMR 安装框架及外罩

### 数字测量传感器（ZEISS ARAMIS）
- **制造商**：ZEISS
- **相机分辨率**：4096 x 3000 pixel（25 Hz，全幅）~ 像素合并时最高 100 Hz
- **帧率**：25 Hz ~ 100 Hz
- **应变测量范围**：0.02% ~ 100% 以上
- **测量范围**：20 x 15 ~ 1800 x 1500 mm² / **重量**：1.0 kg / **照明**：LED
- **处理计算机**：Intel Core i9-13950HX，RAM 64GB DDR5，NVIDIA RTX 3500 Ada 12GB，17" 显示屏，1TB SSD，Windows 11
- 含 3m USB 线缆及一枚定焦微距镜头

**ARAMIS 应用案例 — 拉伸试样的全场应变测量**

<img src="/assets/images/gen/services/roboscan-aramis-usage.webp" alt="ARAMIS 应用案例 — 拉伸试样的全场应变测量及应变集中区域可视化" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

ARAMIS 以像素为单位计算表面位移和应变，并以彩色云图直观呈现应变集中区域。在静态和动态加载试验中，可对开裂、颈缩及局部变形行为进行定量分析。

### 集成运行计算机
- **CPU**：Ultra7-265（20 核 / 20 线程）/ **内存**：32GB DDR5 / **存储**：1TB SSD
- **电源**：80+ 700W ATX
- **操作系统**：Linux（ARAMIS 处理计算机运行 Windows）
- **显示器**：27"，1920 x 1080，HDMI / 含键盘·鼠标

---

## 测量产品线扩展

除标准 **ZEISS ARAMIS** 配置外，RoboScan250 的数字测量传感器还可根据测量目的和对象，在 **ARAMIS 3D 系列**与 **ATOS 5 系列**之间选择扩展。ARAMIS 3D 用于动态变形与运动测量，ATOS 5 用于精密 3D 形貌扫描，可按现场需求灵活配置测量产品组合。

### ARAMIS 3D 系列 — 3D 变形与动态行为测量

一种光学测量系统，可对测量对象的位移、应变、振动等**动态行为进行全场测量**。可根据测量范围和帧率选择型号。

<img src="/assets/images/gen/services/roboscan-aramis3d.webp" alt="ARAMIS 3D 系列 — ARAMIS 3D Camera 12M 与 ARAMIS SRX 规格对比" style="display:block; width:100%; height:auto; max-width:1000px; margin:1.5rem auto;">

- **ARAMIS 3D Camera 12M**：4096 x 3000 pixel，最高 150 fps，测量范围 35 x 25 mm ~ 5000 x 4000 mm
- **ARAMIS SRX**：4096 x 3068 pixel，利用相机内置 RAM（8GB）实现最高约 2000 fps 的高速测量，测量范围 70 x 50 mm ~ 5100 x 4200 mm

### ATOS 5 系列 — 高精度 3D 形貌扫描

一种结构光系统，可将**测量对象的表面形貌扫描为高密度 3D 数据**。可根据测量范围和细节要求选择型号。

<img src="/assets/images/gen/services/roboscan-atos5.webp" alt="ATOS 5 系列 — ZEISS ATOS LRX、ATOS 5 for Airfoil、ATOS 5、ATOS 5X 规格对比" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

- **ZEISS ATOS LRX**：超大范围 3D 扫描（LASER），工作距离 1810 mm
- **ATOS 5 for Airfoil**：精细细节的精密扫描（LED），工作距离 530 mm
- **ATOS 5**：高速 3D 扫描系统（LED），工作距离 880 mm
- **ATOS 5X**：大范围自动化扫描（LASER），工作距离 880 mm

---

## 集成运行软件

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 机器人控制

<ul>
<li><strong>移动机器人控制</strong>
<ul style="list-style:circle;">
<li>地图生成</li>
<li>路径生成</li>
<li>自主移动</li>
</ul>
</li>
<li><strong>关节机器人控制</strong>
<ul style="list-style:circle;">
<li>运动与姿态控制（单轴 / 末端点）</li>
<li>示教控制（基于示教器 / 直接示教）</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 集成控制与测量

<ul>
<li><strong>基于 Web 的实时监控与显示</strong>
<ul style="list-style:circle;">
<li>机器人位置与姿态</li>
<li>设备与序列状态</li>
</ul>
</li>
<li><strong>任务与序列控制</strong>
<ul style="list-style:circle;">
<li>创建 / 保存 / 加载</li>
<li>开始 / 停止 / 取消</li>
<li>参数设置</li>
<li>添加 / 移动 / 删除</li>
</ul>
</li>
<li><strong>测量</strong>
<ul style="list-style:circle;">
<li>3D 位移、运动和应变</li>
<li>全场表面分析与基于点的动态分析</li>
<li>ZEISS CORRELATE / Inspect 集成</li>
<li>测量数据采集与项目管理</li>
<li>外部测量信号同步</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 虚拟环境

<ul>
<li><strong>虚拟环境配置</strong>
<ul style="list-style:circle;">
<li>机器人配置</li>
<li>导入并加载测量对象 CAD（glTF）</li>
<li>显示机器人与测量对象</li>
</ul>
</li>
<li><strong>测量设备与区域配置</strong>
<ul style="list-style:circle;">
<li>测量设备配置</li>
<li>视锥（Frustum）区域配置</li>
<li>测量区域显示</li>
</ul>
</li>
<li><strong>虚拟仿真</strong>
<ul style="list-style:circle;">
<li>设置并移动机器人位置</li>
<li>更改姿态（单轴 / IK / Gizmo）</li>
<li>视图缩放与平移</li>
</ul>
</li>
<li><strong>序列验证</strong>
<ul style="list-style:circle;">
<li>添加移动、姿态与测量任务</li>
<li>仿真并验证任务序列</li>
</ul>
</li>
</ul>

</div>
</div>

---

## 一句话了解 RoboScan250

> **机器人自主移动、自主测量 — 全自动 3D 形貌与变形测量。**

RoboScan250 集成自主移动机器人、六轴关节机器人和 ZEISS ARAMIS 数字测量传感器，实现**移动 → 姿态控制 → 高精度 3D 测量**全过程自动化。测量序列可预先在数字孪生虚拟环境中验证，并通过基于 Web 的集成控制实时操作机器人和测量设备，确保测量的准确性与重复性。
