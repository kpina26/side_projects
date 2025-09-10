# Sweet Lift Taxi Demand Prediction

## Overview
This project analyzes and forecasts **hourly taxi demand** using real-world order data from Sweet Lift Taxi.  
By processing and aggregating raw taxi order records, patterns in ride requests across hours of the day and days of the week were explored.  
The goal was to build and evaluate machine learning models capable of predicting the number of orders per hour, providing valuable insights for operational planning and service optimization.

---

## Project Workflow

### 1. Data Loading & Preprocessing
- Loaded dataset `taxi.csv` containing **datetime** and **num_orders** columns.
- Converted `datetime` column to datetime format and set it as the index.
- Resampled data to **hourly intervals** to aggregate total number of orders.
- Filled missing hourly values with zeros.

### 2. Exploratory Data Analysis (EDA)
- Computed descriptive statistics for hourly orders.
- Plotted:
  - **Hourly orders over time** with a 24-hour rolling mean.
  - **Average orders by hour of day** to identify peak and low demand hours.
  - **Average orders by weekday** to detect weekly demand patterns.

### 3. Feature Engineering
- Added **lag features** to capture demand patterns from previous hours: `lag_1`, `lag_2`, `lag_3`, `lag_24`.
- Added **rolling mean features**: 3-hour and 24-hour rolling averages.
- Created **weekend indicator** (`is_weekend`).
- One-hot encoded `weekday`.
- Dropped rows with NaN values caused by feature creation.

### 4. Model Training & Tuning
Tested models:
1. **Linear Regression**
2. **Random Forest Regressor**
3. **Gradient Boosting Regressor**
4. **XGBoost Regressor**
5. **LightGBM Regressor**
6. **CatBoost Regressor**

- Used **TimeSeriesSplit** for cross-validation.
- Applied **RandomizedSearchCV** for hyperparameter tuning where applicable.

### 5. Model Evaluation Metrics
- **RMSE** (Root Mean Squared Error) — lower is better.
- **MAE** (Mean Absolute Error) — for interpretability of average error in orders.

| Model              | RMSE     | MAE      |
|--------------------|----------|----------|
| Linear Regression  | 46.85    | 34.20    |
| Random Forest      | 45.85    | 34.21    |
| Gradient Boosting  | 45.89    | 34.16    |
| XGBoost            | 46.18    | 33.95    |
| LightGBM           | **43.19**| 33.94    |
| CatBoost           | 45.96    | 34.23    |

---

## Key Findings
- **LightGBM** achieved the **lowest RMSE** of **43.19**, making it the most accurate model for predicting hourly taxi orders.
- Demand peaks occur around **midnight and early morning hours**, with noticeable drops during late morning.
- Weekly patterns show higher demand on weekends.

---

## Conclusion
The Random Forest and LightGBM models performed best overall, with LightGBM offering a small but meaningful improvement in RMSE.  
The project successfully met the goal of achieving an RMSE below 48, confirming the effectiveness of feature engineering and model tuning.

---

## How to Run

Install Juypter Notebook

Open Sprint 13.ipynb

Install necessary libaries

---

## Technologies Used
- Python (Pandas, NumPy, Matplotlib, Seaborn)
- Scikit-learn
- XGBoost
- LightGBM
- CatBoost
- Jupyter Notebook

---

## Author
Kelvin Pina
