# Quantitative-Risk-Modeling-Project
# Credit Risk Modeling – German Credit (PD Prototype)

## 1. Project Overview

This project builds a simple **Probability of Default (PD)** prototype model using the classic German Credit dataset.  
The goal is to demonstrate an end-to-end **risk modeling workflow**:

- Data understanding & preprocessing
- Logistic regression–based PD modeling
- Model evaluation (ROC, AUC, KS)
- PD segmentation and calibration checks
- Simple stress testing
- Feature interpretation

This project is intended as a **learning / portfolio project**, not as a production-ready credit risk model.

---

## 2. Data

- Dataset: German Credit (UCI / Kaggle variant)
- Number of observations: ~1,000
- Target variable:  
  - `Creditability` = 1 → good customer  
  - `Creditability` = 0 → bad / defaulted customer
- Example features:
  - `Age`, `Job`, `Duration`, `Credit amount`
  - `Sex`, `Housing`, `Saving accounts`, `Checking account`
  - `Purpose` (car, education, furniture, etc.)

Some features are numeric, others are categorical text variables.

---

## 3. Methodology

### 3.1 Feature preprocessing

- Numeric features are passed through unchanged.
- Categorical features are encoded using **OneHotEncoder**.
- Preprocessing and modeling are combined into a single **sklearn Pipeline** to:
  - avoid data leakage,
  - ensure consistent transformations on train and test data,
  - and make the workflow easier to reproduce and deploy.

### 3.2 Model

- Model: **Logistic Regression**
- Objective: predict \( P(\text{good}) \), then convert to PD via  
  \[
  \text{PD} = 1 - P(\text{good})
  \]

Train/test split: 80% / 20%, stratified by `Creditability`.

---

## 4. Model Evaluation

- Metric: **ROC AUC** on the test set  
- ROC curve is plotted to visualize the model’s discriminatory power.
- A simple **PD segmentation** is performed:
  - predicted PDs are grouped into 5 buckets,
  - for each bucket, we compare:
    - average predicted PD vs.
    - observed default rate.

This checks whether higher predicted PD indeed corresponds to higher realized default rates.

---

## 5. Stress Testing

A simple scenario analysis is implemented:

- **Scenario**: increase `Credit amount` by +20% for all test customers  
- Recalculate PDs under the stressed scenario
- Compare:
  - baseline average PD vs.
  - stressed average PD

This illustrates how the portfolio PD reacts to a deterioration in credit conditions.

---

## 6. Feature Interpretation

- Extract logistic regression coefficients after preprocessing.
- Examine top features (by absolute coefficient value).
- Interpretation:
  - Positive coefficients → associated with higher \( P(\text{good}) \) (lower PD)
  - Negative coefficients → associated with higher PD

This helps understand which features drive credit risk in the model.

---

## 7. How to Run

```bash
# 1. Create and activate virtual environment (example)
python -m venv .venv
.\.venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Start Jupyter Lab
jupyter lab
