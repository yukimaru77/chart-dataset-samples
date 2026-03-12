# Chart dataset samples

このディレクトリには、依頼に基づいて実際に見られるグラフ系データセットの少数サンプル／デモを保存しています。

## ディレクトリ構成

- `LineEX/`
  - 出典: https://github.com/Shiva-sankaran/LineEX
  - 内容: 公開リポジトリ内の `sample_input/` と `sample_output/` から取得した画像と一部 JSON
- `ExcelChart400K/`
  - 関連出典:
    - https://github.com/soap117/DeepRule
    - https://github.com/zmykevin/ChartOCR
    - https://huggingface.co/datasets/asbljy/DeepRuleDataset/tree/main （公開ミラー、巨大 zip）
  - 内容: 公式データ本体は multi-GB 級のため、今回は関連実装リポジトリに含まれるデモ画像を保存
- `UB-PMC_CHART-Info/`
  - 出典: https://chartinfo.github.io/toolsanddata.html
  - 内容: `UB_PMC_sample_1.21.zip` をダウンロードして展開した公式 sample

## 何がアノテーションとして付いているか

### 1) LineEX

今回入れている JSON 例:
- `LineEX/pred_data_0.png.json`
- `LineEX/pred_data_1.png.json`

この JSON には、**各折れ線／系列ごとの抽出点列**が入っています。
実体はおおむね次のような形です。

```json
{
  "0.png": [
    [[99, 580], [99, 594], [221, 562], ...],
    [[763, 228]],
    [],
    [[99, 359], [141, 354], [178, 353], ...]
  ]
}
```

読み方:
- キー: 元画像名
- 値: 系列ごとの点列
- 各点: 画像座標 `(x, y)`

つまり LineEX サンプルから分かるのは、主に:
- 線系列ごとの点群
- モデル出力例（検出結果画像、対応付け画像）

### 2) ExcelChart400K / DeepRule 系

今回保存したもの:
- `ExcelChart400K/test.png`
- `ExcelChart400K/target.png`
- `ExcelChart400K/target_draw.png`

このディレクトリには今回は**本体アノテーション JSON は未同梱**です。
ただし公開されている DeepRuleDataset / DeepRule README から、代表的な注釈形式は以下です。

- **Line**: 折れ線上のデータ点列
  - 例: `[x1, y1, x2, y2, ...]`
- **Bar**: 棒の bounding box
- **Pie**: 扇形を定義する 3 点
  - 例: `[center_x, center_y, edge1_x, edge1_y, edge2_x, edge2_y]`
- **Cls / chart components**: タイトル、凡例、描画領域などの bounding box

要するに、ExcelChart400K 系では主に:
- チャート要素の bbox
- 線のデータ点
- 円グラフ扇形の幾何情報
- チャート構成要素ラベル

が注釈対象です。

### 3) UB-PMC / CHART-Info

今回入れている JSON 例:
- `UB-PMC_CHART-Info/sample/UB_PMC_sample/PMC3104219___1471-2458-11-S4-S6-2.json`

この JSON は **タスク別の統合注釈** になっています。サンプルから確認できた主な項目:

- `task1`: **Chart Classification**
  - 例: `chart_type: "vertical bar"`
- `task2`: **Text Detection and Recognition**
  - OCR テキストと polygon
- `task3`: **Text Role Classification**
  - tick_label / legend_label などの役割
- `task4`: **Axes Analysis**
  - x/y 軸、tick point、plot 領域
- `task5`: **Legend Analysis**
  - 凡例記号の bbox と対応ラベル
- `task6`: **Data Extraction**
  - 系列名ごとのデータ値
  - 棒・線・点など visual elements

つまり CHART-Info / UB-PMC はかなり豊富で、
- チャート種別
- OCR 結果
- テキストの役割
- 軸情報
- 凡例
- 最終的なデータ系列
- 視覚要素の位置

まで、段階的に注釈されています。

## すぐ見る方法

### ブラウザで一覧表示

`/project/datasets/index.html` を開く。

### シェルで確認

```bash
find /project/datasets -maxdepth 3 | sort
```

## 補足

- `LineEX/pred_data_0.png.json`
  - 線グラフの抽出点列が入っている
- `UB-PMC_CHART-Info/sample/UB_PMC_sample/*.json`
  - CHART-Info タスク形式の注釈 JSON
- ExcelChart400K は公開配布物が大きく、軽量な単発サンプル取得がしづらいので、今回は配布元確認と関連デモ保存に留めた
