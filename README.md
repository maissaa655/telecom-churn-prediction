# 📡 Telecom Churn Prediction & Retention Engine
### End-to-end ML + LLM pipeline for customer retention intelligence
 
---
 
## 🎯 Project Overview
 
This project builds a complete data science pipeline that predicts which telecom customers will churn, explains why, and automatically generates personalized retention strategies using a Large Language Model (LLM).
 
Built on the **Cell2Cell dataset** (51,047 customers, 58 features) as a proof of concept for Tunisie Telecom.
 
---
 
## 📊 Results at a Glance
 
| Metric | Value |
|---|---|
| Dataset | 51,047 customers |
| Best Model | XGBoost |
| AUC-ROC | 0.675 (+6.1% over baseline) |
| Churners caught (threshold=0.4) | 2,422 / 2,942 (82%) |
| Annual revenue at risk identified | ~16.7M DT |
| Retention ROI | **35x** |
| Retention messages generated | 50 personalized per run |
 
---
 
## 📁 Notebooks
 
| # | Notebook | Description |
|---|---|---|
| 01 | [EDA](notebook01-eda.ipynb) | Exploratory Data Analysis — distributions, correlations, missing values |
| 02 | [Segmentation](notebook02.ipynb) | KMeans customer segmentation — 3 risk profiles identified |
| 03 | [Churn Prediction](notebokkk03.ipynb) | XGBoost + SHAP explainability + Business insights |
| 04 | [Retention Engine](notebook04.ipynb) | Groq LLM generates personalized retention messages per customer |
 
---
 
## 🔄 Pipeline Architecture
 
```
Raw Data (Cell2Cell)
      ↓
NB01 — EDA
      Understand distributions, missing values, churn patterns
      ↓
NB02 — Segmentation
      KMeans → 3 customer segments
      Saves: cell2cell_segmented.csv
      ↓
NB03 — Churn Prediction
      XGBoost + SHAP → churn probability per customer
      Business insights: revenue at risk, ROI, churn drivers
      Saves: cell2cell_churn_predictions.csv
             cell2cell_high_risk.csv
      ↓
NB04 — LLM Retention Engine
      Groq API (LLaMA 3.3 70B) → personalized retention strategy per customer
      Saves: cell2cell_retention_messages.csv
```
 
---
 
## 🤖 Tech Stack
 
| Category | Tools |
|---|---|
| Language | Python 3.12 |
| ML Models | XGBoost, LightGBM, Logistic Regression |
| Explainability | SHAP |
| Clustering | Scikit-learn KMeans |
| LLM | Groq API — LLaMA 3.3 70B |
| Data | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Platform | Kaggle Notebooks |
 
---
 
## 📋 Customer Segments
 
| Segment | Customers | Avg Churn Prob | Revenue at Risk | Main Driver |
|---|---|---|---|---|
| Heavy Users At Risk | 40,102 | 47.1% | 10.4M DT | Usage decline |
| Churning Dissatisfied | 9,219 | 42.8% | 5.5M DT | Old equipment |
| Low Engagement | 1,726 | 61.4% | 0.7M DT | Old equipment |
 
---
 
## 💼 Business Value
 
See [business_value.md](business_value.md) for the full ROI analysis, retention strategy, and implementation roadmap.
 
**Key insight:** Targeting only 10,607 high-risk customers with personalized retention calls yields a **35x ROI** — spending 106K DT to save 3.69M DT in annual revenue.
 
---
 
## 🚀 How to Run
 
1. Run **NB01** on the raw Cell2Cell dataset
2. Run **NB02** — saves `cell2cell_segmented.csv`
3. Run **NB03** — saves `cell2cell_high_risk.csv`
4. Add your **Groq API key** to Kaggle Secrets as `GROQ_API_KEY`
5. Run **NB04** — generates personalized retention messages
---
