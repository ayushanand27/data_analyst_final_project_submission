# Deliverables Package

This folder contains the core assets for submission (excluding the PPT you will upload separately).

## Contents
- telecom_churn_prediction_full_v2.ipynb — End-to-end notebook (data generation, modeling, evaluation, segmentation, artifacts)
- recommendations.md — Final business recommendations (playbooks and KPIs)
- telecom_customers_scored_segmented.csv — Scored customers with `churn_prob` and `segment`
- metrics_summary.json — Aggregated model metrics (best model + per-model)
- best_params.json — Best hyperparameters (if tuning used)
- confusion_matrix.png — Model confusion matrix image (if available)
- roc_curve.png — Model ROC curve image (if available)
- shap_summary_*.png — SHAP summary bars (if available)
- best_model.pkl — Serialized best model (if available)

## Overview
- Problem: Predict telecom customer churn, explain drivers, and propose targeted retention actions.
- Data: 10k customers with 6 months of synthetic interaction history (usage, recharges, complaints, payments) and demographics.
- Outputs: Best model metrics, driver insights (SHAP/ELI5), scored-and-segmented customers, and recommendations.

## Environment Setup
- Python: 3.10–3.13 recommended
- Create and activate a virtual environment (Windows PowerShell):
  - `python -m venv .venv`
  - `.\\.venv\\Scripts\\Activate.ps1`
- Install dependencies:
  - `pip install -r requirements.txt`

## Quickstart
- Open the notebook:
  - `jupyter lab notebooks/telecom_churn_prediction_full_v2.ipynb`
- Run all cells to regenerate artifacts into `outputs/`:
  - `metrics_summary.json` (metrics)
  - `telecom_customers_scored_segmented.csv` (scored customers + segments)
  - `confusion_matrix.png`, `roc_curve.png`, `shap_summary_*.png` (visuals)

## Reproduction Steps (script-based)
1. Ensure venv activated and dependencies installed.
2. Generate metrics and artifacts (optional alternative to notebook):
   - `python scripts/generate_metrics.py`
3. Regenerate PPT (if needed):
   - `python slides/report_template_generator.py --input outputs/metrics_summary.json --output outputs/Telecom_Churn_Report.pptx`

## Results & Metrics
- Best Model: LogisticRegression
- Metrics (test):
  - ROC-AUC: 0.655
  - F1: 0.081
  - Accuracy: 0.636
- Notes: ROC-AUC is robust to class imbalance and is the preferred headline metric. Accuracy may be inflated under imbalance; F1 improves with threshold tuning.

## Segments & Counts (N = 10,000)
- At Risk: 257
- Loyal: 2,328
- Dormant: 0
- Needs Attention: 7,415 (Value Growth 6,049 + Unassigned 1,366)
- Use cases:
  - At Risk → win-back and complaint recovery
  - Loyal → protect, reward, upsell
  - Needs Attention → micro-campaigns, nurture journeys

## Retention Playbooks (Summary)
- Immediate (0–30 days): win-backs for At Risk; fast-track complaint recovery; recharge nudges.
- 1–3 months: loyalty boosters, usage-based add-ons, hotspot reduction.
- 3–6 months: product evolution (bundles, sharing), predictive CRM triggers, VoC/NPS loop.
- KPIs: churn %, reactivation %, ARPU uplift, complaints %, NPS, on-time payment %, segment migration, ROI.

## Artifacts Map
- Notebook → notebook cells produce metrics, scored CSV, and visuals under `outputs/`.
- Scripts → `scripts/generate_metrics.py` (metrics, visuals, scored CSV), `scripts/md_to_pdf.py` (report PDF).
- Slides → `slides/report_template_generator.py` consumes `metrics_summary.json` and optional images to build PPT.

## Troubleshooting
- Activation fails in PowerShell → use: `.\\.venv\\Scripts\\Activate.ps1` and `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`.
- Import errors in notebook → first cell ensures `sys.path` includes project root.
- Missing metrics_summary.json → re-run notebook or `scripts/generate_metrics.py`.
- PPT save denied → close the PPT file and re-run the generator.

## Submission Checklist
- [ ] Notebook: `telecom_churn_prediction_full_v2.ipynb`
- [ ] Scored CSV: `telecom_customers_scored_segmented.csv`
- [ ] Metrics: `metrics_summary.json`
- [ ] Visuals (if present): `confusion_matrix.png`, `roc_curve.png`, `shap_summary_*.png`
- [ ] Recommendations: `recommendations.md`
- [ ] Project Report PDF: `Project_Report.pdf`
- [ ] PPT: upload your final PPT separately
