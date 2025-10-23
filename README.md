MISO Load Forecast Dashboard

Forecasting and visualizing regional electricity demand using MISO open data (2021–2024) to demonstrate reproducible, data-driven forecasting and dashboard design for grid operations.

Research Question

How accurately can short-term electricity load in the MISO region be forecast using baseline time-series models, and how can these forecasts be visualized to provide operational insight for grid planning and decision-making?

This project investigates the predictive capability of classical statistical models—specifically ARIMA and SARIMA—for short-term load forecasting in the Midcontinent Independent System Operator (MISO) region. By developing a transparent, reproducible workflow from data ingestion to interactive visualization, it provides a proof-of-concept foundation for utilities, OEMs, and energy-tech organizations exploring grid analytics pipelines.

Proposed Approach

To address the research question, hourly MISO system load data is retrieved from the U.S. Energy Information Administration (EIA) API, cleaned, and aggregated into daily averages.
A baseline ARIMA(1,1,1) model is developed to produce a 14-day load forecast, evaluated against historical data using Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE).
The outputs—including summary statistics, diagnostic plots, and forecast CSVs—serve as the analytical foundation for an interactive Plotly dashboard, designed to support grid operators, analysts, and data-science practitioners in monitoring and planning short-term electricity demand.

Project Objectives

Acquire and preprocess hourly MISO system load data from the U.S. EIA API, with a fallback mechanism to generate realistic synthetic data for offline or air-gapped testing.

Engineer temporal features (hour, day, month) to explore diurnal and seasonal demand variability through statistical summaries and visual analytics.

Develop a baseline ARIMA forecasting model to predict short-term (14-day) load trends and evaluate model accuracy using MAE and RMSE metrics.

Generate visual outputs and data artifacts—including daily load trends, rolling averages, and forecast CSVs—for use in dashboards or external analytics workflows.

Establish a reproducible foundation for extending the analysis to advanced forecasting techniques (e.g., SARIMA, Prophet, or hybrid ML models).

Methods

The analysis was implemented in three sequential stages, each corresponding to a major Jupyter Notebook cell.
All work was performed in Python using pandas, matplotlib, seaborn, statsmodels, and scikit-learn within a Conda-managed environment.

Data Import and Cleaning
Hourly MISO system-load data was retrieved via the EIA API.
A resilient fallback generated synthetic data if the API was unavailable.
The data was cleaned, converted to a DatetimeIndex, resampled to hourly frequency, and interpolated to fill missing load values.
The cleaned dataset was cached locally as data/miso_hourly_load.csv for reproducibility.

Feature Engineering and Exploratory Visualization
Temporal features (hour, day of week, month) were derived to characterize MISO’s load variability.
Descriptive plots—daily load pattern, weekly distribution, monthly trend, and seven-day rolling mean—were generated and saved to the figures/ directory.
These visualizations confirmed realistic cyclic patterns consistent with typical regional demand behavior.

Time-Series Aggregation and Baseline Forecasting
The cleaned hourly data was aggregated to daily means to reduce high-frequency noise.
A baseline ARIMA(1,1,1) model was trained on 80 % of the data and validated on the remaining 20 %.
Model performance was measured using MAE and RMSE, and the model produced a 14-day ahead forecast exported to data/outputs/forecast_next14days.csv.
A diagnostic plot comparing actual versus predicted load was saved to figures/arima_baseline_forecast.png.

Key Results and Next Steps

Results:
The baseline ARIMA(1,1,1) model provided a strong proof-of-concept for short-term load forecasting using open MISO data.
The model achieved MAE ≈ 88.9 MW and RMSE ≈ 110.4 MW on the holdout set, demonstrating consistent predictive accuracy across daily intervals.
A follow-up SARIMA(1,1,1)(1,1,1,7) model introduced weekly seasonality; while its RMSE was higher within the limited data window, it validated that the pipeline supports modular testing of more complex seasonal models.
All forecasts and figures were successfully exported to version-controlled directories and integrated into an interactive Plotly dashboard for dynamic visualization and exploration.

Next Steps:

Extend the data horizon to capture multi-year seasonal effects for improved SARIMA stability and accuracy.

Experiment with Prophet and LSTM neural network models to benchmark statistical vs. deep-learning approaches.

Deploy the forecasting pipeline as a FastAPI or Streamlit microservice, enabling real-time dashboard updates.

Incorporate weather and temperature features to improve predictive power.

Explore cloud integration (AWS Lambda or Azure Functions) for automated data refresh and model retraining.

MISO-load-forecast-dashboard/
├── data/
│   ├── miso_hourly_load.csv               # Cached hourly load data (from EIA API or synthetic)
│   ├── outputs/
│   │   ├── forecast_next14days.csv        # Baseline ARIMA forecast results
│   │   └── sarima_forecast_next14days.csv # Enhanced SARIMA forecast results
│   └── dashboard_ready/
│       └── miso_forecast_unified.csv      # Unified dataset for Plotly dashboard
│
├── figures/
│   ├── daily_pattern.png                  # Average daily load profile
│   ├── weekly_distribution.png            # Load by day of week
│   ├── monthly_trend.png                  # Average monthly load trend
│   ├── rolling_mean.png                   # 7-day rolling mean visualization
│   ├── arima_baseline_forecast.png        # ARIMA model diagnostic plot
│   ├── sarima_forecast_holdout.png        # SARIMA model diagnostic plot
│   └── interactive/
│       └── miso_forecast_dashboard.html   # Interactive Plotly dashboard
│
├── MISO_load_forecast_dashboard.ipynb     # Main Jupyter Notebook
├── requirements.txt                       # Python dependencies
├── README.md                              # Project overview and documentation
└── environment.yml                        # (Optional) Conda environment specification

Citation and Attribution

This project uses publicly available data from the
U.S. Energy Information Administration (EIA) – Electricity Data API
and references regional load statistics from the Midcontinent Independent System Operator (MISO).

All code and analyses are original and developed for educational and research purposes under open-source terms.
If you reuse this work, please cite:

Mohle, M. (2025). MISO Load Forecast Dashboard: A Proof-of-Concept for Short-Term Electricity Demand Forecasting. GitHub Repository.
https://github.com/<your-github-username>/MISO-load-forecast-dashboard

MIT License

Copyright (c) 2025 Michael S. Mohle

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the “Software”), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
