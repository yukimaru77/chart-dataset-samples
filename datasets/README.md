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
