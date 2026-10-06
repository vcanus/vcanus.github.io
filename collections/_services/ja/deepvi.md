---
lang: ja
title: "DeepVi"
description: "AIビジョン分析プラットフォーム"
date: 2019-10-03
weight: 2
header_transparent: false
fa_icon: false
icon: "assets/images/icons/deepvi-icon.svg"
thumbnail: "/assets/images/gen/services/deepvi-thumb.webp"
image: "/assets/images/gen/services/deepvi-hero.webp"

hero:
  enabled: true
  heading: "AIビジョン分析プラットフォーム"
  sub_heading: "画像収集からモデル学習、精密検査、デプロイまで<br>— すべてをDeepViプラットフォームで"
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
      - text: "DeepVi ベータ版を試す"
        url: "https://www.deepvi.app/?utm_source=vcanus_home&utm_medium=product_hero"
        external: true
        fa_icon: false
        size: large
        outline: false
        style: "light"
---

## AIビジョン分析プラットフォーム

**DeepVi**は、**データ収集からモデル学習、精密検査、デプロイ、再学習まで**を単一のプラットフォームで完結する、**No-Code・End-to-EndのAIビジョンプラットフォーム**です。学習と推論は**Built-in Workflow**でひと目で監視・制御でき、ワークフローは**VCANUSワークフローエディター**で拡張・編集できます。ディープラーニング（Classification · Detection · Segmentation）に加え、画像解析で広く使われる精密検査機能である**Align · Inspection（位置合わせ、計測、コード読み取り）**も搭載しています。**専任の開発チームは不要**で、現場の担当者がラベリング、学習、検査、推論、レビューの一連のサイクルを自ら運用できます。**オンプレミスとクラウド**の両方の導入形態に対応し、製造、スマート農業、物流、セキュリティなど**あらゆる産業ですぐに使える**汎用パイプラインを提供します。

<img src="/assets/images/gen/services/deepvi-overview.svg" alt="DeepVi End-to-Endパイプラインの概要" style="display:block; width:100%; height:auto; max-width:1100px; margin:1.5rem auto;">

---

## DeepViでできること

<img src="/assets/images/gen/services/deepvi-capabilities.svg" alt="DeepViの4つのコアバリュー" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

---

## 適用分野

<img src="/assets/images/gen/services/deepvi-applications.svg" alt="DeepViの適用分野 — 4業種の導入前後" style="display:block; width:100%; height:auto; max-width:1100px; margin:0 auto;">

同じパイプラインが業種を問わず機能します。**クラス名とデータを変更するだけで**、製造、スマート農業、物流、セキュリティにとどまらず、医療・ヘルスケア、光学選別、組込みビジョン、自動試験装置（ATE）などへすぐに展開できます。

---

## 主な機能

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Storage（データ管理）
- 大量の画像を登録できる**Webからの一括アップロード**
- **フォルダベースの管理**：フォルダの作成・移動・削除、複数選択での一括移動
- サムネイルの自動生成による**大規模データの高速閲覧**
- **ストレージ使用量**をひと目で確認
- **元データを永続的に保存**し、容易に再利用可能
- データセットは元データを参照するため、データセットを追加しても**ストレージ使用量は一定**

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_storage.webp" alt="DeepVi Storage画面" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Dataset（ラベリング）
- Classification · Detection · Segmentationの3タイプすべてに対応した**統合ラベリング環境**
- **BBox · Polygon · Mask**の高精度ラベリングツール
- **AIアシストによるセグメンテーションとAuto Labeling**でラベリング時間を短縮
- **COCOなどの標準形式でのインポート/エクスポート**、カテゴリーテンプレート
- 再現性のある学習のための**データセットスナップショットの公開**（train/val/test分割を固定）

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_dataset.webp" alt="DeepVi Datasetラベリング画面" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Training · Model（ワークフロー学習と検証）
- **Built-in Workflow**：学習フロー、ノードの状態、ログを1画面に表示
- ノードごとの**実行・一時停止・再開**、パラメーター調整
- **VCANUSワークフローエディター**でワークフローを拡張・編集
- **Fast / Standardのモデルファミリー**、ファミリーの追加も可能
- **Anomaly Detection**：構造的異常と論理的異常の学習
- **Transfer Learning**と**Early Stopping**、リアルタイムのLossチャート
- **Confusion Matrix**と**mAP**による性能評価、**チェックポイントとONNX**のエクスポート

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_training.webp" alt="DeepVi Trainingワークフロー画面" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Align · Inspection（精密検査）
- **基準画像の登録**とワンクリックでのAlignモデル作成
- **位置ずれと回転の自動補正**（Align）
- **6種類の検査ツール**：Caliper · Circle · Distance · Angle · Code · Template
- **公差に基づくOK/NG判定**、基準画像でのゴールデンドライラン
- 推論ワークフローで**ディープラーニングの結果と並行してリアルタイム判定**

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_inspection.webp" alt="DeepVi Align · Inspection画面" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Inference（リアルタイム推論）
- **カメラストリームまたは画像ファイル**からのライブ推論
- アルゴリズムを素早く構成できる**ワークフローベースのインターフェース**（カスタムノードの追加）
- 検出結果と信頼度をリアルタイム表示、**前処理・推論・後処理の時間分析**
- 検出・セグメンテーション・分類の結果を**Align · InspectionのOK/NGと併せて**表示
- **結果、座標、タイムスタンプを自動保存**、条件フィルターによる**履歴検索**
- **結果に応じたアクション**：装置制御、データロギング、アラートなどをワークフローのアクションとして実行

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_inference.webp" alt="DeepVi Inference画面" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

<div style="display:flex; flex-wrap:wrap; gap:2rem; align-items:flex-start; margin-bottom:2rem;">
<div style="flex:1 1 280px; min-width:280px;" markdown="1">

### Review（モデル改善）
- **誤検出のレビュー、再ラベリング、コメント**を通じて学習データを蓄積
- **レビューステータス管理**：承認、却下（理由コード付き）、破棄、および項目ごとの履歴
- レビュー済みラベルと元の予測結果を**比較・編集**
- レビュー済みデータを**データセットに反映 → 再学習**
- 性能評価後、**本番モデルを検証済みモデルに置き換え**

</div>
<div style="flex:1 1 280px; max-width:420px; min-width:0;">
<img src="/assets/images/gen/services/deepvi_review.webp" alt="DeepVi Review画面" style="display:block; width:100%; max-width:420px; height:auto;">
</div>
</div>

---

## DeepViをひと言で

> **コーディング不要、ひとつのプラットフォームですべてを完結。DeepViはAI導入のあらゆる障壁を取り除きます。**

DeepViは、**End-to-EndのAIビジョンパイプライン全体**を単一のプラットフォームで処理します：データ収集（Storage）→ ラベリング（Dataset）→ ワークフロー学習（Training）→ 精密検査（Align · Inspection）→ リアルタイム推論（Inference）→ モデル改善（Review）。同じパイプラインが業種を問わず機能し、**クラス名とデータを変更するだけで**、製造、スマート農業、物流、セキュリティ、医用画像などにすぐに適用できます。

<div style="text-align:center; margin:2.5rem 0 1rem;">
<p style="margin-bottom:1rem;">ベータ期間中は無料でご利用いただけます。</p>
{% include framework/button.html text="DeepVi ベータ版を試す" url="https://www.deepvi.app/?utm_source=vcanus_home&utm_medium=product_bottom" external=true size="large" style="primary" %}
</div>
