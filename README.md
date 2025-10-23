# MISO-load-forecast-dashboard
Forecasting and visualizing regional electricity demand using MISO open data (2021–2024).

research question - How accurately can short-term electricity load in the MISO region be forecast using baseline time-series models, and how can these forecasts be visualized for operational insight?

Proposed approach - To answer this, hourly MISO system load data is cleaned, explored, and aggregated into daily averages. A baseline ARIMA (1,1,1) model is developed to produce a 14-day load forecast, evaluated against historical data using MAE and RMSE metrics. The outputs—including summary statistics, diagnostic plots, and forecast CSVs—serve as the analytical foundation for an interactive dashboard that can support grid operators and energy analysts in monitoring and planning short-term electricity demand.

Project Objectives

Acquire and preprocess hourly MISO system load data from the U.S. EIA API, with a fallback mechanism to generate realistic synthetic data for offline use.

Engineer time-based features (hour, day, month) to explore diurnal and seasonal demand patterns through visualizations and summary statistics.

Develop a baseline ARIMA forecasting model to predict short-term (14-day) load trends and evaluate model accuracy using MAE and RMSE metrics.

Generate visual outputs and data artifacts—including daily load trends, rolling averages, and forecast CSVs—for use in a future dashboard.

Establish a reproducible foundation for extending the analysis to advanced forecasting techniques (e.g., SARIMA, Prophet, or machine learning models).

Methods

The project was implemented in three sequential stages, each corresponding to a major Jupyter Notebook cell. All analysis was performed in Python using the pandas, matplotlib, seaborn, statsmodels, and scikit-learn libraries within a Conda-managed environment.

Data Import and Cleaning
Hourly system-load data for the Midcontinent Independent System Operator (MISO) region was retrieved from the U.S. Energy Information Administration (EIA) API. A fault-tolerant fallback generated a realistic synthetic dataset when the API was unavailable. The resulting data were cleaned, converted to a DatetimeIndex, and resampled to an hourly frequency to ensure uniform temporal coverage. Missing load values were linearly interpolated, and a reproducible local snapshot was saved to data/miso_hourly_load.csv.

Feature Engineering and Exploratory Visualization
Temporal features—including hour of day, day of week, and month—were derived to characterize MISO’s load variability. Summary statistics and exploratory plots (daily, weekly, and monthly patterns, along with a seven-day rolling mean) were created to validate the dataset’s realism and to identify cyclical trends typical of regional electricity demand. All visualizations were saved automatically to the figures/ directory for later inclusion in reports and dashboards.

Time-Series Aggregation and Baseline Forecasting
The cleaned hourly data were aggregated to daily means to reduce high-frequency noise. A baseline ARIMA(1,1,1) model was fitted to 80 % of the data (training set) and evaluated on the remaining 20 % (test set). Model performance was assessed using Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE). The model then produced a 14-day ahead forecast, which was exported to data/outputs/forecast_next14days.csv. A diagnostic plot comparing actual versus predicted loads was saved as figures/arima_baseline_forecast.png.
