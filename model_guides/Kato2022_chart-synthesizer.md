# Kato 2022 local setup notes

## Source
- Repo: https://github.com/rakutentech/chart-synthesizer
- Paper: Parsing Line Chart Images Using Linear Programming (WACV 2022)

## Important scope note
The public repo here is the **chart synthesizer / dataset generator**, not the full released line-chart parser itself. It is still useful because it generates chart images plus JSON annotations used by the paper.

## Local directory
- Code: `/project/models/Kato2022_chart-synthesizer`
- Local runtime: `/project/model_runtimes/kato2022/.venv`

## Local setup actually performed here
A lightweight uv-based runtime was created and verified.

```bash
mkdir -p /project/model_runtimes/kato2022
cd /project/model_runtimes/kato2022
uv venv
. .venv/bin/activate
uv pip install numpy matplotlib opencv-python pillow scipy tqdm
```

Because the original project expects `wnjpn.db`, a tiny local compatibility SQLite file was created so generation can run in this workspace.

## Compatibility patch applied locally
For modern matplotlib, `plt.grid(b=...)` was updated to `plt.grid(visible=...)` in:
- `synthesize_line_charts.py`
- `synthesize_bar_charts.py`

## Verified run command
```bash
. /project/model_runtimes/kato2022/.venv/bin/activate
cd /project/models/Kato2022_chart-synthesizer
python synthesize_line_charts.py --num 2 --output /project/models/Kato2022_chart-synthesizer/generated_lines
```

## Verified output examples
Generated in this workspace:
- `/project/models/Kato2022_chart-synthesizer/generated_lines/line0.png`
- `/project/models/Kato2022_chart-synthesizer/generated_lines/line0.json`
- `/project/models/Kato2022_chart-synthesizer/generated_lines/line1.png`
- `/project/models/Kato2022_chart-synthesizer/generated_lines/line1.json`

## What the JSON contains
The generated line-chart JSON includes:
- title bbox and text
- x/y axis starts, ends, tick positions, tick label bboxes
- each line's point coordinates and corresponding numeric values
- legend icon + label
- line style and width

## Example snippet
See `generated_lines/line0.json`. It contains `data.lines[].points[]` entries with both pixel coordinates and decoded values.

## Caveat
This directory is a **reproducible data synthesizer setup**, not the full linear-programming parser implementation.
