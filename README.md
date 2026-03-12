# line_analysis

グラフ／チャート関連データセットの実サンプル確認用ワークスペース。

## 今回確認したデータセット

- LineEX
- ExcelChart400K（関連実装 DeepRule / ChartOCR のデモを取得）
- UB-PMC / CHART-Info

## 保存先

- `/project/datasets/LineEX`
- `/project/datasets/ExcelChart400K`
- `/project/datasets/UB-PMC_CHART-Info`
- 一覧ページ: `/project/datasets/index.html`
- 補足説明: `/project/datasets/README.md`

## 実行・確認手順

### ファイル一覧

```bash
find /project/datasets -maxdepth 3 | sort
```

### ブラウザ表示

ローカルで `file:///project/datasets/index.html` を開くか、OpenClaw browser で開く。

## 追加したもの

- `datasets/index.html`
- `datasets/README.md`
- `datasets/LineEX/*`
- `datasets/ExcelChart400K/*`
- `datasets/UB-PMC_CHART-Info/*`

## 外部ソース

- LineEX repo: https://github.com/Shiva-sankaran/LineEX
- CHART-Info tools/data: https://chartinfo.github.io/toolsanddata.html
- DeepRule repo: https://github.com/soap117/DeepRule
- ChartOCR repo: https://github.com/zmykevin/ChartOCR
- DeepRuleDataset mirror: https://huggingface.co/datasets/asbljy/DeepRuleDataset/tree/main

## GPU / CUDA assumptions

- この作業自体では GPU / CUDA は未使用
- ただし DeepRule / ChartOCR 系の学習・推論 README には GPU / CUDA 前提の記述あり

## 既知の制限

- ExcelChart400K 本体は公開物が multi-GB 級で、軽量に数件だけ抜き出す導線が弱い
- そのため ExcelChart400K は今回は関連実装リポジトリのデモ画像を保存
- UB-PMC / CHART-Info は公式 sample zip を展開して確認
- LineEX は公開リポジトリ同梱サンプルを使用
