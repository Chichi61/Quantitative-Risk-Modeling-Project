# Quantitative-Risk-Modeling-Project
# Credit Risk Modeling (PD Model) + Monitoring Dashboard
Self-initiated project for me to explore credit risk & model monitoring

## 1. Project Overview

This is a self-initiated learning project where I wanted to “taste” what credit risk modeling looks like in practice and get some intuition for how PD models, model validation, and monitoring workflows work in the real world.

The project covers a simple end-to-end pipeline:
- Exploratory data understanding
- Logistic regression–based PD modeling (a baseline Probability of Default (PD) model)
- Model validation (calibration, segmentation, PSI)
- PD segmentation and calibration checks
- Simple stress testing
- A small risk monitoring dashboard to track PD shifts and feature drif

It is not intended to be a production model, just my way of exploring risk analytics hands-on.

---

## 2. Data

- Dataset: German Credit (UCI / Kaggle variant)
- Number of observations: ~1,000
- Target variable:  
  - `Creditability` = 0 → good customer  
  - `Creditability` = 1 → bad / defaulted customer
- Example features:
  - `Age`, `Job`, `Duration`, `Credit amount`
  - `Sex`, `Housing`, `Saving accounts`, `Checking account`
  - `Purpose` (car, education, furniture, etc.)

Some features are numeric, others are categorical text variables.

---

## 3. Methodology

I experimented with two types of models:
- Logistic Regression (baseline PD model)
- Simple tree-based models to see how they compare
  
Preprocessing includes:
- One-hot encoding for categorical variables
- Standardization for numerical varaiables
- sklearn Pipeline to avoid leakage and ensure reproducibility

## 4. Model Evaluation

To get a feeling for how PD models are evaluated, I implemented:
- ROC / AUC
- PD segmentation (predicted PD buckets vs observed defaults)
- Calibration checks
- Stability check using PSI (train vs test, and over resampled scenarios)

This helped me understand how risk teams assess model performance beyond just accuracy.

---

## 5. Stress Testing

I added a tiny scenario test to see how PD reacts when conditions worsen:

- **Scenario**: increase `Credit amount` by +20% for all test customers  
- Recalculate PDs under the stressed scenario
- Compare:
  - baseline average PD vs.
  - stressed average PD

This is only a simple example, but it helped me visualize how portfolio risk can shift under stress.

---

## 6. Monitoring Dashboard

To explore model monitoring concepts, I built a small dashboard that tracks:
- PD distribution over time
- Feature drift
- PSI for key variables
- Stress-scenario impacts

The dashboard is meant to mimic the kind of monitoring risk teams use after model deployment. So this part maybe the daily usual work of a risk anlyst, I just want to have a little bit "taste" of that.


