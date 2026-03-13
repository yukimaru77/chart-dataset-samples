# line_analysis

グラフ／チャート関連データセットとモデル実験用ワークスペースです。

## 収録内容

### データセットサンプル
- LineEX
- ExcelChart400K（関連実装 DeepRule / ChartOCR デモ中心）
- UB-PMC / CHART-Info

保存先:
- `/project/datasets/LineEX`
- `/project/datasets/ExcelChart400K`
- `/project/datasets/UB-PMC_CHART-Info`
- 一覧ページ: `/project/datasets/index.html`
- 補足説明: `/project/datasets/README.md`

### モデル別ワークベンチ
- `/project/models/ChartOCR`
- `/project/models/Kato2022_chart-synthesizer`
- `/project/models/LineEX`
- `/project/models/LineFormer`
- `/project/models/DePlot`
- `/project/models/OneChart`
- `/project/models/ChartVSR`
- モデル一覧: `/project/models/README.md`
- 公開用モデルガイド: `/project/model_guides`
- 公開用実行例: `/project/model_examples`

各モデルディレクトリには `OPENCLAW_SETUP.md` を置き、以下を記録しています。
- 元論文 / 元リポジトリ
- 環境構築手順
- 実行方法
- ローカルでの再現状況
- 実行結果例 / サンプル出力の保存先

## 実行・確認手順

### データセット一覧
```bash
find /project/datasets -maxdepth 3 | sort
```

### モデル一覧
```bash
find /project/models -maxdepth 2 -name 'OPENCLAW_SETUP.md' -o -name 'README.md' | sort
```

### すぐ試せるもの

#### DePlot
```bash
bash /project/models/DePlot/run_demo.sh /project/datasets/ExcelChart400K/test.png
```

#### Kato 2022 chart synthesizer
```bash
bash /project/models/Kato2022_chart-synthesizer/run_demo.sh 2 /project/models/Kato2022_chart-synthesizer/generated_lines
```

## このワークスペースで追加したもの

- `datasets/index.html`
- `datasets/README.md`
- `datasets/LineEX/*`
- `datasets/ExcelChart400K/*`
- `datasets/UB-PMC_CHART-Info/*`
- データセットごとのアノテーション説明
- `models/*/OPENCLAW_SETUP.md`
- `models/README.md`
- `models/DePlot/run_deplot_demo.py`
- `models/DePlot/run_demo.sh`
- `models/Kato2022_chart-synthesizer/run_demo.sh`
- DePlot と Kato 2022 用の軽量ランタイム（`/project/model_runtimes/*`）

## 外部ソース

- LineEX repo: https://github.com/Shiva-sankaran/LineEX
- CHART-Info tools/data: https://chartinfo.github.io/toolsanddata.html
- DeepRule repo: https://github.com/soap117/DeepRule
- ChartOCR repo: https://github.com/zmykevin/ChartOCR
- LineFormer repo: https://github.com/TheJaeLal/LineFormer
- OneChart repo: https://github.com/LingyvKong/OneChart
- DePlot upstream: https://github.com/google-research/google-research/tree/master/deplot
- DeepRuleDataset mirror: https://huggingface.co/datasets/asbljy/DeepRuleDataset/tree/main

## GPU / CUDA assumptions

- このマシンでは NVIDIA GPU が見えている
- ただし全モデルを同一環境で一気に入れるのではなく、モデルごとに分離したセットアップを推奨
- 実際にこのワークスペースで軽量に検証済みなのは:
  - DePlot: CPU/HF 経由で実行済み
  - Kato 2022 chart synthesizer: uv 環境で実行済み
- 強く CUDA 依存なもの:
  - ChartOCR
  - LineFormer
  - OneChart
  - （将来コード公開時の）ChartVSR

## 既知の制限

- ExcelChart400K 本体は公開物が multi-GB 級で、軽量に数件だけ抜き出す導線が弱い
- ChartOCR / LineFormer / OneChart は重い依存や追加 checkpoint が必要
- ChartVSR は確認時点で参照されていた公開 GitHub リポジトリが利用不可で、ローカル再現は未着手
- Kato 2022 については公開リポジトリが主に synthesizer 側であり、論文本体の parser 実装そのものではない
