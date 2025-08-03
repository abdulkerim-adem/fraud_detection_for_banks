# Fraud Detection Challenge – Week 8&9 (10 Academy AI Mastery)

## 📌 Project Overview
This project tackles **fraud detection** for both **e-commerce transactions** and **bank credit card transactions**.  
The goal is to build **accurate, interpretable, and business-friendly** models that can spot fraudulent activity while balancing customer experience.

We worked with **three datasets**:
- `Fraud_Data.csv` – e-commerce transactions with user, device, IP, and behavioral data.
- `IpAddress_to_Country.csv` – IP ranges mapped to countries.
- `creditcard.csv` – anonymized PCA-transformed credit card transaction data.

---

## 🏆 Business Context
Fraud detection is tricky because:
- Fraud cases are **rare** (extreme class imbalance).
- **False negatives** → direct financial loss.
- **False positives** → frustrated customers.

A good solution should:
1. Detect fraud accurately.
2. Minimize false alarms.
3. Explain its decisions for trust and compliance.

---

## 🛠 Workflow

### **1. Data Analysis & Preprocessing**
- **Cleaning:** Removed duplicates, fixed data types, handled missing values.
- **Geolocation:** Mapped IP addresses → countries using integer conversion and range joins.
- **Feature Engineering:**
    - `hour_of_day`, `day_of_week`, `time_since_signup`
    - User transaction velocity (count so far, time since last purchase)
    - Merged geolocation (`ip_country`)
- **EDA Highlights:**
    - Fraud often spikes during unusual hours/days.
    - Certain sources/browsers show higher fraud rates.
    - Some countries are overrepresented in fraud cases.

---

### **2. Modeling & Evaluation**
We compared:
- **Logistic Regression** – interpretable baseline.
- **XGBoost** – powerful tree-based ensemble.

**Pipeline Steps:**
1. **One-hot encoding** for categorical features.
2. **Scaling** for numeric features.
3. **SMOTE oversampling** (train set only) to address imbalance.
4. Model training & evaluation with:
    - **F1-score**
    - **Precision-Recall AUC (PR-AUC)**
    - Confusion Matrix

**Key Findings:**
- XGBoost consistently outperformed Logistic Regression on both datasets.
- SMOTE + XGBoost achieved the best recall while maintaining strong precision.

---

### **3. Model Explainability**
We used **SHAP** to explain the best models:
- **SHAP Summary Plot:** Global importance & effect of each feature.
- **SHAP Force Plot:** Local explanation for individual transactions.

**Insights:**
- High purchase value, short signup-to-purchase time, and unusual IP country were strong fraud indicators in e-commerce.
- In credit card data, certain PCA components (e.g., V17, V14) strongly influenced predictions.

### Install Dependencies
```bash
pip install -r requirements.txt
```