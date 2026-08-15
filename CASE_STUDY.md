# Wearable Health Telemetry — Johaan's Case Study

> My personal perspective on the project. The team story lives in the
> [main repo's CASE_STUDY.md](https://github.com/Rhythm360/telemetry-healthcare/blob/main/CASE_STUDY.md);
> the technical source of truth is the repo itself. **Synthetic data only. Not a medical device.**

## 1. Why this project

Health-adjacent ML is where inflated claims go to thrive: private data, unreproducible
numbers, and metrics that sound clinical but aren't. After research work under the guidance of
Professor Jevelson Simenthy (Penn State), I wanted a public version that inverted the usual
incentive — a study whose every number a stranger can reproduce from the shipped code, with
limitations stated before results.

## 2. The question I scoped

Can standard model families separate labeled patterns in synthetic wearable-style
cardiovascular signals (heart rate, HRV), and can the pipeline around them be engineered to
the standard I'd want to be judged by: leakage-safe, seeded, cross-validated, tested in CI,
and documented in a model card?

Deliberately *not* in scope: real patient data, clinical claims, or a polished product. The
iOS app and backend are applied extras that show the pipeline serving a client.

## 3. What I built

- **Synthetic data generation** designed to resemble Apple Watch / HealthKit signal
  characteristics — so the data's provenance is fully known and publishable
  ([DATA_ACCESS.md](https://github.com/Rhythm360/telemetry-healthcare/blob/main/DATA_ACCESS.md)
  explains why synthetic).
- **Feature engineering and four model families:** SVM soft-voting ensemble, gradient
  boosting, an MLP, and a random-forest/GBM/XGBoost regression ensemble.
- **Evaluation discipline:** stratified splits, 5-fold cross-validation, fixed seeds,
  macro-averaged metrics for the multiclass task, and `results/metrics.csv` as the single
  machine-readable source of truth.
- **Tests + CI:** a pytest suite over data processing and metric correctness, run on every
  push via GitHub Actions.
- **FastAPI backend** that loads the trained `.pkl` pipelines and serves them (WIP).
- **The documentation set:** model card, research notes (what worked / what didn't), and the
  sanitized architecture overview.

## 4. Results, with their asterisk

Verified from the shipped code (seed 42): 93.9% accuracy for the SVM ensemble on binary
rhythm, 99.4% for gradient boosting on binary health-risk, 99.0% for the MLP on 4-class HRV,
and regression R² of 0.918 (fitness), 0.563 (VO₂max), and 0.970 (cardiovascular age).

The asterisk, stated everywhere the numbers appear: the data is synthetic and separable by
design. High scores here measure whether the pipeline is correct, not whether the models
would survive contact with real physiology. VO₂max's mediocre R² is the honest tell — the
synthetic generator makes it genuinely harder, and I left that result in rather than tuning
it away.

## 5. Collaboration

[Yash Piratla](https://github.com/YashwanthPiratla) drove the app concept and built the
complete SwiftUI iOS front end — HealthKit integration and Core ML on-device inference — plus
the project's overall plan and architecture. We met at the backend contract: my models and
API on one side, his app experience on the other. His perspective is in his own case study.

## 6. What I'd do differently

- Start with the model card instead of writing it last — it sharpens scope before a single
  model trains.
- Pin the backend's dependencies from day one (unpinned floors later caused a two-week trail
  of stale security alerts).
- Budget real time for the applied layer: "applied extra" became "work-in-progress" because
  the study rightly took priority.

## 7. Links

- Main repo: [Rhythm360/telemetry-healthcare](https://github.com/Rhythm360/telemetry-healthcare)
- Team case study: [CASE_STUDY.md](https://github.com/Rhythm360/telemetry-healthcare/blob/main/CASE_STUDY.md)
- My other case studies: [Midnight](https://github.com/Johaan-Mannanal/midnight-product-case-study)
- Portfolio: [johaan.dev](https://johaan.dev)
