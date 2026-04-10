📌 Overview

This project builds a fraud detection system for financial transactions using machine learning pipelines.
The primary goal is to achieve strong performance on a highly imbalanced dataset (fraud rate ≈ 3.5%).

The system consists of:

A data processing pipeline with feature engineering
A modeling pipeline using ensemble learning (XGBoost + LightGBM)
📊 1. Data Processing
🔹 Data Sources
train_transaction.csv: Main transaction data
train_identity.csv: User identity information

Both datasets are merged using TransactionID.

🔹 Feature Engineering
⏱️ Time Features
Hour: Extracted from TransactionDT
→ Fraud patterns vary across different hours of the day
📦 Product Features
ProductCD_Risk: Risk mapping (Low / Medium / High)
Amt_to_Mean_ProductCD: Transaction amount relative to product mean
Amt_to_Std_ProductCD: Standard deviation distance from product mean
💳 Card Features
card1–card5_risk: Risk level based on fraud rate
card1–card5_freq: Frequency encoding
card4_Amt_mean, card4_Amt_diff: Deviation from average amount
card6_Credit: Credit card flag (higher fraud risk)
📍 Address Features
addr1_freq, addr2_freq: Frequency encoding
addr1, addr2: Raw address values
📧 Email Features
Email_Risk_Bin: Domain risk classification (Low / Medium / High)
(e.g., protonmail, gmail, yahoo considered higher risk)
P_email_freq, R_email_freq: Frequency encoding
🆔 User ID (UID) Features
uid: Combination of card, address, email, and day
TransactionAmt_diff_uid: Deviation from user's average
uid_count: Number of transactions per user
🤖 2. Modeling
🔹 Models Used
XGBoost
LightGBM
🔹 Ensemble Strategy
Weighted averaging
Optimization of:
Model weights
Classification threshold
📈 3. Evaluation Metrics
🔹 Data Split
Train / Validation / Test = 80% / 10% / 10%
Stratified split to preserve class distribution
🔹 Metrics
Accuracy: Overall correctness
Balanced Accuracy: Important for imbalanced data
ROC-AUC: Model discrimination capability
Precision / Recall / F1-score
Confusion Matrix
⚙️ 4. Optimization Strategy
🔍 Hyperparameter Search
Weight search: 0 → 1.0 (step = 0.05)
Threshold search: 0.01 → 0.99 (step = 0.01)
🎯 Constraint
Precision ≥ 0.6
Maximize Recall
🏆 5. Results
🔹 ROC-AUC Scores
Model	AUC
XGBoost	0.9794
LightGBM	0.9795
Ensemble (Meta)	0.9809
