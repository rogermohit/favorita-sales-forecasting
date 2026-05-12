# 🛒 Store Sales Forecasting — Favorita (Time Series Project)

This project builds an end-to-end machine learning pipeline to forecast daily product-family sales across more than 50 Favorita supermarket stores in Ecuador.

The work includes exploratory data analysis, feature engineering, classical time-series models, and a gradient-boosted tree model (XGBoost).  
The best performing model achieved **RMSLE = 0.3883** on the validation set.

---

## 📌 Project Goals
- Forecast daily sales for every **store–product family** combination  
- Engineer meaningful features from date, promotions, oil prices, holidays, and earthquake impact  
- Compare multiple forecasting approaches:
  - SARIMAX
  - Prophet
  - XGBoost  
- Evaluate models using **RMSLE (Root Mean Squared Logarithmic Error)**  

---

## 📂 Project Files
The repository includes all necessary files to reproduce the analysis:

| File | Description |
|------|-------------|
| **Sales_Forecasting.ipynb** | Full notebook with EDA, feature engineering, modeling, and test inference |
| **train.csv** | Historical sales data (store, family, date, sales, promo) |
| **test.csv** | Test data with future dates requiring prediction |
| **stores.csv** | Store metadata: city, state, type, cluster |
| **oil.csv** | Daily oil prices (Ecuador is oil-dependent) |
| **holidays_events.csv** | Holiday calendar including transferred/bridge holidays |
| **transactions.csv** | Daily store transaction counts |
| **xgboost_submission.csv** | Final predictions generated using the XGBoost model |
| **Readme.txt** | Original dataset description |

---

## 🧠 Feature Engineering Highlights
Key features created in the notebook include:

- **Lag features:** sales_lag_7, sales_lag_14, sales_lag_28  
- **Rolling window features:** 7/14/28-day rolling means  
- **Calendar features:** month, weekday, weekend flag  
- **Payday indicator:** 15th + end-of-month  
- **Holiday impact:** cleaned holiday flags considering transferred/bridge days  
- **Earthquake window:** flag for weeks after the 2016 Ecuador earthquake  
- **External data:** oil price (forward-filled and backward-filled)  
- **Store metadata:** city, state, type, cluster  

All features were built on **combined train + test**, then split back to avoid mismatch.

---

## 📈 Model Comparison

| Model | Notes | Performance (Val RMSLE) |
|-------|--------|--------------------------|
| **SARIMAX** | Classical time-series, run per store/family | Moderate (slower + less flexible) |
| **Prophet** | Handles seasonality & trends well | Moderate |
| **XGBoost** | Uses engineered time-series features | **0.3883 (Best)** |

> XGBoost performed best because it captures nonlinear patterns, store-family heterogeneity, and interactions between engineered features.

---

## Example Output

The notebook generates:

- Rolling feature visualizations
- Forecast plots from SARIMAX, Prophet, and XGBoost
- Test predictions saved as xgboost_submission.csv
- Daily sales forecast curve for the test period

## Notes on the Dataset

This project uses the Corporación Favorita Store Sales dataset, which includes:

- Promotions
- Government-adjusted holidays
- Earthquake effects
- Oil-driven economic fluctuations

These complexities make the forecasting task realistic and rich.
