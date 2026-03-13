# ChartOCR local setup notes

## Source
- Repo: https://github.com/zmykevin/ChartOCR
- Paper: ChartOCR: Data Extraction from Charts Images via a Deep Hybrid Framework (WACV 2021)

## Local directory
- Code: `/project/models/ChartOCR`

## What this model does
ChartOCR is an end-to-end chart parsing pipeline built around DeepRule / CornerNet-style detectors. It covers bar, line, pie, and chart component detection.

## Official environment from upstream
Upstream expects **conda + GPU + CUDA** and several compiled extensions.

### Official setup steps
```bash
cd /project/models/ChartOCR
conda create --name DeepRule --file DeepRule.txt
conda activate DeepRule

# compile repo NMS
cd /project/models/ChartOCR/external
make
```

### Extra upstream prerequisites
The upstream README also requires:
- CornerNet-Lite corner pooling compilation
- MS COCO API build
- downloaded chart datasets from Google Drive
- trained weights zip

### Batch inference entrypoint
```bash
cd /project/models/ChartOCR
python test_pipe_type_cloud.py --image_path <image_dir> --save_path <save_dir> --type <Bar|Line|Pie>
```

### Web UI entrypoint
```bash
cd /project/models/ChartOCR
python manage.py runserver 8800
```

## Local status in this workspace
- Repo cloned: **yes**
- Full CUDA env compiled: **not executed yet**
- Why not fully executed: very legacy stack, external compiled ops, upstream Azure OCR dependency note, and separate large weight/data downloads

## Example result files available locally
These are repo-provided demo artifacts you can inspect right now:
- `/project/models/ChartOCR/test.png`
- `/project/models/ChartOCR/target.png`
- `/project/models/ChartOCR/target_draw.png`
- `/project/models/ChartOCR/static/target.png`
- `/project/models/ChartOCR/static/target_draw.png`

## Annotation / output hints
From upstream README:
- pie: 3 critical points per sector `[edge1_x, edge1_y, edge2_x, edge2_y, center_x, center_y]`
- line: alternating xy data points `[d1_x, d1_y, ..., dn_x, dn_y]`
- bar: bar bounding boxes
- cls: component bounding boxes (plot area, title, legends, etc.)

## Practical note
If you want a modernized runnable version here, the fastest route is usually:
1. replace old OCR dependency with local OCR (PaddleOCR or Tesseract)
2. pin a compatible CUDA/PyTorch environment
3. download only line/bar checkpoints first
