# 📊 Superstore Sales Forecasting

An end-to-end data science project that analyzes historical retail sales data and forecasts future sales using **Linear Regression** and **Facebook Prophet**.

---

## 📌 Project Overview

This project takes raw Superstore sales data (2014–2017) and walks through the complete data science pipeline:

- Data ingestion & exploration
- Cleaning & preprocessing
- Feature engineering
- Time-series analysis (trend + seasonality)
- Predictive modeling (Linear Regression & Prophet)
- Business insight generation

The final output is a **6-month sales forecast** with confidence intervals, plus actionable business recommendations.

---

## 🎯 Objectives

1. Understand historical sales patterns across years, months, and quarters
2. Identify seasonality (peak and low sales months)
3. Build and compare forecasting models
4. Deliver a business-ready report with growth insights and recommendations

---

## 📂 Project Structure
superstore-sales-forecasting/
│
├── data/
│ └── Sample - Superstore.csv # Raw dataset
│
├── outputs/
│ ├── charts/ # Saved visualizations
│ └── predictions.csv # Forecasted sales (with CI)
│
├── notebooks/
│ └── sales_forecasting.ipynb # Main analysis notebook
│
├── README.md
└── requirements.txt

text

---

## 🗃️ Dataset

- **Source:** Sample Superstore dataset (commonly used for retail analytics)
- **Rows:** 9,994 transactions
- **Columns:** 21 (Order info, Customer info, Product info, Sales, Quantity, Discount, Profit)
- **Time range:** January 2014 – December 2017
- **Region:** United States

**Key columns used:**

| Column | Description |
|--------|-------------|
| `Order Date` | Transaction date |
| `Sales` | Revenue from the order |
| `Profit` | Profit earned |
| `Category`, `Sub-Category` | Product classification |
| `Region`, `State`, `City` | Geography |
| `Segment` | Consumer / Corporate / Home Office |

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Base visualizations |
| `seaborn` | Statistical plots |
| `scikit-learn` | Linear Regression, metrics |
| `prophet` | Time-series forecasting |
| `google.colab` | File upload (Colab environment) |

---

## 🔄 Workflow

### 1. Data Loading & EDA
- Load CSV with `latin-1` encoding
- Inspect shape, dtypes, nulls, and summary statistics

### 2. Data Cleaning
- Convert `Order Date` and `Ship Date` to datetime
- Drop rows with missing critical values
- Remove duplicates
- Handle outliers using the IQR method

### 3. Feature Engineering
- Extract `Year`, `Month`, `Month_Name`, `Quarter`, `Day_of_Week`
- Build lag features (`Lag_1`, `Lag_2`, `Lag_3`) for regression
- Create a `Time_Index` trend variable

### 4. Exploratory Visualizations
- Yearly sales bar chart
- Monthly sales trend (line plot)
- Seasonality by month (average sales)

### 5. Time-Series Aggregation
- Resample data monthly → 48-month series

### 6. Modeling

**Linear Regression**
- Features: `Time_Index`, `Month`, `Quarter`, `Lag_1`, `Lag_2`, `Lag_3`
- Chronological 80/20 train-test split (no shuffling)

**Prophet**
- Yearly seasonality ON, weekly/daily OFF
- Multiplicative seasonality mode
- Forecasts test period + 6 future months

### 7. Evaluation

| Model | MAE | RMSE | R² |
|-------|-----|------|-----|
| Linear Regression | $3,873.75 | $5,019.14 | 0.6292 |
| **Prophet** | **$2,257.83** | **$2,760.08** | — |

✅ **Prophet outperformed Linear Regression by ~42% on MAE.**

### 8. Business Insights
- **Peak month:** February
- **Lowest month:** September
- **Avg yearly growth (CAGR):** 19.77%
- **6-month forecast (Jan–Jun 2018):** $12K → $20K range

---

## 📈 Key Findings

1. **Strong upward trend** — sales grew ~20% year-over-year
2. **Clear seasonality** — Q1 and Q4 outperform mid-year months
3. **Prophet captures seasonality better** than linear regression (which only fits trend + lag correlations)
4. **Future sales outlook** — steady growth projected through mid-2018

---

## 💡 Business Recommendations

- 📦 **Stock up inventory** ahead of peak months (Feb, Mar, Apr)
- 📣 **Run marketing campaigns** during low-sales months (Sep)
- 🔍 **Investigate growth drivers** — is it volume, pricing, or new regions?
- 📊 **Deploy Prophet** into a monthly forecasting pipeline for demand planning

---

## 🚀 How to Run

### Option 1: Google Colab (recommended)
1. Open the notebook in Colab
2. Run the first cell and upload `Sample - Superstore.csv`
3. Execute all cells in order

### Option 2: Local Environment

```bash
# Clone repo
git clone https://github.com/<your-username>/superstore-sales-forecasting.git
cd superstore-sales-forecasting

# Install dependencies
pip install -r requirements.txt

# Launch notebook
jupyter notebook notebooks/sales_forecasting.ipynb
📦 Requirements
text
pandas
numpy
matplotlib
seaborn
scikit-learn
prophet
jupyter
📊 Outputs
outputs/predictions.csv — Forecast with yhat, yhat_lower, yhat_upper

outputs/charts/ — Saved visualizations (trend, seasonality, residuals)

⚠️ Known Limitations
Outliers were dropped rather than capped — may remove legitimate large orders

Linear Regression cannot model seasonality directly (relies on month/quarter features)

Only ~48 monthly data points — Prophet works but has limited training data

Deprecated warnings: resample('M') → use 'ME'; palette → use hue

🔮 Future Improvements
□ Replace IQR dropping with winsorization (capping)
□ Add SARIMA / ARIMA as classical statistical baseline
□ Try XGBoost with lag features for tabular time series
□ Add MAPE for business-friendly error reporting
□ Build a Streamlit dashboard for interactive forecasting
□ Automate monthly retraining pipeline
