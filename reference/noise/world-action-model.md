# World-Action Model (WAM) — CALVIN manipulation

- **Weight**: noise
- **Source**: `2603.28955v1.pdf` (7 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Yuci Han, Alper Yilmaz
- **arXiv**: 2603.28955 · **Benchmark**: CALVIN (robot manipulation)
- **Read status**: method + experiments read (2026-08-07)

## One-line summary

An action-regularized world model: adds an **inverse-dynamics head** to DreamerV2's RSSM latent world model, so representations capture action-relevant structure for downstream control.

## Core method

- RSSM (Recurrent State-Space Model) latent pathway: observations x_t encoded → posterior z_t regularized toward prior ẑ_t (KL); decoder reconstructs ẑ_t; reward estimator provides task-completion signals.
- **Inverse dynamics head**: ẑ_t = ψ([e_t; e_{t+1}]) — a 3-layer MLP predicting the action from consecutive encoder embeddings. The action head **cascades** action-aware structure through the full model (posterior → prior), unlike standard world models that treat actions only as conditioning inputs.
- Downstream: diffusion policy via behavioral cloning on world-model latents, then model-based PPO fine-tuning inside the frozen world model.

## Results

- Imagination quality: PSNR 22.10 vs 21.66, FVD 10.82 vs 12.13 (better rollouts than DreamerV2).
- Policy: behavioral cloning 59.4% → 71.2% average success (vs DreamerV2/DiWA baselines); after PPO fine-tuning 92.8% vs 79.8%.

## Why this is noise for WAM

Robotics/reinforcement-learning domain; no mechanism transfers to a human-AI collaboration framework. **Name collision only**: this paper's abbreviation is also WAM.

## 利用探讨 (how to use — minimal)

1. **Brand/search awareness** — when searching "WAM framework" or publishing, this arXiv paper (2603.28955) exists; prefer the full name "Wait a Minute" in citations if disambiguation matters.
2. Nothing else. Skimmed; no deep-read scheduled.

## 评估标准 / 研发路线

None. Recorded for collision awareness only.

## Related directions

none
