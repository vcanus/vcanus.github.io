---
lang: ja
layout: list
collection: "projects"
title: プロジェクト
description: "当社の実績とプロジェクトのご紹介。"
permalink: "/projects/"
header_transparent: true

hero:
  enabled: true
  heading: "ソリューション"
  sub_heading: "長年培ってきた産業分野の専門知識に裏打ちされた、最先端のソリューションを提供します。"
  text_color: "#FFFFFF"
  background_color: false
  background_gradient: true
  background_image: "/assets/images/gen/home/home-2-large.webp"
  background_image_blend_mode: overlay # "overlay", "multiply", "screen"
  fullscreen_mobile: false
  fullscreen_desktop: false
  height: "500px"
  buttons:
    enabled: false
    list:
      - text: "お問い合わせ"
        url: "/contact"
        external: false
        fa_icon: false
        size: large
        outline: true
        style: "light"

grid:
  collection: "projects"
  sort_by: "weight" # "date", "weight"
  columns: 3
  prevent_click: false

intro:
  enabled: false
  align: left
  image: false
  heading: ""
  sub_heading: ""
  features:
    enabled: true
    list:
      - text: "一部のプロジェクトはオープンソースです"
        fa_icon: false
  buttons:
    enabled: true
    list:
      - text: "GitHubを見る"
        url: "https://github.com/zerostaticthemes"
        external: true
        fa_icon: "fab fa-github"
        size: "large"
        outline: false
        style: "primary"

outro:
  enabled: true
  align: left
  image: false
  heading: "データドリブンの専門性で、複雑な課題を解決します。"
  sub_heading: "構想からデプロイまで、お客様のビジョンをインテリジェントなソリューションへと形にします。"
  buttons:
    enabled: true
    list:
      - text: "お問い合わせはこちら"
        url: "/contact"
        external: false
        fa_icon: false
        size: "normal"
        outline: false
        style: "primary"
---
