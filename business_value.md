# Business Value — Churn Prediction Project
## Telecom Customer Retention Intelligence

---

## 1. Problem Statement

Tunisie Telecom loses a significant portion of its customer base every year to churn. The traditional approach to retention — calling customers randomly or waiting until they request cancellation — is both costly and ineffective. This project addresses that gap by building a **data-driven early warning system** that identifies at-risk customers before they leave.

---

## 2. What We Built

An end-to-end machine learning pipeline that:

- Analyses 51,047 customers across 58 behavioral and demographic features
- Segments customers into 3 distinct risk profiles
- Predicts individual churn probability for every customer
- Explains *why* each customer is at risk using SHAP
- Quantifies the financial impact of churn per segment
- Provides actionable retention recommendations per segment

---

## 3. Model Performance

| Model | AUC-ROC | Churn Recall | vs Baseline |
|---|---|---|---|
| Logistic Regression (baseline) | 0.614 | 59% | — |
| XGBoost (final model) | 0.675 | 63% | +6.1% |
| At threshold = 0.4 | 0.675 | 82% | catches 566 more churners |

**What AUC-ROC 0.675 means in practice:** the model correctly ranks a churner above a non-churner 67.5% of the time — significantly better than random guessing (50%) and better than any rule-based approach.

---

## 4. Customer Segmentation

Three distinct customer segments were identified, each with a different churn profile:

| Segment | Customers | Avg Churn Probability | Annual Revenue at Risk |
|---|---|---|---|
| Heavy Users At Risk | 40,102 | 47.1% | **10,455,614 DT** |
| Churning Dissatisfied Customers | 9,219 | 42.8% | 5,509,092 DT |
| Low Engagement Customers | 1,726 | 61.4% | 738,143 DT |

**Total annual revenue at risk: ~16.7 million DT**

---

## 5. Why Each Segment Churns

Understanding the root cause of churn per segment allows the retention team to make the right offer to the right customer — not a generic discount.

### Segment 0 — Heavy Users At Risk
**Main churn driver: `PercChangeMinutes`**

These customers are progressively reducing their usage month over month. The decline in minutes is an early disengagement signal — they are mentally leaving before they formally churn.

**Recommended retention action:**
- Monitor monthly usage drops as an early alert trigger
- Offer usage bonuses or loyalty rewards before usage drops below 50%
- Proactive outreach: "We noticed you're using less — here's a better plan for you"

---

### Segment 1 — Churning Dissatisfied Customers
**Main churn driver: `CurrentEquipmentDays`**

These customers have old devices and are not being offered upgrade paths. Equipment age is a strong signal of unmet expectations — the customer wants a new phone but their current contract doesn't provide one.

**Recommended retention action:**
- Device upgrade program: subsidised handset offers for customers with equipment > 700 days old
- Early upgrade eligibility as a loyalty reward
- Partner with device manufacturers for exclusive subscriber deals

---

### Segment 2 — Low Engagement Customers
**Main churn driver: `CurrentEquipmentDays`**

Similar to Segment 1 but with much lower overall engagement. These customers barely use the service and have old equipment — a combination that signals they have likely already found an alternative.

**Recommended retention action:**
- Re-engagement campaign: data bonus, free minutes, or entertainment bundle
- Device upgrade offer combined with a simplified, lower-cost plan
- If unresponsive to outreach, consider graceful downgrade rather than full churn

---

## 6. Retention ROI

### Investment vs Return

| Metric | Value |
|---|---|
| High-risk customers identified | 10,607 |
| Cost of retention calls (10 DT/call) | 106,070 DT |
| Revenue saved if 50% of calls succeed | 3,694,403 DT |
| **Net gain** | **3,588,333 DT** |
| **ROI** | **35x** |

**For every 10 DT spent on a targeted retention call, the business recovers 350 DT in saved annual revenue.**

### Why targeted outreach outperforms random calling

Without the model, the retention team would need to call all 51,047 customers to achieve similar coverage — at a cost of 510,470 DT and with a much lower success rate (most customers called would not have churned anyway).

With the model:
- Only 10,607 calls needed (79% reduction in call volume)
- Every call targets a customer with >60% predicted churn probability
- Higher agent success rate due to relevant, segment-specific offers

---

## 7. Threshold Strategy

The model outputs a churn probability for each customer. The **decision threshold** determines who receives a retention call.

| Threshold | Churners Caught | False Alarms | Recommended For |
|---|---|---|---|
| 0.2 | 2,911 / 2,942 (99%) | Very high | Maximum recall campaigns |
| 0.4 | 2,422 / 2,942 (82%) | Moderate | **Standard operations** ✅ |
| 0.5 | 1,856 / 2,942 (63%) | Low | Budget-constrained periods |

**Recommendation:** use threshold 0.4 for standard monthly retention campaigns. Lower to 0.3 during high-churn seasons (e.g. competitor promotional periods).

---

## 8. Implementation Roadmap

### Phase 1 — Immediate (Month 1)
- Deploy model on current customer base
- Generate monthly high-risk customer list for retention team
- Pilot segment-specific retention scripts for each of the 3 segments

### Phase 2 — Short Term (Month 2–3)
- Integrate model output into CRM system
- Set up automated alerts when `PercChangeMinutes` drops >30% month-over-month
- Build equipment age dashboard: flag all customers with `CurrentEquipmentDays` > 700

### Phase 3 — Long Term (Month 4–6)
- Retrain model monthly on fresh data
- A/B test retention offers per segment to measure actual save rate
- Refine ROI calculation based on real retention outcomes
- Expand pipeline to include NPS data and network quality metrics

---

## 9. Key Takeaways

1. **The model works** — AUC 0.675, confirmed stable across 5-fold cross-validation (std = 0.004)
2. **Revenue at risk is quantified** — 16.7M DT annually, concentrated in Heavy Users
3. **Root causes are identified** — usage decline and equipment age drive most churn
4. **ROI is clear** — 35x return on targeted retention investment
5. **Actions are specific** — different offer for each segment, not one-size-fits-all

---

## 10. Limitations & Next Steps

| Limitation | Mitigation |
|---|---|
| Dataset is US telecom (Cell2Cell) | Retrain on Tunisie Telecom data for local accuracy |
| 50% retention success rate assumed | Measure actual save rate and update ROI |
| No competitor data included | Add market context features if available |
| Static model | Schedule monthly retraining as customer behavior evolves |
| No NPS or satisfaction scores | Integrate customer satisfaction data in next version |

---

*Built with XGBoost + SHAP | Dataset: Cell2Cell (51,047 customers) | Model AUC: 0.675*
