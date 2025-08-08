# 🍽️ Restaurant Recommendation Engine – Soulpage IT Solutions Assignment

## 📌 Overview
This project was completed as part of my **Data Science internship interview assignment** with **Soulpage IT Solutions**.

The goal was to build a **recommendation engine** that predicts which restaurants customers are most likely to order from, based on:
- **Customer location(s)**
- **Restaurant information**
- **Customer order history**

The work included:
- **Data understanding & exploratory analysis**
- **Feature engineering**
- **Baseline model training**
- **Cross-validation & model selection**
- **Hyperparameter tuning with Optuna**
- **Final model evaluation**

---

## 📂 Dataset Description
The dataset contained information about customers, their locations, order histories, and vendor details.

**Key tables included:**
| Table       | Description |
|-------------|-------------|
| **Customers** | Demographic and account details |
| **Locations** | Multiple possible delivery points per customer (masked geocoordinates) |
| **Orders**    | Transaction history with order details, vendor ratings, and delivery metrics |
| **Vendors**   | Restaurant details, tags, and (masked) geolocation |

> 📄 See [Variable Definitions](VariableDefinitions.pdf) for a full column breakdown.

---

## 🔍 Approach

### **1️⃣ Data Exploration & Cleaning**
- Removed irrelevant features and handled missing values.
- Analyzed geolocation proximity despite masked coordinates.
- Joined **Customers**, **Locations**, **Orders**, and **Vendors** into a single training dataset.

### **2️⃣ Feature Engineering**
- Encoded categorical features (vendor tags, location type, etc.).
- Created aggregate statistics per customer (frequency, recency, favorite vendors).
- Engineered geospatial features based on masked latitude/longitude.

### **3️⃣ Modeling & Evaluation**
- Baseline models: **Random Forest** and **LightGBM**
- Evaluation: **Stratified K-Fold (5 folds)**
- Metrics: **AUC**, **Precision**, **Recall**, **F1-Score**

---

## 📊 Model Performance Comparison

| Model Variant                         | AUC     | Precision | Recall  | F1-Score |
|---------------------------------------|---------|-----------|---------|----------|
| **Random Forest (Baseline)**          | 0.8847  | 0.7759    | 0.5301  | 0.6299   |
| **LightGBM (Baseline)**               | 0.9088  | 0.7746    | 0.6307  | 0.6952   |
| **LightGBM (5-Fold OOF)**              | 0.9135  | 0.7960    | 0.7256  | 0.7591   |
| **LightGBM (Optuna Tuned – Final)** 🏆 | **0.9308** | **0.7994** | **0.8076** | **0.8035** |

---

## 🏆 Final Model – Optuna Best Hyperparameters

The final model selected was **LightGBM tuned with Optuna** to maximize **F1-score**.

**Best Trial:**
- **F1-Score:** `0.8006`
- **Hyperparameters:**
```python
{
  'learning_rate': 0.09770743989680095,
  'num_leaves': 87,
  'max_depth': 10,
  'colsample_bytree': 0.972686471143885,
  'subsample': 0.707145188107552,
  'reg_alpha': 0.6061466743895735,
  'reg_lambda': 0.0590723910015536
}
```

