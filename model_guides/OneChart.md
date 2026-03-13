# OneChart local setup notes

## Source
- Repo: https://github.com/LingyvKong/OneChart
- HF weights: https://huggingface.co/kppkkp/OneChart/tree/main
- Project page: https://onechartt.github.io/
- Paper: OneChart: Purify the Chart Structural Extraction via One Auxiliary Token (ACM MM 2024)

## Local directory
- Code: `/project/models/OneChart`

## Official install
Upstream reports CUDA 11.8 + torch 2.0.1.

```bash
cd /project/models/OneChart/OneChart_code
conda create -n onechart python=3.10 -y
conda activate onechart
pip install -e .
pip install -r requirements.txt
pip install ninja
```

## Quick HF-based inference snippet
```python
from transformers import AutoModel, AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained('kppkkp/OneChart', trust_remote_code=True, use_fast=False, padding_side="right")
model = AutoModel.from_pretrained('kppkkp/OneChart', trust_remote_code=True, low_cpu_mem_usage=True, device_map='cuda')
model = model.eval().cuda()

image_file = 'image.png'
res = model.chat(tokenizer, image_file, reliable_check=True)
print(res)
```

## Demo entrypoint from upstream repo
```bash
cd /project/models/OneChart/OneChart_code
python vary/demo/run_opt_v1.py --model-name /path/to/onechart_weights
```
Then select `1`, then provide the image path interactively.

## Local status in this workspace
- Repo cloned: **yes**
- Full environment + weights downloaded: **not executed yet**
- Why not fully executed: larger modern VLM stack, custom remote code / weights, and longer download time

## Example assets available locally
- `/project/models/OneChart/assets/append_all.png`
- `/project/models/OneChart/assets/logo.png`

## What OneChart returns
The model is designed to output a structured chart summary as a python-dict-like string, e.g. title / source / axis titles / values.

## Practical note
If you want, this is a good candidate for a dedicated GPU setup next, because the HF checkpoint path is publicly available and the repo gives a direct `model.chat(...)` interface.
