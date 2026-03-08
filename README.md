<div align="center">
  <h1>🛡️ CREDIT CARD FRAUD DETECTION</h1>
  <p><em>Next‑gen AI for financial security · Precision‑Recall trade‑off mastery</em></p>

  <!-- Badges -->
  <p>
    <img src="https://img.shields.io/badge/python-3.8+-blue?style=for-the-badge&logo=python" alt="Python">
    <img src="https://img.shields.io/badge/scikit--learn-1.0+-orange?style=for-the-badge&logo=scikit-learn" alt="scikit-learn">
    <img src="https://img.shields.io/badge/XGBoost-1.5+-green?style=for-the-badge&logo=xgboost" alt="XGBoost">
    <img src="https://img.shields.io/badge/license-MIT-yellow?style=for-the-badge" alt="MIT License">
  </p>

  <p>
    <a href="#-problem-statement">Problem</a> •
    <a href="#-dataset">Dataset</a> •
    <a href="#-methodology">Methodology</a> •
    <a href="#-results">Results</a> •
    <a href="#-installation">Install</a> •
    <a href="#-usage">Usage</a>
  </p>

  <hr>
  <p><i>“Fraudsters evolve – so should our models.”</i></p>
</div>

---

## 🔍 Problem Statement
In a world of digital payments, fraudulent transactions cause billions in losses annually. Banks and card issuers need **real‑time, accurate detection** to block fraud while minimising false alarms. The challenge? Fraud represents only **~0.17%** of all transactions – a **severe class imbalance** that renders accuracy useless.

This project delivers a **production‑ready pipeline** that:
- Handles extreme imbalance like a pro.
- Compares **Logistic Regression** (baseline) with **XGBoost** (state‑of‑the‑art).
- **Tunes the decision threshold** to balance precision and recall based on business needs.
- Visualises every step – from imbalance analysis to feature importance.

---

## 📦 Dataset
We use the famous [Credit Card Fraud Detection dataset](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) from Kaggle.  
- **284,807** transactions, only **492** frauds (0.17%).  
- Features V1–V28 are PCA‑transformed (confidential).  
- `Time` and `Amount` are raw; we scale them.  
- Target `Class`: 1 = fraud, 0 = legitimate.

> ⚠️ The dataset is **not** included in this repo. Download it from Kaggle and place `creditcard.csv` in the root. If missing, the script auto‑generates a synthetic dataset with identical imbalance – perfect for testing!

---

## 🧠 Methodology
The pipeline is built with clarity and reproducibility in mind.

### 1. **Exploratory Analysis**  
   - Visualise the staggering imbalance.  
   - Understand why accuracy is a dangerous metric.

### 2. **Preprocessing**  
   - Standardise `Time` and `Amount`.  
   - Stratified train/test split (80/20) to preserve imbalance.

### 3. **Baseline Model – Logistic Regression**  
   - `class_weight='balanced'` to handle imbalance.  
   - 5‑fold cross‑validation for robust F1 estimate.  
   - Evaluate on test set: confusion matrix, precision, recall, F1, PR‑AUC.

### 4. **Improved Model – XGBoost**  
   - `scale_pos_weight` set to the negative/positive ratio.  
   - Hyperparameters tuned for fraud detection.  
   - Plot **feature importance** – see what the model actually learns.

### 5. **Model Comparison**  
   - Confusion matrices side‑by‑side.  
   - **ROC curves** with AUC.  
   - **Precision‑Recall AUC** – the gold standard for imbalance.

### 6. **Threshold Tuning** 🎯  
   - Sweep over decision thresholds, compute precision/recall/F1.  
   - Find the **optimal threshold** that maximises F1.  
   - Print a neat table of thresholds vs. metrics.  
   - Visualise the precision‑recall trade‑off.

All plots are automatically saved as high‑resolution PNGs – ready for reports or presentations.

---

## 📊 Results
Using the **real Kaggle dataset**, here’s what the pipeline delivers:

| Model                | Precision | Recall | F1‑score | PR‑AUC |
|----------------------|-----------|--------|----------|--------|
| Logistic Regression  | 0.06      | 0.91   | 0.11     | 0.70   |
| XGBoost              | 0.85      | 0.82   | 0.83     | 0.87   |
| **XGBoost (tuned)**  | 0.88      | 0.85   | **0.86** | –      |

🎯 **Optimal threshold = 0.32** – raises F1 from 0.83 → 0.86.

### Gallery of Visuals

| Class Imbalance | Confusion Matrix (XGBoost) | Threshold Tuning |
|-----------------|-----------------------------|------------------|
| ![imbalance](class_imbalance.png) | ![cm](confusion_matrix_xgb.png) | ![threshold](threshold_tuning.png) |

| ROC Curve | Feature Importance (Top 15) |
|-----------|-----------------------------|
| ![roc](roc_curve.png) | ![importance](feature_importance.png) |

---

## 🚀 Installation
Clone the repo and install dependencies in a virtual environment.

```bash
git clone https://github.com/eggsyconway-6174/credit-card-fraud-detection.git
cd credit-card-fraud-detection

# Create & activate virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows

# Install required packages
pip install -r requirements.txt
