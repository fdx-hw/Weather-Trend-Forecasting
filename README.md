#  Global Weather Forecasting Project

##  Overview
This project focuses on analyzing global weather data and building predictive models to forecast daily temperatures.  
It includes **data cleaning**, **exploratory data analysis (EDA)**, **time-series forecasting**, and **machine learning modeling** to understand climate behavior and improve prediction accuracy.

---

## Data Cleaning & Preprocessing
- Dataset contains ~104,000 weather observations across 41 variables (temperature, humidity, precipitation, air quality, etc.).
- Removed missing, duplicate, and extreme outlier values using statistical thresholds.
- Normalized numeric features using **RobustScaler** to minimize the influence of outliers.
- Kept only **metric-based features** for consistency across global locations.

---

##  Exploratory Data Analysis (EDA)
- **Temperature:** Slightly right-skewed, meaning most locations experience moderate temperatures.
- **Humidity:** Right-skewed; humid environments dominate globally.
- **Precipitation:** Highly imbalanced with mostly dry days and few heavy rainfall events.
- **Correlations:** Strong negative relationship between temperature and humidity; weaker relationships among other features.
- Visualized global distributions, city-level trends, and feature correlations.

---

##  Time-Series Forecasting
To avoid averaging across different climates, forecasts were generated at the **city level** (e.g., *Kabul*, *Bangkok*).

### Models Used:
- **ARIMA:** Captures short-term dependencies; low MAE and RMSE values; ideal for local forecasting.
- **Prophet:** Captures long-term seasonality and trends; slightly higher error but smoother results.

| Model | Strength | Limitation |
|--------|-----------|-------------|
| ARIMA | Precise short-term predictions | Misses complex seasonality |
| Prophet | Good trend and seasonality handling | Less reactive to short spikes |

---

## Anomaly Detection
Temperature anomalies were identified using three methods:
1. **IQR (Interquartile Range):** Detects values beyond 1.5×IQR.
2. **Z-score:** Identifies points beyond ±2.5 standard deviations.
3. **Rolling Window:** Finds sudden deviations from a 7-day moving average.

Each anomaly type was visualized in color to highlight sudden spikes or drops across the time series.

---

## Machine Learning Models
Developed **Random Forest** and **XGBoost** models using engineered features:
- Lag features (past 1–14 days)
- Rolling statistics (7-day and 14-day mean/std)
- Expanding mean
- Temporal encodings (day, month, weekday, year)
- Seasonal components (`sin`/`cos` of month)

### Model Results
| Model | MAE | RMSE | Comment |
|--------|-----|------|----------|
| Random Forest | 0.036 | 0.050 | Best short-term accuracy |
| XGBoost | 0.228 | 0.294 | Captures smoother trends |

---

## City-Level Climate Comparison
| City | Climate Type | Observations |
|-------|---------------|---------------|
| **Abu Dhabi** | Hot, arid, minimal rainfall | Steady rise in temperature |
| **Bangkok** | Warm, humid, tropical | Similar warming pattern with rainfall variability |

Both cities exhibit a gradual warming trend and reduced precipitation, suggesting a global warming effect.

---

## Air Quality Analysis
- Pollutants such as **PM2.5**, **PM10**, and **NO₂** are highly correlated — they increase together due to common emission sources.
- Weather parameters like temperature and humidity show weaker correlations with pollutants, indicating climate has less influence on pollution spikes than human activity.

---

##  Key Takeaways
- **Random Forest** achieved the best accuracy and consistency.
- **ARIMA** excelled in short-term, city-level forecasting.
- Combining anomaly detection, EDA, and ML modeling created a robust, explainable weather prediction pipeline.

---

## How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/fdx-hw/Weather-Trend-Forecasting.git
   cd weather-forecasting
2. Open the Jupyter Notebook
3. Run all the cells in order
4. Modify the city variable (e.g., "Bangkok", "Abu Dhabi") to run city-specific forecasts.
