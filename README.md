# Bike Sharing Demand Forecasting

## Project Overview

This project focuses on forecasting hourly bike-sharing demand using historical rental data and machine learning regression models. The goal was to identify patterns in bike usage, compare different models, and improve prediction performance through hyperparameter tuning.

The project follows an end-to-end workflow, from exploratory data analysis and feature engineering to model evaluation and interpretation.

## Objectives

- Analyze historical bike-sharing demand and identify usage patterns.
- Develop and compare multiple regression models.
- Establish a seasonal-naive baseline for comparison.
- Improve model performance through hyperparameter tuning.
- Evaluate predictions using appropriate regression metrics.

## Dataset

- **Source:** OpenML Bike Sharing Demand dataset
- **Observations:** 17,379 hourly records
- **Features:** 15 columns, including the date and an additional experimental promotion flag
- **Target variable:** `count` — hourly bike rental demand

Key features include:
- **Time-based:** Season, year, month, hour, weekday
- **Weather-related:** Temperature, feels-like temperature, humidity, wind speed, weather conditions
- **Calendar-related:** Holiday and working-day indicators

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

## Project Workflow

### 1. Data Preprocessing and EDA
- Inspected dataset structure, data types, and missing values.
- Analyzed demand patterns across hours, weekdays, seasons, and promotional periods.
- Explored relationships between weather conditions and bike demand.

### 2. Train-Test Split
Used a chronological 80/20 train-test split instead of randomly shuffling observations. This preserved the time order and helped evaluate the models on future observations.

- **Training set:** 13,903 observations
- **Test set:** 3,476 observations

### 3. Baseline Model
Established a seasonal-naive baseline using demand from the same hour in the previous week (`shift(168)`).

This provided a reference point to determine whether machine learning models could improve upon a simple historical forecasting approach.

### 4. Model Development
Trained and compared the following regression models:

- Linear Regression
- Decision Tree Regressor
- Random Forest Regressor
- Gradient Boosting Regressor
- XGBoost
- LightGBM
- CatBoost

### 5. Hyperparameter Tuning
Experimented with model parameters such as tree depth, number of estimators, learning rate, minimum samples per split, and minimum samples per leaf to improve prediction performance.

### 6. Model Evaluation
Evaluated model performance using Mean Absolute Percentage Error (MAPE) and Weighted Absolute Percentage Error (WMAPE).

WMAPE was also considered to understand total absolute prediction error relative to total actual demand, particularly when demand varied substantially across hours.

## Results

### Model Comparison

| Model | MAPE |
|---|---:|
| Linear Regression | 358.59% |
| Decision Tree — tuned | 41.90% |
| Random Forest — initial | 38.01% |
| Random Forest — tuned | **36.66%** |
| Gradient Boosting — tuned | 51.23% |
| XGBoost — tuned | 54.90% |
| LightGBM — tuned | 44.32% |
| CatBoost | 56.56% |

*Results reflect the evaluated model configurations in this project. The tuned Random Forest achieved the lowest MAPE among the models tested.*

### Final Model: Random Forest Regressor

The selected model used the following parameters:

- `n_estimators = 100`
- `max_depth = 15`
- `min_samples_split = 20`
- `min_samples_leaf = 2`
- `random_state = 42`

**Final evaluation:**
- **MAPE:** 36.66%
- **WMAPE:** 21.38%

The tuned model improved on the initial Random Forest configuration, reducing MAPE from 38.01% to 36.66%.

## Key Findings

- Bike demand varied considerably by hour, with demand generally peaking between 4 PM and 6 PM.
- Midweek demand was generally higher than weekend demand.
- Weather and seasonal patterns were useful factors to investigate when understanding demand.
- The tuned Random Forest outperformed the other evaluated models on the primary MAPE metric.
- Performance on an unseen winter period was weaker, with MAPE around 41%, highlighting the challenge of forecasting across changing seasonal conditions.
- The experimental promotion-flag analysis showed differences in average demand between flagged and non-flagged observations. These results should be interpreted in the context of how the flag was constructed.

## Limitations and Future Improvements

- Use walk-forward validation to evaluate model consistency across multiple future periods.
- Investigate systematic overprediction and underprediction through bias analysis.
- Compare hourly and daily forecasting performance.
- Further investigate feature engineering, seasonal patterns, and promotion effects.
- Evaluate model performance across different demand levels and seasonal segments.

## Conclusion

This project provided practical experience in regression-based forecasting, time-aware data splitting, model comparison, hyperparameter tuning, and evaluation using multiple error metrics.

It also highlighted that selecting a forecasting model involves more than minimizing one metric: validation strategy, error direction, seasonal changes, and the intended business use all matter.
