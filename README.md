# Weekly Demand Forecasting for 5000 Unique Real-Time Time Series

This project demonstrates a dynamic approach to time series demand forecasting for 5000 unique products, providing forecasts for weekly demand over a 12-week horizon. The workflow utilizes a set of different forecasting models, evaluates them based on performance metrics, and selects the best model for each time series based on real-time data. The methodology is designed to continuously adapt as new data is received, ensuring that the most accurate model is used for each time series.

## Overview

The primary goal of this code is to forecast the demand for 5000 unique products (represented by individual time series) on a weekly basis. By using an expanding window cross-validation technique, the system evaluates different models, updates forecasts every 2 weeks, and determines which model best captures the demand patterns for each product. The output consists of 12-week forecasts, along with 80% prediction intervals, for each time series.

## Key Features

- **Dynamic Model Selection**: Uses multiple time series forecasting models and dynamically selects the best-performing model for each time series.
- **Expanding Window Cross-Validation**: Re-trains the model every 2 weeks and updates forecasts for the next 12 weeks, evaluating performance using Mean Absolute Error (MAE).
- **Forecast Confidence Intervals**: Provides 80% prediction intervals to quantify uncertainty in the forecasted demand.
- **Real-Time Adaptation**: As new data is received, the system adapts by choosing the best-fitting model, considering changes in trend, seasonality, or business cycles.

## Workflow

1. **Data Input**: The input data consists of time series for 5000 unique products, with weekly demand recorded over several years. The data should include columns such as `unique_id`, `ds` (date), `y` (actual demand).
   
2. **Model Selection**: The following forecasting models are considered:
    - Holt-Winters Method
    - Croston Method
    - Optimized Croston Method
    - Historic Average
    - Dynamic Optimized Theta (DOT)
    - Seasonal Exponential Smoothing
    - Aggregate-Dissagregate Intermittent Demand Approach (ADIDA)
    - ARIMA
    - MSTL (Multivariate Seasonal-Trend Decomposition using LOESS)
    - IMAPA (Intermittent Multiple Aggregation Prediction Algorithm)
    - TSB (Teunter-Syntetos-Babai)
    - Naive Method
    - Random Walk with Drift
    - Multiplicative Functional Linear Exponential Smoothing (MFLES)
    - Auto ARIMA
    - Auto ETS
    - Auto Theta
    - Auto CES

3. **Cross-Validation**:
   - An expanding window cross-validation routine is used to simulate real-time forecasting. Every 2 weeks, the forecasting process is re-run, and the next 12 weeks are predicted. This process is repeated four times, each time adjusting the model to the most recent data.
   - In each cutoff period, the forecast is generated using only the data available up to that point, preventing any data leakage.

4. **Evaluation**: The models are evaluated using the Mean Absolute Error (MAE) to assess their performance. The model with the lowest MAE for each time series is selected as the best model.

5. **Forecast Generation**: Once the best model for each time series is identified, forecasts for the next 12 weeks are generated, along with 80% prediction intervals to capture the uncertainty in the forecast.

6. **Output**: The output is a DataFrame that includes:
   - The best-performing model for each time series.
   - The forecasted demand for the next 12 weeks.
   - The 80% prediction intervals for each forecast.
  
## Customization

- **Add new models**: You can extend the model set by adding additional forecasting models as needed.
- **Modify cross-validation window**: Adjust the frequency of re-training (e.g., every 1 week or every month) by changing the parameters in the cross-validation function.
- **Use different metrics**: While MAE is used by default, you can replace it with other evaluation metrics such as RMSE, MAPE, etc.

## Future Enhancements

- **Incorporating external factors**: Future versions could integrate additional features like promotions, price, and inventory data to improve forecast accuracy.
- **Real-time data pipeline**: Extend the code to work with real-time data pipelines, automatically updating forecasts as new data is received.
- **Model performance visualization**: Create visualizations to better understand model performance and identify trends in forecasting accuracy over time.
