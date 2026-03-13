# ChartVSR local setup notes

## Source
- Paper / preprint: https://arxiv.org/abs/2602.16455
- Paper HTML mentions GitHub: `https://github.com/InternLM/VSR`

## Current reproducibility status
As checked in this workspace, the GitHub URL referenced from the paper did **not** resolve to a public repository at the time of setup.

That means there is currently **no verified public code release available here to clone and run**.

## What the paper says
ChartVSR is built on top of **Qwen2.5-VL-3B** and introduces a two-stage visual self-refinement process:
1. refine stage: predict pixel-level localizations
2. decode stage: use those localizations as visual anchors to decode final structured chart data

## Local directory
- Notes only: `/project/models/ChartVSR`

## Why no executable setup is included yet
- public repo path referenced in paper appears unavailable
- no validated checkpoint path was found during this setup pass

## Recommended next step when code appears
A likely future setup pattern will be:
- clone public repo
- create a fresh Python 3.10+ env
- install Qwen2.5-VL-compatible transformers / flash-attn stack as required by that repo
- download released ChartVSR weights

## Practical note
At the moment this model should be treated as **paper-tracked, not yet locally reproducible** in this workspace.
