# 🚀 Fraud Detection System

## 📌 Overview

This project builds a **fraud detection system** for financial transactions using machine learning pipelines.

The primary goal is to achieve strong performance on a **highly imbalanced dataset** *(fraud rate ≈ 3.5%)*.

### 🔧 System Components

* Data processing pipeline with feature engineering
* Modeling pipeline using ensemble learning (**XGBoost + LightGBM**)

---

## 🏆 Dataset & Competition

This project is based on the **IEEE-CIS Fraud Detection** competition on Kaggle.

* 📊 Organized by: IEEE Computational Intelligence Society
* 🎯 Goal: Detect fraudulent financial transactions
* 📉 Challenge: Highly imbalanced dataset with complex anonymized features

The dataset includes:

* `train_transaction.csv`: Transaction-level data
* `train_identity.csv`: Identity-related information

➡️ Both datasets are merged using `TransactionID`.

---

## 📊 1. Data Processing

### 🔹 Data Sources

* Transaction data
* Identity data

---

## 🧠 2. Feature Engineering

### ⏱️ Time Features

* `Hour`: Extracted from `TransactionDT`
  → Fraud patterns vary across different hours

---

### 📦 Product Features

* `ProductCD_Risk`: Risk mapping *(Low / Medium / High)*
* `Amt_to_Mean_ProductCD`: Relative transaction amount
* `Amt_to_Std_ProductCD`: Standard deviation distance

---

### 💳 Card Features

* `card1–card5_risk`: Risk level based on fraud rate
* `card1–card5_freq`: Frequency encoding
* `card4_Amt_mean`, `card4_Amt_diff`: Amount deviation
* `card6_Credit`: Credit card flag *(higher risk)*

---

### 📍 Address Features

* `addr1_freq`, `addr2_freq`: Frequency encoding
* `addr1`, `addr2`: Raw address values

---

### 📧 Email Features

* `Email_Risk_Bin`: Domain risk classification
  *(e.g., protonmail, gmail, yahoo → higher risk)*
* `P_email_freq`, `R_email_freq`: Frequency encoding

---

### 🆔 UID Features

* `uid`: Combination of card, address, email, and day
* `TransactionAmt_diff_uid`: Deviation from user average
* `uid_count`: Number of transactions per user

---

## 🤖 3. Modeling

### 🔹 Models Used

* XGBoost
* LightGBM

### 🔹 Ensemble Strategy

* Weighted Averaging
* Optimization of:

  * Model weights
  * Classification threshold

---

## 📈 4. Evaluation

### 🔹 Data Split

* Train / Validation / Test = **80% / 10% / 10%**
* Stratified split to preserve class distribution

---

### 🔹 Metrics

* Accuracy
* Balanced Accuracy *(important for imbalance)*
* ROC-AUC
* Precision / Recall / F1-score
* Confusion Matrix

---

## ⚙️ 5. Optimization Strategy

### 🔍 Search Space

* **Weight**: 0 → 1.0 *(step = 0.05)*
* **Threshold**: 0.01 → 0.99 *(step = 0.01)*

### 🎯 Constraint

* Precision ≥ 0.6
* Maximize Recall

---

## 🏆 6. Results

### 🔹 ROC-AUC Scores

| Model           | AUC        |
| --------------- | ---------- |
| XGBoost         | 0.9794     |
| LightGBM        | 0.9795     |
| Ensemble (Meta) | **0.9809** |

---


## 🛠️ Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* XGBoost
* LightGBM

---

## 📬 Future Improvements

* Add SHAP for model interpretability
* Deploy as API (FastAPI / Flask)
* Real-time fraud detection pipeline
* Hyperparameter tuning with Optuna

---
