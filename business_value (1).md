# Business Value — Telecom Churn Prediction & Retention Engine
## End-to-End ML + LLM Pipeline for Customer Retention Intelligence

---

## 1. Problem Statement

Tunisie Telecom loses a significant portion of its customer base every year to churn. The traditional approach — calling customers randomly or waiting until they request cancellation — is costly and ineffective. This project addresses that gap by building a **data-driven early warning system** that identifies at-risk customers before they leave and automatically generates personalized retention strategies.

---

## 2. What We Built

A 4-notebook end-to-end pipeline:

| Notebook | What it does | Business output |
|---|---|---|
| NB01 — EDA | Analyses 51,047 customers across 58 features | Understanding of churn patterns |
| NB02 — Segmentation | Groups customers into 3 risk profiles | Targeted segment strategy |
| NB03 — Churn Prediction | Predicts churn probability + explains why | Revenue at risk, ROI, churn drivers |
| NB04 — Retention Engine | LLM generates personalized retention messages | Ready-to-use agent scripts per customer |

---

## 3. Model Performance

| Model | AUC-ROC | Churn Recall | vs Baseline |
|---|---|---|---|
| Logistic Regression (baseline) | 0.614 | 59% | — |
| XGBoost (final model) | 0.675 | 63% | +6.1% |
| At threshold = 0.4 | 0.675 | **82%** | catches 566 more churners |

**Cross-validation:** Mean AUC = 0.666 ± 0.004 across 5 folds — model is stable and not overfitting.

---

## 4. Customer Segmentation

Three distinct customer segments identified with different churn profiles:

| Segment | Customers | Avg Churn Probability | Annual Revenue at Risk |
|---|---|---|---|
| Heavy Users At Risk | 40,102 | 47.1% | **10,455,614 DT** |
| Churning Dissatisfied Customers | 9,219 | 42.8% | 5,509,092 DT |
| Low Engagement Customers | 1,726 | 61.4% | 738,143 DT |

**Total annual revenue at risk: ~16.7 million DT**

---

## 5. Why Each Segment Churns

### Segment 0 — Heavy Users At Risk
**Main churn driver: `PercChangeMinutes` — usage declining month over month**

These customers are progressively reducing their usage. The decline in minutes is an early disengagement signal — they are mentally leaving before formally churning.

**Retention strategy:**
- Monitor monthly usage drops as an early alert trigger
- Intervene when usage drops >30% vs previous month
- Offer: usage bonus, loyalty reward, or plan upgrade
- Message: *"We noticed you're using less — here's a better plan for you"*

---

### Segment 1 — Churning Dissatisfied Customers
**Main churn driver: `CurrentEquipmentDays` — old device, no upgrade path**

These customers have old devices and are not being offered upgrade paths. Equipment age signals unmet expectations — the customer wants a new phone but their contract doesn't provide one.

**Retention strategy:**
- Device upgrade program for customers with equipment > 700 days old
- Early upgrade eligibility as a loyalty reward
- Partner with device manufacturers for exclusive subscriber deals
- Message: *"As a valued customer, you qualify for an early device upgrade"*

---

### Segment 2 — Low Engagement Customers
**Main churn driver: `CurrentEquipmentDays` — old device + low engagement**

Similar to Segment 1 but with much lower overall engagement. These customers barely use the service and have old equipment — likely already found an alternative.

**Retention strategy:**
- Re-engagement campaign: data bonus, free minutes, or entertainment bundle
- Device upgrade offer combined with a simplified lower-cost plan
- If unresponsive, offer graceful downgrade rather than accepting full churn
- Message: *"We miss you — here's an exclusive offer to stay connected"*

---

## 6. LLM Retention Engine (Notebook 04)

The most innovative component of the pipeline. After identifying high-risk customers, the system automatically generates a **personalized retention strategy** for each one using the Groq API (LLaMA 3.3 70B).

### What the LLM produces for each customer

For every high-risk customer, the model generates a 4-part retention strategy:

```
1. SITUATION  — why this specific customer is at risk (1 sentence)
2. OFFER      — one tailored retention offer (1 sentence)
3. MESSAGE    — what the agent says when calling (2 sentences)
4. URGENCY    — how soon to contact and why (1 sentence)
```

### Why this matters

Without the LLM, the retention team uses generic scripts:
*"We'd like to offer you a 10% discount to stay."*

With the LLM, every call is personalized:
*"Mr. X, we noticed your usage dropped significantly last month — we'd like to offer you a data bonus and network quality guarantee before your renewal date."*

**Personalized offers have 2–3x higher acceptance rates than generic ones.**

---

## 7. Retention ROI

### Investment vs Return

| Metric | Value |
|---|---|
| High-risk customers identified | 10,607 |
| Cost of retention calls (10 DT/call) | 106,070 DT |
| Revenue saved if 50% of calls succeed | 3,694,403 DT |
| **Net gain** | **3,588,333 DT** |
| **ROI** | **35x** |

**For every 10 DT spent on a targeted retention call, the business recovers 350 DT in saved annual revenue.**

### Targeted vs Random Outreach

| Approach | Calls needed | Cost | Churners caught |
|---|---|---|---|
| Random (no model) | 51,047 | 510,470 DT | ~14,711 (all) |
| Model threshold 0.5 | ~4,600 | 46,000 DT | 1,856 |
| **Model threshold 0.4** | **~6,900** | **69,000 DT** | **2,422** ✅ |
| Model threshold 0.2 | ~9,700 | 97,000 DT | 2,911 |

**Threshold 0.4 is the optimal balance** — catches 82% of churners at 86% less cost than calling everyone.

---

## 8. Threshold Strategy

| Threshold | Churners Caught | Precision | Recommended For |
|---|---|---|---|
| 0.2 | 2,911 / 2,942 (99%) | 0.30 | Maximum recall campaigns |
| 0.4 | 2,422 / 2,942 (82%) | 0.35 | **Standard operations** ✅ |
| 0.5 | 1,856 / 2,942 (63%) | 0.41 | Budget-constrained periods |
| 0.6 | 991 / 2,942 (34%) | 0.48 | Very high-value customers only |

**Recommendation:** use threshold 0.4 for standard monthly campaigns. Lower to 0.3 during high-churn seasons (competitor promotions, contract renewal periods).

---

## 9. Implementation Roadmap

### Phase 1 — Immediate (Month 1)
- Deploy model on current Tunisie Telecom customer base
- Generate monthly high-risk customer list for retention team
- Deploy LLM retention engine — auto-generate scripts before each campaign
- Pilot segment-specific offers for each of the 3 segments

### Phase 2 — Short Term (Month 2–3)
- Integrate model output into CRM system
- Set up automated alerts when `PercChangeMinutes` drops >30% month-over-month
- Build equipment age dashboard: flag customers with device > 700 days old
- A/B test LLM-generated messages vs standard scripts to measure lift

### Phase 3 — Long Term (Month 4–6)
- Retrain model monthly on fresh Tunisie Telecom data
- Refine ROI calculation based on real retention outcomes
- Expand pipeline to include NPS scores and network quality metrics
- Scale LLM engine to full high-risk population (currently sampled at 50)

---

## 10. Key Takeaways

1. **The model works** — AUC 0.675, stable across 5-fold CV (std=0.004), catches 82% of churners
2. **Revenue at risk is quantified** — 16.7M DT annually, concentrated in Heavy Users
3. **Root causes are identified** — usage decline and equipment age drive most churn
4. **ROI is clear** — 35x return on targeted retention investment vs random calling
5. **Actions are personalized** — LLM generates specific offer + message per customer per segment
6. **Pipeline is scalable** — runs end-to-end automatically from raw data to retention scripts

---

## 11. Limitations & Next Steps

| Limitation | Mitigation |
|---|---|
| Dataset is US telecom (Cell2Cell) | Retrain on Tunisie Telecom data for local accuracy |
| 50% retention success rate assumed | Measure actual save rate and update ROI model |
| No competitor data included | Add market context if available |
| LLM sampled at 50 customers | Scale to full high-risk population with batching |
| No NPS or satisfaction scores | Integrate customer satisfaction data in next version |
| Static model | Schedule monthly retraining as customer behavior evolves |

---

*Built with XGBoost + SHAP + Groq LLaMA 3.3 70B | Dataset: Cell2Cell (51,047 customers) | Model AUC: 0.675 | Pipeline: 4 notebooks end-to-end*
