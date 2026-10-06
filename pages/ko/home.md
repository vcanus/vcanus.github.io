---
lang: ko
layout: home
permalink: "/"
title: "VCANUS"
description: "Data Innovator"
header_transparent: true
meta_title: "Data Innovator"

hero:
  enabled: true
  heading: "데이터를 지능으로.<br>한 바이트씩."
  sub_heading: "VCANUS는 실시간 분석, Edge AI, 디지털 트윈을 활용하여 다양한 산업에서 더 스마트한 의사결정, 효율적인 자동화, 향상된 정밀도를 실현합니다."
  text_color: "#FFFFFF"
  background_color: "#1d2830"
  background_gradient: true
  background_image: "/assets/images/gen/home/ai-data-innovation-large.webp"
  background_image_blend_mode: overlay # "overlay", "multiply", "screen"
  fullscreen_mobile: true
  fullscreen_desktop: false
  height: "660px"
  buttons:
    enabled: false

services:
  enabled: true
  heading: "우리의 제품"
  sub_heading: "혁신과 효율을 이끄는 최첨단 플랫폼을 만나보세요."
  limit: 4
  columns: 2
  sort: "weight" # 'date'
  view_more_button_text: "전체 제품 보기"
  view_more_button_link: "/services"
  prevent_click: false
 
intro:
  enabled: true
  align: left
  image: "/assets/images/gen/content/where-data-meets-progress-thumbnail.webp"
  heading: "데이터가 발전을 만나는 곳."
  sub_heading: "AI 기반 솔루션이 원시 데이터를 실용적인 인사이트로 변환하여, 기업이 운영의 효율성·정밀도·적응력을 최적화할 수 있도록 지원합니다."
  features:
    enabled: false
    list:
      - text: "Configure the homepage sections in front-matter."
        fa_icon: "fas fa-check"
      - text: "An advanced hero image section with dozens of design options."
        fa_icon: "fas fa-check"
      - text: "Fully responsive and SEO optimised."
        fa_icon: "fas fa-check"
      - text: "Multiple content types including services, projects, blog and more."
        fa_icon: "fas fa-check"
  buttons:
    enabled: true
    list:
      - text: "회사 소개"
        url: "/about"
        external: false
        fa_icon: ""
        size: large
        outline: false
        style: "primary"

partners:
  enabled: false
  limit: 5
  sort: "weight" # 'date'

projects:
  enabled: true
  heading: "우리의 솔루션"
  sub_heading: "데이터와 AI로 실제 문제를 어떻게 해결하는지 살펴보세요."
  limit: 3
  columns: 3
  sort: "weight" # 'date'
  view_more_button_text: "전체 솔루션 보기"
  view_more_button_link: "/projects"
  prevent_click: false

outro:
  enabled: true
  align: center
  image: false
  heading: "데이터 기반 전문성으로 복잡한 과제를 해결하세요."
  sub_heading: "개념에서 배포까지—여러분의 비전을 지능형 솔루션으로 전환합니다."
  features:
    enabled: false
    list:
      - text: "실시간 분석으로 즉각적인 인사이트."
        fa_icon: "fas fa-bolt"
      - text: "Edge AI로 저지연 온디바이스 지능 구현."
        fa_icon: "fas fa-microchip"
      - text: "디지털 트윈으로 가상 테스트 및 시뮬레이션."
        fa_icon: "fas fa-project-diagram"
  buttons:
    enabled: true
    list:
      - text: "지금 문의하기"
        url: "/contact"
        external: false
        size: "large"
        outline: false
        style: "primary"

posts:
  enabled: true
  heading: "최신 게시물"
  sub_heading: "데이터와 AI에 관한 최신 인사이트, 뉴스, 혁신 소식을 확인하세요."
  limit: 3
  columns: 3
  sort: "weight" # 'date'
  view_more_button_text: "전체 게시물 보기"
  view_more_button_link: "/blog"
  prevent_click: false
---
