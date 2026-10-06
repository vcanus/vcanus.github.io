---
lang: ja
title: "RoboScan250"
description: "移動ロボットによる3D形状・変形計測の自動化システム"
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
  sub_heading: "3D形状・変形計測の自動化<br> — 移動ロボットとデジタル計測センサーで実現"
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
      - text: "今すぐ購入"
        url: "https://www.zerostatic.io/theme/jekyll-advance/"
        external: true
        fa_icon: false
        size: large
        outline: false
        style: "primary"
---

## 移動ロボットによる3D形状・変形計測の自動化システム

**RoboScan250** は、**自律移動ロボット（AMR）**、**6軸多関節ロボット**、**ZEISS ARAMIS デジタル計測センサー（ドイツ）** を1つのプラットフォームに統合し、**3D形状・変形計測を自動化**します。ロボットが計測対象まで自律走行し、多関節ロボットが計測姿勢を決め、高精度な3D変位・動き・ひずみを自動で計測します。計測シーケンスは**デジタルツインの仮想環境**で事前に検証し、**Web ベースの統合モニタリング・制御**によりロボットと計測機器の状態をリアルタイムで管理します。

---

## 主な機能

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 高精度3D形状計測
- **ZEISS ARAMIS** 計測システム（ドイツ）
- 解像度 **4096 x 3000 pixel**
- フレームレート **25 Hz ~ 100 Hz**
- 計測エリア **20 x 15 ~ 1800 x 1500 mm²**
- **3D変位・動き**の計測
- **ひずみ**計測
- **LED 照明**

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 計測パス生成とシーケンス管理

<ul>
<li><strong>ロボットの計測位置・姿勢の調整</strong>
<ul style="list-style:circle;">
<li>協働ロボットのダイレクトティーチング</li>
<li>ティーチングペンダント</li>
<li>仮想環境</li>
</ul>
</li>
<li><strong>計測シーケンスの作成と管理</strong>
<ul style="list-style:circle;">
<li>ロボット移動・計測のタスク作成</li>
<li>タスクごとの詳細設定</li>
<li>タスクの追加・移動・削除</li>
<li>保存・読み込みなどのシーケンス管理</li>
</ul>
</li>
</ul>

</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### デジタルツインと仮想環境要素の管理

<ul>
<li><strong>仮想環境でのシーケンス検証</strong>
<ul style="list-style:circle;">
<li>ロボットの位置・姿勢の確認</li>
<li>計測エリアの確認</li>
</ul>
</li>
<li><strong>仮想環境要素の管理</strong>
<ul style="list-style:circle;">
<li>対象物 CAD データの取り込みと画面への登録</li>
<li>ロボットデータの管理</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### リアルタイムモニタリングと統合制御

<ul>
<li><strong>Web ベースの設備状態統合モニタリング</strong>
<ul style="list-style:circle;">
<li>ロボットと計測機器の状態をリアルタイムで監視</li>
</ul>
</li>
<li><strong>シーケンス実行状態のモニタリング</strong>
<ul style="list-style:circle;">
<li>移動・姿勢・計測タスクの管理</li>
<li>タスク一覧と実行状態の表示</li>
<li>ログメッセージによる原因分析</li>
</ul>
</li>
<li><strong>Web ベースのロボット制御</strong></li>
<li><strong>AMR の位置・経路計画 → 自律走行</strong></li>
</ul>

</div>
</div>

---

## システム構成

### 移動ロボット（AMR）
- **寸法**：870 x 600 x 265 mm
- **速度**：1.5 m/s（最大）
- **質量**：130 kg
- **可搬重量**：250 kg
- **精度**：グローバル ±30 mm / ドッキング ±5 mm
- **バッテリー**：48V 出力 x 1、24V 出力 x 1（全負荷で8時間稼働、充電90分）
- **充電ステーション**：入力 AC 90~264 V、最大消費電力 2200 W
- 手動充電ユニット付属

### 6軸多関節ロボット

お客様の要件に応じて、次の2種類の6軸協働ロボットから選択できます。

**Type A**
- **軸数**：6軸 / **可搬重量**：9 kg / **リーチ**：1,200 mm / **繰り返し精度**：±0.05 mm
- **DC コントローラ内蔵**：DC コンバータ不要
- **PDB ボード**：回路保護、電源入力 24~48V、最大 80A
- **付属品**：ユニバーサルアダプタ、AMR 取付フレームおよびカバー

**Type B**
- **軸数**：6軸 / **可搬重量**：7 kg / **リーチ**：1,210 mm / **繰り返し精度**：±0.1 mm
- **DC-AC インバータ**：AMR の DC 電源 → ロボットの AC 電源へ変換、入力 48V DC / 出力 220V AC、定格 3kW
- **PDB ボード**：回路保護、電源入力 24~48V、最大 80A
- **付属品**：ユニバーサルアダプタ、AMR 取付フレームおよびカバー

### デジタル計測センサー（ZEISS ARAMIS）
- **メーカー**：ZEISS
- **カメラ解像度**：4096 x 3000 pixel（25 Hz、フル）～ビニング時最大 100 Hz
- **フレームレート**：25 Hz ~ 100 Hz
- **ひずみ計測範囲**：0.02% ～ 100% 超
- **計測エリア**：20 x 15 ~ 1800 x 1500 mm² / **質量**：1.0 kg / **照明**：LED
- **処理用コンピュータ**：Intel Core i9-13950HX、RAM 64GB DDR5、NVIDIA RTX 3500 Ada 12GB、17インチディスプレイ、1TB SSD、Windows 11
- USB 3m ケーブル、単焦点マクロレンズ1本付属

**ARAMIS 活用事例 — 引張試験片の全視野ひずみ計測**

<img src="/assets/images/gen/services/roboscan-aramis-usage.webp" alt="ARAMIS 活用事例 — 引張試験片の全視野ひずみ計測とひずみ集中の可視化" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

ARAMIS は表面の変位とひずみをピクセル単位で算出し、ひずみ集中箇所をカラーマップで可視化します。静的・動的荷重試験において、き裂、くびれ（ネッキング）、局所変形の挙動を定量的に解析します。

### 統合運用コンピュータ
- **CPU**：Ultra7-265（20 コア / 20 スレッド） / **メモリ**：32GB DDR5 / **ストレージ**：1TB SSD
- **電源**：80+ 700W ATX
- **OS**：Linux（ARAMIS 処理用コンピュータは Windows で動作）
- **モニター**：27インチ、1920 x 1080、HDMI / キーボード・マウス付属

---

## 計測製品ラインナップの拡張

標準の **ZEISS ARAMIS** 構成に加え、RoboScan250 のデジタル計測センサーは、計測目的と対象に応じて **ARAMIS 3D シリーズ** と **ATOS 5 シリーズ** から選択して拡張できます。動的な変形・動きの計測には ARAMIS 3D を、精密な3D形状スキャンには ATOS 5 を適用し、現場の要件に合った計測ラインナップを構成します。

### ARAMIS 3D シリーズ — 3D変形・動的挙動の計測

対象物の変位、ひずみ、振動などの**動的挙動を全視野で計測**する光学式計測システムです。計測ボリュームとフレームレートに応じてモデルを選択できます。

<img src="/assets/images/gen/services/roboscan-aramis3d.webp" alt="ARAMIS 3D シリーズ — ARAMIS 3D Camera 12M と ARAMIS SRX の仕様比較" style="display:block; width:100%; height:auto; max-width:1000px; margin:1.5rem auto;">

- **ARAMIS 3D Camera 12M**：4096 x 3000 pixel、最大 150 fps、計測ボリューム 35 x 25 mm ~ 5000 x 4000 mm
- **ARAMIS SRX**：4096 x 3068 pixel、カメラ内蔵 RAM（8GB）を用いた最大約 2000 fps の高速計測、計測ボリューム 70 x 50 mm ~ 5100 x 4200 mm

### ATOS 5 シリーズ — 高精度3D形状スキャン

対象物の**表面形状を高密度な3Dデータとしてスキャン**する構造化光方式のシステムです。計測ボリュームと詳細度の要件に応じてモデルを選択できます。

<img src="/assets/images/gen/services/roboscan-atos5.webp" alt="ATOS 5 シリーズ — ZEISS ATOS LRX、ATOS 5 for Airfoil、ATOS 5、ATOS 5X の仕様比較" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

- **ZEISS ATOS LRX**：超大型ボリュームの3Dスキャン（LASER）、作動距離 1810 mm
- **ATOS 5 for Airfoil**：微細形状の精密スキャン（LED）、作動距離 530 mm
- **ATOS 5**：高速3Dスキャンシステム（LED）、作動距離 880 mm
- **ATOS 5X**：大型ボリュームの自動スキャン（LASER）、作動距離 880 mm

---

## 統合運用ソフトウェア

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### ロボット制御

<ul>
<li><strong>移動ロボットの制御</strong>
<ul style="list-style:circle;">
<li>マップ生成</li>
<li>経路生成</li>
<li>自律移動</li>
</ul>
</li>
<li><strong>多関節ロボットの制御</strong>
<ul style="list-style:circle;">
<li>動作・姿勢制御（軸ごと / 先端点）</li>
<li>ティーチング制御（ペンダント / ダイレクトティーチング）</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 統合制御と計測

<ul>
<li><strong>Web ベースのリアルタイムモニタリングと表示</strong>
<ul style="list-style:circle;">
<li>ロボットの位置・姿勢</li>
<li>設備・シーケンスの状態</li>
</ul>
</li>
<li><strong>タスク・シーケンス制御</strong>
<ul style="list-style:circle;">
<li>作成 / 保存 / 読み込み</li>
<li>開始 / 停止 / キャンセル</li>
<li>パラメータ設定</li>
<li>追加 / 移動 / 削除</li>
</ul>
</li>
<li><strong>計測</strong>
<ul style="list-style:circle;">
<li>3D変位・動き・ひずみ</li>
<li>全視野の表面解析とポイントベースの動的解析</li>
<li>ZEISS CORRELATE / Inspect との連携</li>
<li>計測データの取得とプロジェクト管理</li>
<li>外部計測信号との同期</li>
</ul>
</li>
</ul>

</div>
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### 仮想環境

<ul>
<li><strong>仮想環境の構築</strong>
<ul style="list-style:circle;">
<li>ロボットの構成</li>
<li>対象物 CAD（glTF）の取り込みと読み込み</li>
<li>ロボットと対象物の表示</li>
</ul>
</li>
<li><strong>計測機器とエリアの設定</strong>
<ul style="list-style:circle;">
<li>計測機器の構成</li>
<li>視錐台（フラスタム）エリアの構成</li>
<li>計測エリアの表示</li>
</ul>
</li>
<li><strong>仮想シミュレーション</strong>
<ul style="list-style:circle;">
<li>ロボット位置の設定と移動</li>
<li>姿勢の変更（軸ごと / IK / Gizmo）</li>
<li>ビューのズームイン・アウトとパン</li>
</ul>
</li>
<li><strong>シーケンス検証</strong>
<ul style="list-style:circle;">
<li>移動・姿勢・計測タスクの追加</li>
<li>タスクシーケンスのシミュレーションと検証</li>
</ul>
</li>
</ul>

</div>
</div>

---

## RoboScan250 をひと言で

> **ロボットが自ら移動して計測する — 完全自動の3D形状・変形計測。**

RoboScan250 は、自律移動ロボット、6軸多関節ロボット、ZEISS ARAMIS デジタル計測センサーを統合し、**移動 → 姿勢制御 → 高精度3D計測** の全工程を自動化します。デジタルツインの仮想環境で計測シーケンスを事前に検証し、Web ベースの統合制御によりロボットと計測機器をリアルタイムで運用することで、計測の精度と再現性を確保します。
