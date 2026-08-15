# Wearable Health Telemetry: My Case Study

[![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-lightgrey)](LICENSE)
![Type: documentation](https://img.shields.io/badge/type-documentation--only-blue)

My role-focused case study of the wearable health telemetry project — an exploratory ML study
on synthetic cardiovascular signals, wrapped in a full-stack demonstration. Unlike my
[Midnight case study](https://github.com/Johaan-Mannanal/midnight-product-case-study), the
source here is fully public: **[Rhthm360/telemetry-healthcare](https://github.com/Rhthm360/telemetry-healthcare)**.

> Team-voiced case study: [CASE_STUDY.md in the main repo](https://github.com/Rhthm360/telemetry-healthcare/blob/main/CASE_STUDY.md).
> **Synthetic data only. Not a medical device.**

## One-sentence description

An honest, reproducible study of whether standard ML models can classify labeled patterns in
synthetic wearable-style heart signals — every number reproducible from the shipped code.

## My role — AI model training and backend

Built with [Yash Piratla](https://github.com/YashwanthPiratla) (app concept, SwiftUI iOS front
end). My side of the split:

- **ML pipeline, end to end:** synthetic data generation, feature engineering, training,
  evaluation, and visualization (`src/`), with leakage-safe preprocessing, fixed seeds,
  5-fold cross-validation, and a pytest suite run in CI.
- **Model training and comparison:** an SVM soft-voting ensemble, gradient boosting, a neural
  network (MLP), and a random-forest/GBM/XGBoost regression ensemble.
- **FastAPI backend:** serves the trained pipelines with PostgreSQL persistence
  (work-in-progress applied extra).
- **Documentation:** model card, research notes, data-access rationale, verified metrics.

## Verified results (from the public repo)

Reproduced from the shipped code with seed 42 — source of truth is
[results/metrics.csv](https://github.com/Rhthm360/telemetry-healthcare/blob/main/results/metrics.csv):

| Model | Task | Headline |
|-------|------|----------|
| SVM ensemble | Binary rhythm | 93.9% accuracy, 0.987 ROC-AUC |
| Gradient boosting | Binary health-risk | 99.4% accuracy |
| Neural network (MLP) | 4-class HRV | 99.0% accuracy, 0.99 macro-F1 |
| Regression ensemble | Fitness / VO₂max / CV age | R² 0.918 / 0.563 / 0.970 |

Because the data is synthetic and separable by design, these results measure the pipeline,
not clinical performance — stated plainly in the
[model card](https://github.com/Rhthm360/telemetry-healthcare/blob/main/MODEL_CARD.md).

## Full story

[CASE_STUDY.md](CASE_STUDY.md) — the problem I set for myself, methodology choices,
what worked and what didn't, and what I'd do differently.

## Links

- **Main repo (public source):** [Rhthm360/telemetry-healthcare](https://github.com/Rhthm360/telemetry-healthcare)
- **My personal case study, in depth:** [CASE_STUDY.md](CASE_STUDY.md)
- **Portfolio:** [johaan.dev](https://johaan.dev)
