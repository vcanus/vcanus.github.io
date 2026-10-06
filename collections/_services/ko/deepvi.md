---
lang: ko
title: "DeepVi"
description: "AI 기반 비전 분석 플랫폼"
date: 2019-10-03
weight: 2
header_transparent: false
fa_icon: false
icon: "assets/images/icons/deepvi-icon.svg"
thumbnail: "/assets/images/gen/services/deepvi-thumb.webp"
image: "/assets/images/gen/services/deepvi-hero.webp"

hero:
  enabled: true
  heading: "AI 기반 비전 분석 플랫폼"
  sub_heading: "이미지 수집부터 모델 학습·정밀 검사·배포까지 DeepVi 플랫폼에서 수행"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: true
  background_image_blend_mode: false # "overlay", "multiply", "screen"
  background_image: "/assets/images/gen/services/deepvi-hero.webp"
  fullscreen_mobile: false
  fullscreen_desktop: false
  height: 660px
  buttons:
    enabled: true
    list:
      - text: "DeepVi 베타 시작하기"
        url: "https://www.deepvi.app/?utm_source=vcanus_home&utm_medium=product_hero"
        external: true
        fa_icon: false
        size: large
        outline: false
        style: "light"
---

## AI 기반 비전 분석 플랫폼

**DeepVi**는 **데이터 수집부터 모델 학습·정밀 검사·배포·재학습까지** 하나의 플랫폼에서 처리하는 **No-Code End-to-End AI 비전 플랫폼**입니다. 학습·추론 과정은 **내장 워크플로**로 한눈에 확인·제어하고, 워크플로 확장·편집은 VCANUS의 **워크플로 편집기**로 수행합니다. 딥러닝(Classification · Detection · Segmentation)과 함께 이미지 분석에 많이 쓰는 **Align · Inspection(정합·계측·판독)** 기능을 탑재해 **별도 개발 인력 없이** 현장 담당자가 라벨링·학습·검사·추론·리뷰 사이클을 직접 운영할 수 있으며, **온프레미스 또는 클라우드** 환경을 선택할 수 있습니다. 제조·스마트팜·물류·보안 등 **다양한 산업 환경에 즉시 적용 가능**한 범용 파이프라인을 제공합니다.

<img src="/assets/images/gen/ko/services/deepvi-overview.svg" alt="DeepVi 전체 파이프라인 개요" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

---

## DeepVi로 할 수 있는 것

<img src="/assets/images/gen/ko/services/deepvi-capabilities.svg" alt="DeepVi 4가지 핵심 가치" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

---

## 적용 분야

<img src="/assets/images/gen/ko/services/deepvi-applications.svg" alt="DeepVi 적용 분야 — 4대 산업 도입 전·후" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

산업이 달라도 동일한 파이프라인이 동작합니다 — **클래스명과 데이터만 바꾸면** 제조·스마트팜·유통·보안뿐 아니라 의료·헬스케어·광학 선별·임베디드 비전·자동 시험 장비(ATE) 등 다양한 분야로 즉시 확장됩니다.

---

## 주요 기능

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Storage (데이터 관리)
- **웹 일괄 업로드**로 대량 이미지 등록
- **폴더 기반 관리** — 생성·이동·삭제, 다중 선택 일괄 이동
- 전용 썸네일 자동 생성으로 **대용량 데이터 고속 탐색**
- **스토리지 사용량** 한눈에 확인
- **원본 데이터 영구 보관** · 재사용 용이
- 데이터셋은 원본을 참조 — 추가해도 **스토리지 용량 불변**

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_storage.webp" alt="DeepVi Storage 화면" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Dataset (라벨링)
- Classification / Detection / Segmentation<br>**3종 라벨링 통합 지원 환경**
- **BBox · Polygon · Mask** 정밀 라벨링 툴
- **AI 보조 분할 · Auto Labeling**으로 라벨링 시간 단축
- **COCO 등 표준 포맷** 가져오기·내보내기, 카테고리 템플릿
- **학습 데이터 스냅샷**(train/val/test 분할 확정)으로 재현 가능한 학습

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_dataset.webp" alt="DeepVi Dataset 라벨링 화면" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Training · Model (워크플로 학습 · 검증)
- **워크플로 탑재** — 학습 흐름·노드 상태·로그를 한 화면에서 확인
- 노드 단위 **실행 · 일시정지 · 재개**, 파라미터 조정
- 워크플로 확장·편집은 **VCANUS 워크플로 편집기** 연동
- **Fast · Standard 2계열 모델** 지원, 모델 계열 추가 가능
- **이상 탐지(Anomaly Detection)** — 구조적 · 논리적 이상 탐지 학습 지원
- **Transfer Learning · Early Stop**, Loss 실시간 차트
- **Confusion Matrix · mAP** 성능 평가, **체크포인트 · ONNX** 내보내기

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_training.webp" alt="DeepVi Training 워크플로 화면" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Align · Inspection (정밀 검사)
- **기준 이미지 등록** 및 Align 모델 원클릭 생성
- **이동 · 회전 자동 보정**(Align)
- **Caliper · Circle · Distance · Angle · Code · Template** 6종 검사 도구
- **공차 기반 OK/NG 판정**, 기준 이미지 사전 검증(Dry-run)
- 추론 워크플로에서 **딥러닝 결과와 함께 실시간 판정**

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_inspection.webp" alt="DeepVi Align · Inspection 화면" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Inference (실시간 추론)
- **카메라 · 파일 이미지** 실시간 연동 추론
- **Workflow 기반** 빠른 알고리즘 구성 (사용자 정의 노드 추가)
- 탐지 결과·신뢰도 실시간 표시 + **전처리·추론·후처리 시간 분석**
- 검출·분할·분류 결과와 **Align·Inspection OK/NG 통합 표시**
- **결과·좌표·시각 자동 저장**, 조건 필터로 **이력 조회**
- **결과 기반 액션** — 판정 결과로 설비 제어 · 데이터 기록 · 알림 등 워크플로 액션 자동 실행

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_inference.webp" alt="DeepVi Inference 화면" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Review (모델 개선)
- **오탐 검토 · 재라벨링 · 코멘트**로 추가 학습 데이터 누적
- **검수 상태 관리** — 승인·거부(사유 코드)·폐기, 항목별 이력 조회
- 원본 예측과 검수 라벨 **비교 편집**
- 검수 완료 데이터를 **데이터셋에 반영 → 재학습**
- 성능 평가 후 **검증된 모델로 운영 모델 교체**

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_review.webp" alt="DeepVi Review 화면" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

---

## DeepVi 한 줄 요약

> **코딩 없이, 하나의 플랫폼에서 — AI 도입의 모든 장벽을 해결합니다.**

DeepVi는 데이터 수집(Storage) → 라벨링(Dataset) → 워크플로 학습(Training) → 정밀 검사(Align · Inspection) → 실시간 추론(Inference) → 모델 개선(Review)까지 **End-to-End AI 비전 파이프라인**을 단일 플랫폼에서 완결합니다. 산업이 달라도 동일한 파이프라인 — **클래스명과 데이터만 바꾸면** 제조 · 스마트팜 · 유통 · 보안 · 의료 등 어떤 분야에도 즉시 적용됩니다.

<div style="text-align:center; margin:2.5rem 0 1rem;">
<p style="margin-bottom:1rem;">지금 베타 기간 동안 무료로 사용해 보세요.</p>
{% include framework/button.html text="DeepVi 베타 시작하기" url="https://www.deepvi.app/?utm_source=vcanus_home&utm_medium=product_bottom" external=true size="large" style="primary" %}
</div>
