# Bike Rental Demand Prediction

## Project Overview

This project focuses on analyzing hourly bike rental demand and developing regression models to predict the number of bike rentals based on seasonal, calendar, and weather-related factors.

The project uses historical bike-sharing data from Washington, D.C., to explore demand patterns, evaluate predictive performance, and understand model errors and prediction bias.

## Dataset

The project uses the original [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset), specifically the hourly dataset (`hour.csv`).

- **Records:** 17,379 hourly observations
- **Time Period:** 2011–2012
- **Location:** Washington, D.C.
- **Target Variable:** `demand` — hourly bike rental count

The dataset includes information about season, year, month, hour, weather conditions, temperature, humidity, wind speed, holidays, and working days.

## Project Workflow

1. Data loading and inspection
2. Exploratory Data Analysis (EDA)
3. Data cleaning and feature preparation
4. Chronological train-test split and time-series cross-validation
5. Baseline model development
6. Random Forest Regressor development and evaluation
7. Model evaluation using MAE, RMSE, WMAPE, and Mean Error
8. Prediction error and bias analysis
9. Comparison with a model using a Poisson objective
10. Findings, limitations, and conclusions

## Model Evaluation

The final Random Forest model was evaluated on an untouched test set using a chronological split to preserve the time-based order of observations.

| Evaluation Metric | Result |
|---|---:|
| MAE | 44.99 |
| RMSE | 69.56 |
| WMAPE | 18.09% |
| Mean Error | -16.48 |

### Understanding the Results

- **MAE:** The model's predictions differ from actual hourly demand by approximately 45 rentals on average.
- **RMSE:** Penalizes larger prediction errors more heavily than MAE.
- **WMAPE:** The total absolute prediction error represents 18.09% of the total actual rental demand.
- **Mean Error:** The negative value indicates an overall tendency to underpredict demand.

## Prediction Error Analysis

Additional analysis was performed to understand where the model makes larger prediction errors and whether its predictions show a consistent bias.

This included examining actual versus predicted demand, identifying observations with larger errors, and comparing prediction errors across different hours.

## Tools and Technologies

- Python
- Pandas and NumPy
- Matplotlib and Seaborn
- Scikit-learn
- Jupyter Notebook
- Power BI

## Conclusion

The project demonstrates an end-to-end regression workflow, from exploratory data analysis and feature preparation to model evaluation and error analysis.

A chronological validation and testing approach was used to evaluate the model while respecting the temporal structure of the dataset.
