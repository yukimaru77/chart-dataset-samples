# DePlot local setup notes

## Source
- Upstream README: https://github.com/google-research/google-research/tree/master/deplot
- HF model: https://huggingface.co/google/deplot
- Paper: DePlot: One-shot visual language reasoning by plot-to-table translation

## Local directory
- Wrapper files: `/project/models/DePlot`
- Local runtime: `/project/model_runtimes/deplot/.venv`

## Local setup actually performed here
A lightweight uv runtime was created and DePlot inference was executed locally.

```bash
mkdir -p /project/model_runtimes/deplot
cd /project/model_runtimes/deplot
uv venv
. .venv/bin/activate
uv pip install transformers torch pillow sentencepiece accelerate
```

## Verified demo script
File created locally:
- `/project/models/DePlot/run_deplot_demo.py`

Run with:
```bash
. /project/model_runtimes/deplot/.venv/bin/activate
python /project/models/DePlot/run_deplot_demo.py /project/datasets/ExcelChart400K/test.png
```

## Verified example output
Saved locally:
- raw: `/project/models/DePlot/demo_output.txt`
- cleaned: `/project/models/DePlot/demo_output_pretty.txt`

Example output obtained in this workspace:
```text
TITLE |
 | Series1 | Series2
1 | 0 | 0
2 | 0 | 0
3 | 0 | 0
4 | 0 | 0
5 | 0 | 0
6 | 0 | 0
7 | 0 | 0
8 | 0 | 0
9 | 0 | 0
10 | 0 | 1
11 | 1 | 1
```

## Notes
- DePlot is often the easiest chart-to-table baseline to run today.
- It is convenient through Hugging Face even without cloning the original google-research monorepo.
- For a full official demo UI, upstream also supports the pix2struct demo path.
