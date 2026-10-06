---
lang: zh
title: "智能制造"
description: "智能视觉，精准控制，无缝自动化。"
date: 2018-12-20
weight: 3
header_transparent: false
thumbnail: "/assets/images/gen/projects/vlap3d-thumbnail.webp"
image: "/assets/images/gen/projects/vlap3d-large.webp"
client: ""

hero:
  enabled: true
  heading: "智能制造"
  sub_heading: "智能视觉，精准控制，无缝自动化。"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: false
  background_image: "/assets/images/gen/projects/vlap3d-large.webp"
  background_image_blend_mode: false
  fullscreen_mobile: false
  fullscreen_desktop: false
  height: "600px"
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

## VCANUS 智能制造解决方案

**智能视觉，精准控制，无缝自动化。**

VCANUS 集成 TSLoom、VURT-X、VRCAM、Edge AI 和 3D 测量技术，提供 End-to-End（端到端）智能制造解决方案。我们的专业领域涵盖机器视觉、机器人自动化和 AI 驱动的工艺优化，帮助制造企业实现实时监控、预测控制和自主生产。
凭借在卷对卷涂布、显示屏缺陷分类、设备对位、金属 3D 打印和激光材料加工等领域的成熟经验，我们通过智能自动化帮助各行业提升质量、减少浪费并优化效率。

## 为什么选择 VCANUS 智能制造？

**VCANUS 帮助制造企业：**
- 利用机器视觉、Edge AI 和机器人系统实现复杂工艺自动化。
- 通过自适应反馈实时监控和控制质量。
- 借助 AI 驱动的分析和工艺仿真优化生产工作流。
- 与 MES、ERP 和 PLC 系统无缝集成，实现闭环自动化。
- 部署针对特定行业需求定制的可扩展解决方案。

我们的解决方案将前沿技术与深厚的领域经验相结合，为智能工厂提供可落地的洞察和切实的投资回报。

## 核心技术与解决方案

### 1. 基于机器视觉的智能制造
利用 TSLoom 和 Edge AI 将视觉数据转化为可落地的智能：

**卷对卷涂布系统**
- 弯月面形状检测：利用机器视觉检测弯月面形状特征。
- 涂层厚度预测：应用 AI 模型实时预测涂层厚度。
- 工艺优化：动态调整涂布参数，确保均匀性。

侧置相机（轴向视角）实时观测模唇与基材之间的弯月面（涂布液珠）截面，形成从机器视觉形状检测、AI 厚度预测到参数动态调整的闭环，确保膜层均匀。

|<img src="/assets/images/gen/projects/r2r-mon-setup.webp" width="560">|
|---|
| 侧置相机布置：从涂布辊侧面（轴向视角）观测弯月面截面 |

|<img src="/assets/images/gen/projects/r2r-mon-loop.webp" width="560">|
|---|
| 闭环控制：侧置相机 → 弯月面形状检测 → AI 厚度预测 → 参数优化 |

**显示屏缺陷分类**
- 缺陷检测：利用高分辨率相机识别显示面板中的微小缺陷。
- 分类与分析：借助机器学习按类型、尺寸和位置对缺陷进行分类。
- 根本原因分析：将缺陷与工艺参数关联分析，精准定位问题。

**设备对位**
- 边缘与多边形检测：利用模式匹配和几何对位设定设备原点。
- 自动校准：实现微米级的设备设置精度。

**金属 3D 打印系统**
- 熔池监控：利用红外相机采集熔池图像。
- 自适应激光控制：实时调整激光功率，保持熔池尺寸稳定。

### 2. 基于距离位移传感器的制造
利用 1D/2D 位移传感器进行在线检测和 3D 轮廓测量：

**在线零件检测**
- 1D/2D 传感器集成：部署传感器进行实时尺寸检查。
- 缺陷检测：识别表面缺陷、翘曲和尺寸偏差。

**3D 形状测量**
- 2D 传感器 + 执行器系统：将传感器与直线执行器结合，生成复杂零件的 3D 轮廓。
- 自动报告：基于公差限生成合格/不合格报告。

|<img src="/assets/images/gen/projects/2dp1.webp" width="400">|<img src="/assets/images/gen/projects/2dp2.webp" width="500">|
|---|---|
| 实时尺寸检测 | 基于直线执行器的 3D 轮廓测量 |

### 3. 先进机器人应用
借助 VRCAM 和 VURT-X 实现精密材料加工创新：

**激光材料去除系统**
- 3D 扫描与路径规划：使用 VRCAM 获取零件表面并生成最佳刀具路径。
- 自适应材料去除：通过 VURT-X 实时控制机器人搭载的激光器，以微米级精度去除材料。

**基于激光烧结的图案化系统**
- 激光烧结工艺：利用激光烧结形成电子电路线路。
- 缺陷检测：借助机器视觉和 AI 分析检测电路缺陷。

### 4. 飞行（On-The-Fly）激光加工
在工件于输送带上连续移动、无需停止的状态下，利用振镜扫描器进行激光打标和加工。与步进重复（停止—加工—移动）的分度方式相比，可大幅缩短节拍时间。编码器实时检测输送带行程，扫描控制器持续校正打标坐标，使零件在持续移动的同时，以与静止目标相同的精度完成加工。

**2D On-The-Fly**
- 进给同步：通过编码器检测输送带行程，并相应补偿 X·Y 振镜打标坐标。
- 连续产线应用：在输送带打标和切割产线上，以固定焦距对平面工件进行不停机高速加工。

**3D On-The-Fly — VCANUS 技术**
- 3D 路径生成：基于工件 3D 表面数据（高度图 / CAD 模型），生成贴合曲面和台阶面的最佳加工路径。
- 实时动态聚焦控制：同时进行进给校正（X·Y）和表面高度跟踪（Z），利用 z-shifter（动态聚焦模块）使焦点在曲面、台阶面和圆柱面上始终保持在表面。
- 精密同步：对齐编码器、扫描器和工件 3D 坐标系并补偿同步延迟，即使在高进给速度下也能保持加工精度。

|<img src="/assets/images/gen/projects/otf-2d.webp" width="430">|<span style="display:inline-block;width:50px">&nbsp;</span>|<img src="/assets/images/gen/projects/otf-3d.webp" width="430">|
|---|:---:|---|
| **2D On-The-Fly 配置**<br>2 轴振镜扫描头 + 编码器位置反馈（平面对象） | | **3D On-The-Fly 配置**<br>动态 Z 聚焦模块沿曲面跟踪焦点（Δz） |

## VCANUS 解决方案的主要优势

| 解决方案领域 | 主要优势 |
|---|---|
| 机器视觉 | 实时监控、缺陷分类和自适应工艺控制。 |
| 距离位移传感器 | 高速在线检测、3D 轮廓测量和自动化质量控制。 |
| 机器人自动化 | 精密材料加工、VRCAM 路径规划和 VURT-X 实时控制。 |
| 飞行激光加工 | 不停机连续加工、3D 路径生成和表面跟随实时聚焦控制。 |
| Edge AI 与 3D 测量 | 预测分析、统计过程控制和闭环质量管理。 |

## 成功案例
### 卷对卷涂布系统
- 挑战：工艺波动导致涂层厚度不一致，并体现为弯月面形状的变化。
- 解决方案：部署机器视觉 + AI 模型，基于实时弯月面分析预测并调整涂布参数。
- 成果：涂层厚度预测准确率达到 98%

|<img src="/assets/images/gen/projects/r2r1.webp" width="300">|<img src="/assets/images/gen/projects/r2r2.webp" width="300">|<img src="/assets/images/gen/projects/r2r3.webp" width="300">|
|---|---|---|
| 原始图像 | 弯月面形状检测 | 特征提取 |

### 显示屏缺陷分类
- 挑战：提高缺陷分类准确率。
- 解决方案：通过增加分割功能并优化学习网络，提升缺陷检测性能。
- 成果：缺陷检测与分类准确率提升 5%。

|<img src="/assets/images/gen/projects/lcd1.webp" width="300">|<img src="/assets/images/gen/projects/lcd2.webp" width="300">|<img src="/assets/images/gen/projects/lcd3.webp" width="300">|
|---|---|---|
||||

### 金属 3D 打印系统
- 挑战：熔池尺寸不稳定导致零件缺陷。
- 解决方案：采用红外相机监控 + 自适应激光控制。
- 成果：通过实时调整，零件质量提升 20%。

{% include framework/shortcodes/youtube.html id='kHJCm3TZ9vo' %}

### 激光材料去除
- 挑战：人工去除材料质量不稳定且耗时。
- 解决方案：部署机器人搭载的激光扫描器 + VRCAM 路径规划 + VURT-X 实时控制。
- 成果：节拍时间缩短 20%，表面精整质量提升 15%。

## 为什么选择 VCANUS？

✅ 成熟经验：在汽车、航空航天、电子和重工业领域成功部署。
<br>
✅ End-to-End 解决方案：从传感器集成到 AI 分析和机器人自动化。
<br>
✅ 无缝集成：兼容 PLC、MES、ERP 及第三方软件。
<br>
✅ 可扩展、可定制：根据您独特的生产需求量身定制。
<br>
✅ 面向未来：持续融入最新的 AI、视觉和机器人技术。

## 服务行业

| 行业 | 应用 |
|---|---|
| 汽车 | 车身覆盖件检测、涂层厚度控制和机器人材料去除。 |
| 航空航天 |涡轮叶片检测、复合材料加工和精密对位。 |
| 电子 | 显示屏缺陷分类、PCB 检测和电路激光烧结。 |
| 重型机械 | 大型零件 3D 测量、磨损分析和自动化焊接检测。 |
| 金属 3D 打印 | 熔池监控、自适应激光控制和缺陷检测。 |

## 开始使用 VCANUS 智能制造
借助智能化、数据驱动的解决方案，革新您的生产：
- 洽谈针对您需求量身定制的试点项目。
- 预约机器视觉、机器人或 Edge AI 解决方案演示。
- 探索应对您独特制造挑战的定制解决方案。
