---
title: "Fraud Detection in Banking Transactions (ASB)"
date: 2025-08-09
draft: false
summary: "End-to-end R + ML pipeline on 500k synthetic transactions…"
tags: ["analytics", "machine-learning", "banking", "R"]

project_url: "https://github.com/GitRajib1230/Project_ASB"
demo_url: ""

cover:
  image: "project-asb.png"
  relative: true
  alt: "ASB Fraud Detection Project"
  caption: "ASB Fraud Detection Project"
---


## Overview
We built a complete fraud detection pipeline in **R** to support ASB Bank. Using **500,000** synthetic transactions (May–July 2024), we engineered temporal/behavioral features and trained multiple models, optimizing for **recall** while controlling false negatives.

## Dataset
- 500k transactions • May–July 2024 • Synthetic ASB-like data  
- Target: `FraudLabel` (1/0)  
- Raw attributes: date/time, amount, type, location, balance, joint flag, device/agent, merchant class, age

## Feature Engineering
`hour`, `weekday`, `weekend_flag`, `time_flag`, `Time_of_Day`, `agent_cat`, `balance_cat`, `joint_cat`, `age_group`, `trans_cat` (+ one-hot encoding)

## Feature Selection
- **Chi-square** (categoricals): `agent_cat`, `joint_flag`, `trans_cat`, `hour`, `weekday`, `TransactionType`, …
- **t-tests** (continuous): `transaction amount`, `balance`, `age`  
All significant at *p* < 0.05.

## Models & Metrics
Compared **LightGBM** ✅ (best), XGBoost, Random Forest, Logistic Regression, KNN.  
Evaluated with **Accuracy, Recall, AUC, Precision, Specificity** (10-fold CV, class imbalance handled via **SMOTE**).

**Best model (LightGBM):**
- Accuracy: **78.4%**
- AUC: **87.1%**
- Recall: **75.9%**
- PPV: **8.3%** (impacted by imbalance)

### Confusion Matrix (LightGBM)
|                | Predicted Fraud | Predicted Non-Fraud |
|----------------|-----------------|---------------------|
| Actual Fraud   | **680**         | 2,627               |
| Actual Non-Fraud | 2,137         | 95,909              |

> PPV is low due to imbalance, but LightGBM captured the **highest fraud cases** with the **lowest false-negative rate**.

## Top Features
1. `TransactionAmount`
2. `Time_of_Day`
3. `Agent`
4. `Weekday`
5. `Age`

## Business Recommendations
1. **Protect elderly (65+)** — OTP + restrict late-night access  
2. **Education & alerts** — mid-week fraud summaries (esp. Wednesdays)  
3. **Geo-fencing & device profiling** — detect anomalous combos  
4. **Smart flagging** — review high-risk transactions instead of blanket blocks

## Repo & Artifacts
- Code & docs: **[GitHub Repo]({{< param project_url >}})**
- Reproducible analysis: `704_Group_26_R_Code.qmd`
- A2 poster: `Poster_Final_Group26.pdf`  
- Built with: `tidymodels`, `xgboost`, `lightgbm`, `bonsai`, `themis (SMOTE)`  

**Contributors:** Md Rajib Hossain, Dicky Samudra, Jiawei Xu, Taha Sameer  
*Academic project using synthetic data only.*

