# Shipment Cost Prediction

## 📦 Project Overview
This project builds a predictive model to estimate **shipment delivery costs** based on package characteristics such as weight, dimensions, destination, and product type. The analysis demonstrates how data-driven modeling can support logistics companies in **pricing optimization, operational planning, and resource allocation**.

The project follows an end-to-end machine learning workflow, from exploratory data analysis (EDA) to feature engineering, model training, validation, and interpretation.

---

## 🎯 Problem Statement
Predict shipment delivery costs using package features (weight, dimensions, destination, and shipping-related attributes) to enable logistics organizations to:
- Improve pricing accuracy
- Anticipate high-cost shipments
- Optimize transportation and handling decisions
- Support scalable, data-driven cost estimation

---

## 📊 Dataset Description
- **Records:** 263,000+ shipments  
- **Target Variable:** `price` (shipment cost)
- **Key Features:**
  - Numeric: `weight`, `length`, `width`, `height`
  - Categorical: `destination_port`, `product_name`
  - Temporal: `shipment_date`

> ⚠️ The full dataset is not included in this repository due to size and privacy considerations.

---

## 🔍 Exploratory Data Analysis (EDA)

### Key Findings
- **Severe Right-Skewness:**  
  All numeric variables (price and dimensions) are heavily right-skewed, with most shipments being small and inexpensive, and a small number of extreme outliers.
- **Outliers in Price:**  
  Shipment prices range up to extremely high values, dominating the scale and requiring transformation.
- **Weak Linear Correlation:**  
  Physical dimensions alone have weak linear relationships with price, suggesting non-linear and categorical drivers.
- **Categorical Distribution:**  
  - Destination ports are evenly distributed across top locations.
  - Product names are high-variance and diverse, indicating heterogeneous shipment types.

---

## 🧹 Data Cleaning & Preprocessing
- Renamed columns for consistency and readability
- Converted `shipment_date` to datetime
- Dropped rows with missing shipment dates
- Imputed missing numeric values using robust statistics
- Filled missing categorical values with placeholders
- Created a new feature:
  - **Volume = length × width × height**

---

## 🛠️ Feature Engineering
- **Log Transformation** applied to:
  - `price`, `weight`, and `volume`
- Purpose:
  - Reduce skewness
  - Stabilize variance
  - Improve linear model performance
- Result:
  - Distributions became significantly more balanced
  - Outliers no longer dominated the loss function

---

## 🤖 Modeling Approach

### Data Splitting
The dataset was split into:
- **Training Set:** 60%
- **Validation Set:** 20%
- **Test Set:** 20%

This ensures reliable evaluation and guards against overfitting.

### Model
- **Baseline Model:** Linear Regression
- Implemented using a **Pipeline** with:
  - `StandardScaler` for numeric features
  - `OneHotEncoder` for categorical features
- This design prevents feature leakage and ensures reproducibility.

---

## 📈 Model Performance

| Dataset | R² Score | MAE | RMSE |
|-------|---------|-----|------|
| Train | ~0.95 | ~0.28 | ~0.38 |
| Validation | 0.9508 | 0.2871 | 0.3848 |
| Test | Comparable | Comparable | Comparable |

### Interpretation
- Strong generalization across train, validation, and test sets
- Minimal evidence of overfitting
- Log transformation significantly improved model stability

---

## 🔑 Feature Importance (Interpretability)
Using Linear Regression coefficients on log-transformed data:
- **Volume and Weight** are the strongest numeric predictors
- **Product type** (categorical features) plays a major role
- **Destination port** has limited influence on price

This suggests shipment cost is driven more by **what is shipped** and **how large it is**, rather than **where it is shipped**.

---

## 🌍 Real-World Application (Logistics Context)
This analysis demonstrates how a logistics company could:
- Provide **instant shipping cost estimates**
- Detect **high-cost shipments early**
- Improve **pricing fairness and consistency**
- Support **capacity and route planning**
- Enable scalable, automated cost modeling

The approach reflects real-world constraints such as skewed data, extreme outliers, and operational variability.

---



