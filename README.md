# 🔥 NASA Global Wildfire Insights

End-to-end data science on NASA FIRMS (2024): from EDA and classification to a new **weekly spatio-temporal forecasting** layer that predicts short-term fire activity on a simple lat/lon grid.


---

## 📌 Objectives

- Analyze global fire detections in 2024 using MODIS satellite data.
- Uncover spatio-temporal patterns in wildfire activity.
- Assess fire intensity and confidence levels.
- Build classification models to predict fire confidence.
- Apply dimensionality reduction (PCA, t-SNE) to explore class separability.
- Use KMeans clustering to identify latent groupings in fire events.

---

## 📊 Methodology

- **Data Preprocessing**: Cleaned, encoded, and sampled over 100,000 fire records.
- **Supervised Learning**: Trained a `RandomForestClassifier` to predict fire confidence class.
- **Dimensionality Reduction**: Applied `PCA` and `t-SNE` to visualize separability.
- **Clustering**: Used `KMeans` in embedded spaces to explore natural groupings.
- **Evaluation**: Assessed models via precision/recall/F1-score and adjusted Rand index.

---

## ✅ Key Insights

- Some satellite features show clear correlation with fire confidence.
- The Random Forest model achieved meaningful classification performance.
- PCA and t-SNE revealed overlap between fire classes, hinting at complexity in feature space.
- Clustering yielded low alignment with true classes — showing unsupervised learning alone may not capture fire confidence without supervision.

---

## ✨ What’s new (Forecasting layer)

We added a full forecasting pipeline that:

- Aggregates point detections → **weekly counts per 0.25° lat/lon bin**
- Builds time-series features: **lags** (1 week), **rolling sums** (4 weeks), **weekly seasonality** (sin/cos)
- Compares models:
  - **ARIMA(2,1,2)** baseline on the global weekly series (train/test split aligned to Mondays)
  - **Prophet** (weekly seasonality)
  - **XGBoost** on spatio-temporal features (per-cell), then **sum over cells** for global curves
  - **Bias correction** (remove mean error on validation), and a **log-target variant** (+ optional bias)
- Reconciles global scale: **match XGB totals to ARIMA trend** for consistent totals
- Evaluates with **MAE / RMSE / SMAPE** + saves a **metrics table** and **Parquet forecasts**
---
### 📘 The forecasting notebook

- Reads raw FIRMS CSV and builds `data/processed/firms_weekly.parquet`
- Engineers features (`lag1`, `lag4_sum`, `w_sin`, `w_cos`)
- Splits **80% train / 20% test** by week (time-aware); inside train keeps last **10%** for validation
- Trains **ARIMA**, **Prophet**, **XGBoost** (+ tuned and **log-target** variants)
- Applies **bias correction** and (optional) **ARIMA reconciliation**
- Plots **global curves** (sum over cells) and writes:
  - model metrics → `data/processed/metrics.csv`
  - forecast curves → `data/processed/forecast_*.parquet`

---

### 📈 What the Results Show

- **ARIMA:** smooth short-term baseline; residual diagnostics included (QQ/ACF/Ljung–Box).
- **Prophet:** captures weekly seasonality but trended down for late season in this dataset.
- **XGBoost:**
  - Strong on **RMSE** after simple **bias correction**.
  - **Log-target** training can improve **MAE** but may over-predict (explicit bias term shown).
  - Feature importance confirms seasonality + recent lags are most useful.
