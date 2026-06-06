
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
| Notebook | Description |
|---|---|
| 01_EDA | Exploratory Data Analysis |
| 02_Segmentation | KMeans customer segmentation |
| 03_Churn_Prediction | XGBoost + SHAP + Business Insights |

## Tech Stack
Python · XGBoost · LightGBM · SHAP · Scikit-learn · Pandas · Matplotlib

## Business Value
See [business_value.md](business_value.md) for full ROI analysis and retention strategy.
