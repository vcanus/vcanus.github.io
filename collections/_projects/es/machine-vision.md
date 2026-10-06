---
lang: es
title: "Visión artificial"
description: "Soluciones de visión artificial basadas en FPGA de Gidel — VCANUS, distribuidor oficial en Corea"
date: 2019-10-03
weight: 2
header_transparent: false
thumbnail: "/assets/images/gen/projects/machine-vision-thumbnail.webp"
image: "/assets/images/gen/projects/machine-vision-large.webp"

hero:
  enabled: true
  heading: "Soluciones de visión artificial"
  sub_heading: "Soluciones de visión artificial basadas en FPGA de Gidel"
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
      - text: "Comprar ahora"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: true
        style: "primary"
---

## Soluciones de visión artificial basadas en FPGA de Gidel — Suministradas en Corea por VCANUS

**Gidel** (Israel) es un especialista global con más de 30 años dedicados a la visión artificial basada en FPGA. Su portafolio abarca todo el pipeline de visión: **frame grabbers PCIe**, **computadoras Edge integradas FPGA + NVIDIA Jetson**, **simuladores de cámara** y **bibliotecas de IP cores de procesamiento de imágenes**.

**VCANUS es el distribuidor oficial de Gidel en Corea** y ofrece suministro de productos, soporte técnico y servicios de integración a la medida a clientes coreanos en aplicaciones de visión industrial, UAV, defensa, medicina, AR deportiva y ATE.

**Características clave de la línea de productos Gidel**

- **Procesamiento determinista basado en FPGA** — Desempeño en tiempo real a nivel de hardware, sin jitter del sistema operativo, Zero Frame Loss
- **Interfaces multicámara** — GigE Vision · CoaXPress-12 · Camera Link compatibles en una sola plataforma
- **Compresión en tiempo real en FPGA** — IP cores JPEG · Lossless · Quality+ · HDR
- **Sincronización multicámara (InfiniVision)** — Sincronización a nivel de nanosegundos en más de 100 cámaras
- **Integración de computación Edge con IA** — Computadora Edge que combina FPGA + NVIDIA Jetson
- **Herramientas de desarrollo y personalización** — ProcVision Suite · GIL · CamSim · SkyBoost SDK

---

## Frame grabber — Serie HawkEye

**Frame grabbers para ranura PCIe.** Interfaces de cámaras industriales unificadas en una sola tarjeta, con procesamiento de imágenes integrado en la FPGA que incluye compresión, HDR y debayering.

**Funciones principales**
- **Línea con múltiples interfaces** — Modelos GigE Vision · CoaXPress-12 · Camera Link
- **Zero Frame Loss · Zero CPU usage** — transferencia DMA directa por hardware
- **Procesamiento integrado en la FPGA** — procesamiento de imágenes en tiempo real, compresión, HDR
- **PoCXP / PoCL** — alimentación y datos por el mismo cable, lo que simplifica el cableado
- **Compatible con InfiniVision** — extensión para sincronización multicámara

### Modelos GigE Vision

Adquisición simultánea multicanal de cámaras industriales GigE Vision en una sola tarjeta.

<img src="/assets/images/gen/projects/gidel-hawkeye-gige.png" alt="Frame grabber HawkEye GigE Vision" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### Modelos CoaXPress

Conectividad de alto ancho de banda para cámaras industriales con CoaXPress-12.

<img src="/assets/images/gen/projects/gidel-hawkeye-cxp.png" alt="Frame grabber HawkEye CoaXPress" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### Modelos Camera Link

Compatibilidad con las interfaces Camera Link Deca / Full / Medium / Base.

<img src="/assets/images/gen/projects/gidel-hawkeye-cl.png" alt="Frame grabber HawkEye Camera Link" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## FantoVision — Computadora Edge IoT (FPGA + Jetson)

**Una computadora Edge que integra la adquisición de imágenes basada en FPGA y la inferencia de IA con NVIDIA Jetson en un solo dispositivo compacto.** La adquisición, la compresión, el preprocesamiento y la inferencia de IA se completan en sitio sin necesidad de un servidor, lo que la hace ideal para **UAV / drones, robótica industrial, dispositivos médicos y sistemas de visión embebida** donde importan las restricciones SWaP (tamaño, peso, potencia).

**Funciones principales**
- Computadora Edge integrada **FPGA + NVIDIA Jetson** (opciones Xavier NX · Orin NX)
- **Factor de forma compacto** — aprox. 13.4 × 9 × 6 cm, ~750 g
- **Procesamiento integrado en la FPGA** — compresión, HDR, mejora de imagen
- **Inferencia de IA basada en CUDA** — adquisición e inferencia simultáneas
- **Opciones robustecidas** — opción I (rango de temperatura extendido), opción R (protección contra vibración / polvo / humedad)
- Adecuada para implementaciones en exteriores, defensa y aeroespacial

### Serie FantoVision 20

Computadora Edge compacta basada en interfaces GigE Vision · Camera Link.

<img src="/assets/images/gen/projects/gidel-fantovision20.png" alt="Serie FantoVision 20" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### Serie FantoVision 40

Computadora Edge de alto desempeño con interfaces CoaXPress-12 y opción 10GigE.

<img src="/assets/images/gen/projects/gidel-fantovision40.png" alt="Serie FantoVision 40" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## Simulador de cámara — CamSim

**Un simulador de cámara basado en PCIe que permite verificar todo el frame grabber y el pipeline de visión sin una cámara física.** Las pruebas deterministas permiten desarrollar algoritmos y validar de forma reproducible pipelines multicámara.

**Línea de modelos**
- **CamSim-CL** — Camera Link (compatible con Deca / Full / Medium / Base)
- **CamSim-X** — CoaXPress multicanal

**Casos de uso**
- Desarrollo y verificación de algoritmos
- Reproducción de pipelines multicámara
- Pruebas deterministas para aislar la causa raíz
- Desarrollo y pruebas antes de contar con el hardware

<img src="/assets/images/gen/projects/gidel-camsim.png" alt="Simulador de cámara CamSim" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

<img src="/assets/images/gen/projects/gidel-camsim-diagram.png" alt="Diagrama del sistema CamSim" style="display:block; width:100%; max-width:560px; height:auto; margin:1rem auto;">

---

## Biblioteca de imágenes — GIL y herramientas de desarrollo

**Una cadena de herramientas de desarrollo unificada, adaptada al hardware de Gidel.** Reutilice IP cores verificados para mayor confiabilidad y cree algoritmos de visión a la medida incluso sin una experiencia profunda en FPGA.

**GIL (Gidel Imaging Library)**
- Biblioteca de IP cores de visión y procesamiento de imágenes basada en 30 años de experiencia en desarrollo FPGA
- **Descarga de la CPU** — la FPGA se encarga del cómputo pesado y libera recursos del sistema
- **IP cores diversos** — sistema (Multiport · MultiFIFO), interfaz de cámara, procesamiento de imágenes (debayer · histograma · morfología), depuración
- **IP cores de compresión** — JPEG · Lossless · Quality+
- **Virtualización de FPGA** — varias aplicaciones comparten la FPGA de forma simultánea
- **Compatibilidad con el estándar GenICam**

**ProcVision Suite**
- Desarrollo y compilación de IP cores FPGA a la medida basados en C/C++
- Implementación de algoritmos accesible para quienes no son expertos en FPGA → desarrollo más rápido
- Personalización OEM/ODM ágil

**SkyBoost SDK**
- API de alta velocidad RAW → JPEG
- Acelerado por hardware, más rápido que sus equivalentes en software

---

## Áreas de aplicación

Los productos Gidel se implementan en industrias donde el desempeño determinista en tiempo real y la sincronización multicámara son críticos.

<img src="/assets/images/gen/projects/machine-vision-applications.svg" alt="Áreas de aplicación de Gidel — 8 industrias" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

---

## Soluciones integradas con VCANUS

Más allá de distribuir los productos Gidel, VCANUS los combina con su propia **plataforma de datos (TSLoom)** y su **plataforma de visión con IA (DeepVi)** para ofrecer **soluciones de visión industrial End-to-End**.

<img src="/assets/images/gen/projects/machine-vision-solutions.svg" alt="Escenarios de soluciones integradas VCANUS + Gidel" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">
