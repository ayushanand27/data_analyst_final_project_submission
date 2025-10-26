# Telecom Customer Churn Analysis – Project Report

## Abstract
This project develops a data-driven approach to predict telecom customer churn, explain key drivers, and recommend targeted retention strategies. Using six months of synthetic customer interactions (usage, recharges, complaints, and payments), we trained classification models and produced actionable insights and segments to guide win-back and loyalty initiatives.

## Introduction & Objectives
Customer churn erodes revenue and raises acquisition costs. The objectives were to:
- Predict churn propensity for each customer using recent interaction history.
- Explain the drivers of risk so stakeholders can build trust and take action.
- Segment customers into actionable cohorts with clear playbooks.

Success criteria included a robust ranking metric (ROC-AUC), interpretable drivers (SHAP/ELI5), and deliverables that are straightforward to operationalize (scored CSV, PPT, concise report).

## Tools Used
- Languages & Libraries: Python (pandas, numpy, scikit-learn, xgboost, seaborn, matplotlib, shap, eli5)
- Notebooks & Reporting: JupyterLab, python-pptx
- Artifacts: metrics_summary.json, scored CSV with churn_prob & segment, visuals (ROC/CM/SHAP), PPT report

## Steps Involved in Building the Project
1. Data Generation & Preparation
   - Created a synthetic but realistic dataset for 10,000 customers with 6 months of interactions (calls, recharges, complaints, payments) and demographics.
   - Feature engineering:
     - Recency features: days since last call/recharge/complaint/bill.
     - Behavior: recharge_txn_count, avg_recharge_amount, on_time_pay_ratio (postpaid).
     - Trends: usage_trend (slope of monthly minutes); complaint_intensity; recharge_consistency (CV).
     - Patterns: roaming ratio, weekend ratio, peak-hour usage.
   - Cleaned types and missing values; ensured reproducibility with fixed seeds.
2. Modeling & Validation
   - Trained RandomForest, LogisticRegression (best), and optional XGBoost.
   - Validation: Stratified K-fold; hyperparameters tuned via GridSearchCV.
   - Primary metric: ROC-AUC; also tracked F1 and Accuracy for operating-point context.
3. Explainability & Insights
   - SHAP to quantify global and local feature importance; ELI5 for weight-level clarity.
   - Visuals: SHAP summary bars; ROC curve; confusion matrix.
4. Segmentation & Targeting
   - Computed churn_prob for each customer using the best model.
   - Segmented into At Risk, Loyal, Dormant, Needs Attention using simple business rules.
5. Reporting & Deliverables
   - PPT for executives, scored CSV for activation, metrics JSON for governance, and this report.

## Results (Key Numbers)
- Best Model: LogisticRegression
- ROC-AUC: 0.655 | F1: 0.081 | Accuracy: 0.636
- Segment distribution (N = 10,000): At Risk 257 | Loyal 2,328 | Dormant 0 | Needs Attention 7,415

## Explainability (Drivers)
- Recency dominates: more days since last call/recharge increases churn risk.
- Recharge behavior: lower frequency and lower avg amounts increase risk; inconsistency matters.
- Complaints: recent complaints correlate with churn; prioritize recovery flows.
- Payments (postpaid): lower on_time_pay_ratio associates with churn; drive AutoPay.

## Segmentation & Business Actions
- At Risk (257): immediate win-back offers, complaint recovery SLAs, outreach via multi-channel nudges.
- Loyal (2,328): protect and upsell; loyalty boosters and referrals.
- Dormant (0 this run): normally reactivation offers and simplified pathways.
- Needs Attention (7,415): nurture and micro-campaigns; monitor migration to At Risk/Loyal.

## Limitations & Future Work
- Labels: This run used synthetic labels due to a single-class environment; replace with production churn outcomes for deployment.
- Thresholding: Tune operating thresholds to improve precision/recall for campaigns.
- Monitoring: Add drift, calibration, and fairness diagnostics; schedule retraining.
- Features: Incorporate network KPIs and digital engagement events for richer signals.

## How to Reproduce
1. Environment: create venv and `pip install -r requirements.txt`.
2. Notebook: run `notebooks/telecom_churn_prediction_full_v2.ipynb` (outputs in `outputs/`).
3. Script: `python scripts/generate_metrics.py` to regenerate metrics, visuals, and scored CSV.
4. PPT (optional): `python slides/report_template_generator.py --input outputs/metrics_summary.json --output outputs/Telecom_Churn_Report.pptx`.

## Conclusion
The solution identifies churn early using recent behavior and recency features, explains the drivers for stakeholder trust, and maps actions to segments. Operationalizing with real labels and CRM integration can reduce churn, improve ARPU, and enhance customer experience.
