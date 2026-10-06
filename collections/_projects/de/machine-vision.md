---
lang: de
title: "Machine Vision"
description: "FPGA-basierte Machine-Vision-Lösungen von Gidel – VCANUS, offizieller Distributor in Korea"
date: 2019-10-03
weight: 2
header_transparent: false
thumbnail: "/assets/images/gen/projects/machine-vision-thumbnail.webp"
image: "/assets/images/gen/projects/machine-vision-large.webp"

hero:
  enabled: true
  heading: "Machine-Vision-Lösungen"
  sub_heading: "FPGA-basierte Machine-Vision-Lösungen von Gidel"
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
      - text: "Jetzt kaufen"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: true
        style: "primary"
---

## FPGA-basierte Machine-Vision-Lösungen von Gidel – in Korea bereitgestellt von VCANUS

**Gidel** (Israel) ist ein weltweit tätiger Spezialist mit über 30 Jahren Fokus auf FPGA-basierte Machine Vision. Das Portfolio deckt die gesamte Bildverarbeitungskette ab – **PCIe-Framegrabber**, **integrierte Edge-Computer mit FPGA + NVIDIA Jetson**, **Kamerasimulatoren** und **Bibliotheken mit Imaging-IP-Cores**.

**VCANUS ist der offizielle Distributor von Gidel in Korea** und bietet koreanischen Kunden Produktlieferung, technischen Support und kundenspezifische Integration für industrielle Bildverarbeitung, UAV, Verteidigung, Medizintechnik, Sport-AR und ATE-Anwendungen.

**Wesentliche Merkmale der Gidel Produktlinie**

- **Deterministische Verarbeitung auf FPGA-Basis** – Echtzeitleistung auf Hardwareebene, kein OS-Jitter, Zero Frame Loss
- **Mehrkamera-Schnittstellen** – GigE Vision · CoaXPress-12 · Camera Link auf einer einzigen Plattform
- **Echtzeit-Kompression im FPGA** – IP-Cores für JPEG · Lossless · Quality+ · HDR
- **Mehrkamera-Synchronisation (InfiniVision)** – Synchronisation im Nanosekundenbereich über mehr als 100 Kameras
- **Integration von KI-Edge-Computing** – kombinierter Edge-Computer aus FPGA + NVIDIA Jetson
- **Entwicklungswerkzeuge und Anpassung** – ProcVision Suite · GIL · CamSim · SkyBoost SDK

---

## Framegrabber – HawkEye Serie

**Framegrabber für den PCIe-Steckplatz.** Industrielle Kameraschnittstellen auf einer einzigen Karte vereint, mit FPGA-Bildverarbeitung auf der Karte einschließlich Kompression, HDR und Debayering.

**Wesentliche Funktionen**
- **Produktreihe mit mehreren Schnittstellen** – Modelle für GigE Vision · CoaXPress-12 · Camera Link
- **Zero Frame Loss · keine CPU-Last** – direkte DMA-Übertragung per Hardware
- **FPGA-Verarbeitung auf der Karte** – Bildverarbeitung, Kompression und HDR in Echtzeit
- **PoCXP / PoCL** – Strom und Daten über dasselbe Kabel für vereinfachte Verkabelung
- **InfiniVision-kompatibel** – Erweiterung zur Mehrkamera-Synchronisation

### GigE-Vision-Modelle

Gleichzeitige Mehrkanalerfassung industrieller GigE-Vision-Kameras auf einer einzigen Karte.

<img src="/assets/images/gen/projects/gidel-hawkeye-gige.png" alt="HawkEye GigE Vision Framegrabber" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### CoaXPress-Modelle

Anbindung industrieller Kameras mit hoher Bandbreite über CoaXPress-12.

<img src="/assets/images/gen/projects/gidel-hawkeye-cxp.png" alt="HawkEye CoaXPress Framegrabber" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### Camera-Link-Modelle

Unterstützung der Camera-Link-Schnittstellen Deca / Full / Medium / Base.

<img src="/assets/images/gen/projects/gidel-hawkeye-cl.png" alt="HawkEye Camera Link Framegrabber" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## FantoVision – IoT-Edge-Computer (FPGA + Jetson)

**Ein Edge-Computer, der FPGA-basierte Bilderfassung und KI-Inferenz mit NVIDIA Jetson in einem kompakten Gerät vereint.** Bilderfassung, Kompression, Vorverarbeitung und KI-Inferenz erfolgen direkt vor Ort ohne Server – ideal für **UAV / Drohnen, Industrierobotik, Medizingeräte und Embedded-Vision-Systeme**, bei denen SWaP-Vorgaben (Größe, Gewicht, Leistung) entscheidend sind.

**Wesentliche Funktionen**
- Integrierter Edge-Computer aus **FPGA + NVIDIA Jetson** (Optionen Xavier NX · Orin NX)
- **Kompakte Bauform** – ca. 13,4 × 9 × 6 cm, ca. 750 g
- **FPGA-Verarbeitung im Gerät** – Kompression, HDR, Bildverbesserung
- **CUDA-basierte KI-Inferenz** – gleichzeitige Erfassung und Inferenz
- **Robuste Ausführungen** – Option I (erweiterter Temperaturbereich), Option R (Schutz gegen Vibration / Staub / Feuchtigkeit)
- Geeignet für Einsätze im Außenbereich, in der Verteidigung sowie in der Luft- und Raumfahrt

### FantoVision 20 Serie

Kompakter Edge-Computer mit GigE-Vision- und Camera-Link-Schnittstellen.

<img src="/assets/images/gen/projects/gidel-fantovision20.png" alt="FantoVision 20 Serie" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

### FantoVision 40 Serie

Leistungsstarker Edge-Computer mit CoaXPress-12-Schnittstellen und 10GigE-Option.

<img src="/assets/images/gen/projects/gidel-fantovision40.png" alt="FantoVision 40 Serie" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

---

## Kamerasimulator – CamSim

**Ein PCIe-basierter Kamerasimulator, mit dem Sie Framegrabber und die gesamte Bildverarbeitungskette ohne physische Kamera verifizieren können.** Deterministische Tests ermöglichen Algorithmenentwicklung und die reproduzierbare Validierung von Mehrkamera-Pipelines.

**Modellreihe**
- **CamSim-CL** – Camera Link (Unterstützung für Deca / Full / Medium / Base)
- **CamSim-X** – Mehrkanal-CoaXPress

**Anwendungsfälle**
- Entwicklung und Verifizierung von Algorithmen
- Reproduktion von Mehrkamera-Pipelines
- Deterministische Tests zur Ursacheneingrenzung
- Entwicklung und Tests vor Verfügbarkeit der Hardware

<img src="/assets/images/gen/projects/gidel-camsim.png" alt="CamSim Kamerasimulator" style="display:block; width:100%; max-width:720px; height:auto; margin:0 auto;">

<img src="/assets/images/gen/projects/gidel-camsim-diagram.png" alt="CamSim Systemdiagramm" style="display:block; width:100%; max-width:560px; height:auto; margin:1rem auto;">

---

## Imaging-Bibliothek – GIL und Entwicklungswerkzeuge

**Eine einheitliche, auf Gidel Hardware abgestimmte Entwicklungsumgebung.** Verwenden Sie bewährte IP-Cores für hohe Zuverlässigkeit und entwickeln Sie eigene Bildverarbeitungsalgorithmen auch ohne tiefgehende FPGA-Kenntnisse.

**GIL (Gidel Imaging Library)**
- Bibliothek mit Vision- und Imaging-IP-Cores auf Basis von 30 Jahren FPGA-Entwicklungserfahrung
- **CPU-Entlastung** – das FPGA übernimmt rechenintensive Aufgaben und schont Systemressourcen
- **Vielfältige IP-Cores** – System (Multiport · MultiFIFO), Kameraschnittstellen, Bildverarbeitung (Debayer · Histogramm · Morphologie), Debugging
- **Kompressions-IP-Cores** – JPEG · Lossless · Quality+
- **FPGA-Virtualisierung** – mehrere Anwendungen nutzen das FPGA gleichzeitig
- **Unterstützung des GenICam-Standards**

**ProcVision Suite**
- Entwicklung und Kompilierung eigener FPGA-IP-Cores auf Basis von C/C++
- Algorithmenimplementierung auch für Nicht-FPGA-Experten → schnellere Entwicklung
- Schnelle OEM/ODM-Anpassung

**SkyBoost SDK**
- Hochgeschwindigkeits-API für RAW → JPEG
- Hardwarebeschleunigt und schneller als Softwarelösungen

---

## Anwendungsbereiche

Gidel Produkte werden in Branchen eingesetzt, in denen deterministische Echtzeitleistung und Mehrkamera-Synchronisation entscheidend sind.

<img src="/assets/images/gen/projects/machine-vision-applications.svg" alt="Gidel Anwendungsbereiche – 8 Branchen" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

---

## Integrierte Lösungen mit VCANUS

Über den reinen Vertrieb von Gidel Produkten hinaus kombiniert VCANUS diese mit der eigenen **Datenplattform (TSLoom)** und der **KI-Vision-Plattform (DeepVi)** zu **End-to-End-Lösungen für die industrielle Bildverarbeitung**.

<img src="/assets/images/gen/projects/machine-vision-solutions.svg" alt="Integrierte Lösungsszenarien von VCANUS + Gidel" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">
