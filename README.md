# Anomaly_Detection_-_Forecasting
This assignment combines anomaly detection in building electricity consumption with forecasting South African CPI inflation for 2026. It covers data preparation, exploratory analysis, statistical and machine learning models, model evaluation, and interpretation of findings.
# Electricity Anomaly Detection and Inflation Forecasting

**EDAB6808 · Assignment 2 · University of the Free State**

## Project overview

This assignment contains two applications of time-dependent data: detecting unusual electricity-meter readings and forecasting South African consumer price inflation. Both tasks emphasise data quality, appropriate validation, benchmark comparison and clear interpretation of model performance.

## Question 1: Electricity anomaly detection

### Objective and data

Identify anomalous hourly electricity readings across buildings and produce a binary prediction for every reading in an unseen test file.

The training data contain **1,749,494 readings from 200 buildings**, including **37,296 labelled anomalies (2.13%)**. The test file contains **1,800,567 readings from 206 buildings**.

### Approach

- Audit the readings and preserve the distinction between missing values and recorded consumption.
- Construct historical consumption, calendar and contextual features.
- Compare Random Forest, XGBoost, Logistic Regression and a label-assisted Isolation Forest approach.
- Separate building groups for tuning, threshold selection and evaluation.
- Assess Average Precision, precision, recall and F1 rather than relying on accuracy for this imbalanced task.

### Key findings

XGBoost ranked first under the pooled Average Precision selection criterion.

| Evaluation measure | XGBoost result |
| --- | --- |
| Average Precision | **0.7540** |
| Precision at the selected threshold | **95.36%** |
| Recall at the selected threshold | **62.00%** |
| F1-score | **0.7514** |

The final model flagged **27,252 test readings (1.51%)**. This percentage describes the predictions; it is not test accuracy because the test labels were unavailable. High precision supports selective investigation, while the recall result shows that substantial numbers of anomalies can still be missed.

## Question 2: South African inflation forecasting

### Objective and data

Forecast monthly headline year-on-year CPI inflation for **January–December 2026**, using **60 monthly observations from January 2021 to December 2025**. The target is the official Statistics South Africa Table B2 inflation rate; the supplied Table B1 CPI index supports validation and exploratory analysis.

### Approach

- Compare SARIMA and Random Forest with last-value and seasonal naive benchmarks.
- Tune configurations using expanding historical forecast origins.
- Select the model family using 2024 year-ahead forecasts.
- Check the fixed choices on 2025, without changing the selection using those later results.
- Distinguish a complete year-ahead forecast path from forecasts updated one month at a time.

### Key findings

- **SARIMA(1,1,0)(0,0,1)₁₂**, without deterministic drift, was selected on 2024 RMSE: approximately **1.190 percentage points**, compared with **1.201** for the last-value benchmark.
- Random Forest performed better in the locked 2025 year-ahead check: RMSE approximately **0.321**, compared with **0.416** for SARIMA.
- The final selected forecast reached approximately **4.22% in December 2026**, with a conditional 95% pointwise prediction interval of approximately **0.55%–7.88%**.

The forecasts are monthly year-on-year rates. Averaging those rates does not produce annual-average CPI inflation. No observed 2026 inflation was used to fit or evaluate the models.

## Repository materials

| Material | Contents |
| --- | --- |
| Anomaly-detection notebook and executive report | Feature engineering, model comparison, evaluation and test-prediction analysis. |
| Inflation-forecasting notebook and executive report | Target validation, chronological backtests, forecast comparisons and uncertainty analysis. |

## Tools and skills

Python, pandas, NumPy, scikit-learn, XGBoost, Optuna, statsmodels, matplotlib and seaborn. The assignment develops feature engineering, imbalanced classification, threshold selection, chronological validation and forecast communication.

## Limitations and lessons

Anomaly-detection performance varies between buildings, and high precision does not ensure high recall. Inflation-model rankings change with the period, forecast horizon and error measure. Five years of inflation data and wide prediction intervals limit confidence in a single forecast path. Both tasks show why model selection and evaluation should be kept separate.

## Credits

Collaborative coursework by **Buhle Mbokodo and Reatile Seekoei** for EDAB6808 at the University of the Free State. Data references and detailed methods appear in the two executive reports.
