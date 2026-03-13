# LineFormer local setup notes

## Source
- Repo: https://github.com/TheJaeLal/LineFormer
- Paper: LineFormer: Line Chart Data Extraction Using Instance Segmentation (ICDAR 2023)

## Local directory
- Code: `/project/models/LineFormer`

## Official install
Upstream uses MMDetection and reports testing on PyTorch 1.13.1 + CUDA 11.7.

```bash
cd /project/models/LineFormer
conda create -n LineFormer python=3.8
conda activate LineFormer
bash install.sh
```

`install.sh` performs:
- `pip install openmim`
- `conda install pytorch==1.13.1 torchvision==0.14.1 pytorch-cuda=11.7 -c pytorch -c nvidia`
- `mim install mmcv-full`
- `pip install -e mmdetection`
- extra utilities like `bresenham`, `tqdm`, `opencv-python`, `scikit-image`

## Inference pattern from upstream
```python
import infer
import cv2
import line_utils

img_path = "demo/PMC5959982___3_HTML.jpg"
img = cv2.imread(img_path)

CKPT = "iter_3000.pth"
CONFIG = "lineformer_swin_t_config.py"
DEVICE = "cpu"

infer.load_model(CONFIG, CKPT, DEVICE)
line_dataseries = infer.get_dataseries(img, to_clean=False)
img = line_utils.draw_lines(img, line_utils.points_to_array(line_dataseries))
cv2.imwrite('demo/sample_result.png', img)
```

## Checkpoint requirement
Upstream requires downloading a trained checkpoint separately from Google Drive.

## Local status in this workspace
- Repo cloned: **yes**
- Full MMDetection env installed: **not executed yet**
- Checkpoint downloaded: **not yet**
- Demo input/result images available: **yes**

## Example result files available locally
- input: `/project/models/LineFormer/demo/PMC5959982___3_HTML.jpg`
- result: `/project/models/LineFormer/demo/sample_result.png`

## Practical note
This is a strong line-chart extractor, but to make it fully runnable you need the exact checkpoint and an MMDetection-compatible env.
