---
lang: ja
title: "VURT-X"
description: "VCANUS Universal Robot Transformation X"
date: 2019-10-03
weight: 3
header_transparent: false
fa_icon: false
icon: "assets/images/icons/vurtx-icon.svg"
thumbnail: "/assets/images/gen/services/vurtx-thumb.webp"
image: "/assets/images/gen/services/vurtx-hero.webp"

hero:
  enabled: true
  heading: "VURT-X"
  sub_heading: "コード不要。ペンダント不要。思いどおりに制御。"
  text_color: "#ffffff"
  background_color: ""
  background_gradient: true
  background_image_blend_mode: false
  background_image: "/assets/images/gen/services/vurtx-hero.webp"
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

## VCANUS Universal Robot Transformation - X

VURT-Xは、産業用ロボットおよび協働ロボットの仮想シミュレーションと、リアルタイムの直接制御のために設計されたユニバーサルロボット変換プラットフォームです。手作業によるティーチング工程を置き換え、従来のロボットコードを不要にすることで、直感的なシーケンス管理とGUIによる直接操作を通じて、迅速な導入、高い柔軟性、自動化の簡素化を実現します。
VURT-Xは、KUKA、Stäubli、FANUC、ABB、Rainbow Roboticsなど複数メーカーのロボットを単一の共通インターフェースで管理できる統合プラットフォームを提供し、メーカーごとのプログラミングを不要にします。さらに、Beckhoff PLC機能を統合しており、自動化システムに不可欠なI/O信号制御（ランプ、スイッチ、ボタンなど）をシームレスに行えます。
多様なロボットを運用するメーカーにとって、VURT-Xはセットアップ時間を短縮し、プログラミングの複雑さを最小限に抑え、運用効率を高めることで、ロボットの導入と管理をより体系的かつ低コストにします。

## なぜユニバーサルロボット変換が必要なのか

従来のロボットプログラミングはティーチングペンダントと手作業のコーディングに依存しており、時間がかかり、ミスが起きやすく、柔軟性に欠けます。この方式は導入を遅らせるだけでなく、特に複数台のロボットを管理する場合に保守の負担を増大させます。
VURT-Xは次の方法でこれらの課題を解決します。
- GUIによる直接制御で手作業のティーチングを不要にします。
- 自動化されたシーケンス管理で従来のロボットコードを不要にします。
- 仮想シミュレーションでパス検証と干渉チェックを可能にします。
- リアルタイムモニタリングと3D可視化により、高精度な運用と診断を実現します。
メーカー依存で分断されたワークフローを、統合された拡張性の高いソリューションに置き換えることで、VURT-Xは導入を加速し、エンジニアリング負荷を削減し、生産性を向上させます。

## VURT-Xでできること

VURT-Xを使用すると、次のことが可能です。
- 仮想環境でモーションパスをシミュレーション・検証し、干渉を検出する。
- ティーチングペンダントを使わず、直感的なGUIでロボットを直接操作する。
- ロボットと外部システムの動作を同期し、協調した高精度作業を行う。
- 3D可視化によりロボットの状態をリアルタイムで監視する。
- ポイントツーポイント動作やカスタムタスク（ピック＆プレース、検査、梱包、ラベリングなど）を含むシーケンスを作成・シミュレーション・実行する。
- 組込みPLCをプログラミング・活用し、高度な自動化ロジックを実現する。

<img src="/assets/images/gen/services/vurt-x.png" alt="仕組み" width="900"/>

## 主な機能

### ロボット互換性
- 産業用ロボット：KUKA、Stäubli、FANUC、ABBなど
- 協働ロボット：Rainbow Robotics、Doosan Robotics、Neuromeka

### 仮想シミュレーション
- ユーザー定義の3Dモデル管理（ツール、ターゲット、障害物）。
- 動作可否の検証と干渉チェック。
- シーケンスのシミュレーションと検証。

### 直接操作
- 手動/自動の運転モード。
- ジョグ、早送り、直線動作、各軸動作。
- ポイントツーポイント動作と関節角度による動作制御。

### リアルタイム制御・同期動作
- 外部システムとのデータ交換（EtherCAT、TCP/IP、Beckhoff ADS）。
- サイクルタイム：4～10 ms（ロボットとプロトコルにより異なります）。
- 多軸協調のための速度・位置同期。

### リアルタイムモニタリング・3D可視化
- ロボット状態（関節角度、位置など）のライブモニタリング。
- PLC値のリアルタイム追跡。

### シーケンス制御・タスク管理
- シーケンス制御（開始、停止、一時停止、リセット）。
- タスクの作成・登録・管理（ポイントツーポイント動作、PCまたはPLC連携のカスタムタスク）。
- 安全なタスク実行のためのインターロック設定。

### 高い拡張性
- CAMソフトウェアとの連携によるパス/シーケンスの自動生成。
- 計測機器（3Dビジョン、ToFカメラ、ステレオカメラなど）との互換性。

### PLCプログラミング・活用
- 対応言語：LD（ラダー図）、FBD（ファンクションブロック図）、ST（ストラクチャードテキスト）、SFC（シーケンシャルファンクションチャート）、C/C++。
- PLCパラメーターの読み書きにより、自動化ロジックとシームレスに連携。

### エラー管理
- 誤差補正（セットアップ誤差：座標補正、位置誤差：3Dテーブルベースの補正）。
- 誤差テーブルの管理（登録、更新）。

### ロボットシステムの集中制御（Enterprise Edition）
- 共通インターフェースと使いやすいGUIによる複数メーカーのロボットの統合。
- 複数ロボットのリアルタイムシーケンス制御により、個別のペンダントが不要。
- 3D可視化による工場フロア全体の統合モニタリング。
