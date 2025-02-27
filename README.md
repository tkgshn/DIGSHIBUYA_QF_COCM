# 寄付フロー＆QF シミュレーション比較アプリケーション

このアプリケーションは、寄付データを視覚化し、異なる四次関数資金調達（Quadratic Funding、QF）アルゴリズムのシミュレーション結果を比較するためのインタラクティブなツールです。

## プロジェクト構造

このプロジェクトは、モジュール化された React アプリケーションとして再構築されています。主要なディレクトリ構造は以下の通りです：

```
/
├── src/
│   ├── algorithms/         # 数学的アルゴリズム
│   │   ├── kMeansClustering.js
│   │   └── pcaProjection.js
│   ├── components/         # UIコンポーネント
│   │   ├── App.js
│   │   ├── ControlPanel.js
│   │   ├── QFTable.js
│   │   ├── QFBarChart.js
│   │   ├── QFLineChart.js
│   │   ├── QFCumulativeChart.js
│   │   └── QFComparison.js
│   ├── hooks/              # カスタムフック
│   │   ├── useDataLoader.js
│   │   ├── useDonationData.js
│   │   └── usePlotlyChart.js
│   ├── utils/              # ユーティリティ関数
│   │   └── qfCalculations.js
│   ├── visualizations/     # 可視化コンポーネント
│   │   ├── SankeyDiagram.js
│   │   ├── Network3D.js
│   │   └── Clustering2D.js
│   ├── styles/             # スタイルシート
│   │   └── main.css
│   └── index.js            # エントリーポイント
├── index.html              # HTMLテンプレート
├── cocm_network.html       # COCM ネットワーク可視化
├── package.json            # プロジェクト設定
└── Contribution.json       # 寄付データ（既存）
```

## セットアップと実行方法

### 必要条件

- Node.js（バージョン 14 以上推奨）
- npm（Node.js に付属）

### インストール

1. 依存パッケージをインストールします：

```bash
npm install react react-dom plotly.js numeric d3
```

### 開発サーバーの起動

1. 開発サーバーを起動します：

```bash
npm start
```

2. ブラウザで http://localhost:1234 を開きます（Parcel のデフォルトポート）

### ビルド

本番用にアプリケーションをビルドするには：

```bash
npm run build
```

ビルドされたファイルは `dist` ディレクトリに出力されます。

## 機能

- 寄付者からプロジェクトへの資金フローの可視化（Sankey 図）
- 寄付者とプロジェクトの関係性の 3D 可視化
- 寄付パターンに基づく寄付者のクラスタリング（PCA + k-means）
- 通常 QF と COCM QF の比較シミュレーション
  - プロジェクト別寄付総額とマッチング額
  - 順位別割り当て総額の配分
  - 累積資金配分の公平性
- COCM ネットワーク可視化（cocm_network.html）
  - 寄付者とプロジェクトのクラスタリングによる関係性の可視化
  - 3D および 2D フォースレイアウトによるネットワーク表示
  - クラスター選択による同質的なコミュニティの強調表示
  - 「Crypto Babes Club」のような同質的なコミュニティからのみ支持されているプロジェクトの識別

## 技術スタック

- React 17
- Plotly.js（データ可視化）
- D3.js（フォースレイアウト可視化）
- numeric.js（数値計算、PCA実装）
- Parcel（バンドラー）

## COCM（Connection-Oriented Cluster Matching）について

COCM は、Quadratic Funding (QF) におけるSybil攻撃や調整されたグループによる操作を防ぐために開発された手法です。

主な特徴:
1. 寄付者のクラスタリング: 寄付パターンに基づいて寄付者をグループ化
2. 多様性の評価: 異なるクラスターから支持を集めるプロジェクトを優遇
3. コミュニティコンセンサス: 単に「最大のネットワーク」ではなく「共有ネットワークでの最大のコンセンサス」を重視

cocm_network.html では、この概念を視覚的に理解できるよう、寄付者とプロジェクトの関係性をクラスタリングに基づいて可視化しています。
