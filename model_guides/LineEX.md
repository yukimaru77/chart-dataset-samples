# LineEX local setup notes

## Source
- Repo: https://github.com/Shiva-sankaran/LineEX
- Paper: LineEX: Data Extraction from Scientific Line Charts (WACV 2023)

## Local directory
- Code: `/project/models/LineEX`

## What this model does
LineEX is a 3-stage pipeline:
1. keypoint extraction
2. chart element detection + text extraction
3. grouping / legend mapping / datapoint scaling

## Official setup from upstream
```bash
cd /project/models/LineEX
conda env create -f environment.yml
conda activate LineEX
chmod +x download.sh
./download.sh -T False -V False -L True
```

This downloads weights and optionally train/val/test data.

## Pipeline run command
```bash
cd /project/models/LineEX
python pipeline.py --input_path=sample_input/
```

## Module-level commands
```bash
cd /project/models/LineEX/modules/KP_detection
python run.py

cd /project/models/LineEX/modules/CE_detection
python run.py

cd /project/models/LineEX/modules/Grouping_legend_mapping
python eval.py
```

## Local status in this workspace
- Repo cloned: **yes**
- Full environment created: **not fully materialized**
- Weights + test set download executed: **not executed yet**
- Sample inputs/outputs present in repo: **yes**

## Example result files available locally
- input: `/project/models/LineEX/sample_input/0.png`
- detection output: `/project/models/LineEX/sample_output/det_0.png`
- keypoints: `/project/models/LineEX/sample_output/kp_0.png`
- mapped result: `/project/models/LineEX/sample_output/mapped_0.png`
- extracted series JSON: `/project/models/LineEX/sample_output/pred_data_0.png.json`

## What the example JSON contains
`pred_data_0.png.json` stores extracted line series as lists of `(x, y)` points in image coordinates.

## Practical note
This is one of the more reproducible classic line-chart pipelines here, but it still depends on a legacy PyTorch stack from its `environment.yml`.
