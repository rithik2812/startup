# Startup Ecosystem Forecasting using ARIMA & LSTM

This repository presents a complete end-to-end forecasting pipeline designed to analyze long-term trends in the global startup ecosystem.
The project transforms raw startup-level data into a structured annual time-series and evaluates two forecasting approaches — ARIMA and LSTM — to determine which method more accurately predicts future funding cycles, valuation behavior, and unicorn emergence.

The analysis integrates data cleaning, aggregation, feature engineering, exploratory analysis, model development, performance evaluation, and 5-year ahead forecasting.

## Project Overview

Startup funding patterns evolve over time due to changing market dynamics, macroeconomic conditions, investor risk preferences, and technological shifts.
To study these behaviors, the project aggregates multiple startup-level metrics into yearly indicators and applies two forecasting approaches:

ARIMA — classical statistical model for stationary or linear time-series

LSTM — deep learning architecture capable of capturing nonlinear dependencies

## The goal of the project is to:

Convert cross-sectional startup data into a usable time-series

Identify multi-year trends in funding, valuation, and unicorn growth

Compare model performance on real aggregated data

Predict future patterns for the next 5 years

Interpret which model is best suited for long-term startup ecosystem analysis.


## Dataset Description

The raw dataset is structured at the startup level, with each row representing one startup.
This micro-level view contains detailed financial attributes that can be aggregated into annual macro indicators.

The dataset contains:

Startup Name – Company name

Year Founded – Establishment year

Funding Amount (M USD) – Funding received (in millions USD)

Valuation (M USD) – Company valuation

Revenue (M USD) – Annual revenue

Profitable – Binary indicator (1 = profitable, 0 = not profitable)

Even though the data is not originally time-series, it becomes suitable for forecasting after aggregation.


## Why This Dataset Works for Time-Series Forecasting

After grouping the data by year, the project computes aggregate values such as:

Total funding raised across all startups in that year

Number of startups founded

Average valuation

Profitability percentage

Number of unicorns (valuation ≥ 1B USD)

This produces a chronologically ordered annual dataset, which is ideal for time-series learning models.

The dataset captures macroeconomic cycles, investment booms, downturns, and valuation trends — all critical for forecasting.

Yearly Aggregation Methodology.


## To transform raw startup-level data into time-series, the following metrics are computed for each year:

n_startups – Count of startups founded

total_funding – Sum of funding amount

avg_valuation – Mean valuation across startups

avg_revenue – Average yearly revenue

profitability_rate – Percentage of profitable startups

unicorn_count – Count of startups valued ≥ 1000M USD.


## These aggregated metrics allow us to build time-series such as:

Year vs Total Funding

Year vs Average Valuation

Year vs Unicorn Count

Year vs Profitability Rate

These features reflect both short-term fluctuations and long-term momentum in the startup ecosystem.


## Exploratory Data Analysis (EDA)

A detailed EDA was performed to understand temporal behavior:

Total funding per year — reveals investment cycles, global shocks, and boom phases

Average valuation per year — signals how investor confidence changes

Unicorn count per year — reflects high-growth environment and scaling potential

Revenue and profitability trends — show financial health evolution over time

The EDA highlights both linear patterns (general upward trend) and nonlinear patterns (cyclical dips during downturns), justifying the comparison of ARIMA and LSTM.

ARIMA Model

ARIMA (Auto-Regressive Integrated Moving Average) is used as the baseline forecasting model.

Why ARIMA is Included

Works well when data size is small

Handles linear, autoregressive behavior

Provides interpretable coefficients

Sets a statistical benchmark against which complex models can be compared

How ARIMA Works in This Project

AR component uses past values to predict future ones

I component applies differencing to remove non-stationarity

MA component uses past forecasting errors

The model was trained on 80% of the timeline and validated on the remaining 20% to avoid leakage.

Limitations of ARIMA

Cannot handle strong nonlinear trends

Struggles with structural breaks (economic shocks)

Long-term forecasts tend to become overly linear and conservative

Despite these limitations, ARIMA provides a stable baseline.

LSTM Model

LSTM (Long Short-Term Memory Network) is a deep neural network well-suited for sequential data.

Why LSTM is Necessary for This Dataset

Startup ecosystem metrics are influenced by:

global market cycles

inflation, recession, interest rates

policy shifts

investor risk appetite

tech innovation waves

These dynamics introduce long-range nonlinear dependencies, which LSTM can learn far better than ARIMA.

LSTM Pipeline

Lookback window = 3 years

Features scaled using MinMaxScaler

Input shaped as sequences: (samples, 3 timesteps, 1 feature)

Architecture:

LSTM (32 units)

Dense output layer predicting next year’s value

Advantages

Captures nonlinear patterns

Learns multi-year dependency structures

More accurate long-term trajectories

## Model Performance

A detailed comparison was conducted using percentage error metrics:

| **Metric** | **ARIMA** | **LSTM** |
|-----------|-----------|----------|
| **RMSE%** | 32.28%    | 21.52%   |
| **MAE%**  | 22.37%    | 17.88%   |


## Interpretation

LSTM outperforms ARIMA in both metrics

ARIMA underfits nonlinear growth

LSTM identifies hidden relationships between years

Indicates that startup investment dynamics are not linear.


 ## Future Forecasting

Using the trained models, 5-year forecasts were generated.

ARIMA Forecast Characteristics

Smooth and linear

Stable but conservative

Misses nonlinear cycles

Good for baseline; not ideal for long horizons

LSTM Forecast Characteristics

More realistic fluctuation patterns

Captures ecosystem cycles

Indicates acceleration or slowdown phases

More adaptable to historical complexity

The LSTM forecast provides a richer understanding of future ecosystem behavior.
