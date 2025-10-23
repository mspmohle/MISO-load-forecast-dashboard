# MISO-load-forecast-dashboard
Forecasting and visualizing regional electricity demand using MISO open data (2021–2024).

research question - How accurately can short-term electricity load in the MISO region be forecast using baseline time-series models, and how can these forecasts be visualized for operational insight?

Proposed approach - To answer this, hourly MISO system load data is cleaned, explored, and aggregated into daily averages. A baseline ARIMA (1,1,1) model is developed to produce a 14-day load forecast, evaluated against historical data using MAE and RMSE metrics. The outputs—including summary statistics, diagnostic plots, and forecast CSVs—serve as the analytical foundation for an interactive dashboard that can support grid operators and energy analysts in monitoring and planning short-term electricity demand.
