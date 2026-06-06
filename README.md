
# Telecom Churn Prediction
### End-to-end ML pipeline for customer retention intelligence

## Project Overview
Predicts which telecom customers will churn using XGBoost + SHAP explainability.
Built on the Cell2Cell dataset (51,047 customers, 58 features).

## Results
- XGBoost AUC-ROC: 0.675 (+6.1% over baseline)
- 16.7M DT annual revenue at risk identified
- 35x ROI on targeted retention calls

## Notebooks
## Notebooks

| Notebook | Description | Link |
|---|---|---|
| 01 — EDA | Exploratory Data Analysis | [Open](notebook01-eda.ipynb) |
| 02 — Segmentation | KMeans customer segmentation | [Open](notebook02.ipynb) |
| 03 — Churn Prediction | XGBoost + SHAP + Business Insights | [Open](notebokk03.ipynb) ||

## Tech Stack
Python · XGBoost · LightGBM · SHAP · Scikit-learn · Pandas · Matplotlib

## Business Value
See [business_value.md](business_value.md) for full ROI analysis and retention strategy.
