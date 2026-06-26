# Solar Irradiance Prediction for Rome

## Project Overview

This regression capstone predicts daily solar energy potential in Rome, Italy, using NASA POWER meteorological data. The target variable is daily all-sky solar irradiance, represented in the prepared dataset as `solar_irradiance_kwh_m2_day`.

The central question is whether weather and seasonal variables can predict daily solar irradiance more accurately than a simple historical monthly-average baseline. This matters for renewable energy planning because better daily solar estimates can support photovoltaic production planning, battery scheduling, demand management, and cleaner electricity systems.

The project is aligned with SDG 7, Affordable and Clean Energy, and SDG 13, Climate Action.

## Repository Structure

```text
.
|-- data/
|   `-- rome_solar_data_2015_2025.csv
|-- notebook/
|   `-- Simone_Rossi_regression_capstone.ipynb
|-- outputs/
|   `-- generated plots from the notebook
|-- src/
|   `-- requirements.txt
`-- README.md
```

## Dataset

The dataset contains daily solar and meteorological records for Rome from 2015-01-01 through 2025-12-31.

- Source: NASA POWER, accessed on 18 June 2026.
- Raw rows in the notebook: 4,018 daily records.
- Cleaned rows after removing one extreme precipitation value above 120 mm: 4,017.
- Missing values: none.
- Duplicate rows: none.

Main variables include:

- `date`
- `day_of_year`
- `temp_mean_c`, `temp_max_c`, `temp_min_c`
- `humidity_pct`
- `wind_speed_2m_m_s`, `wind_speed_10m_m_s`
- `precipitation_mm`
- `cloud_cover_pct`
- `solar_irradiance_kwh_m2_day` as the prediction target

## Notebook Workflow

The notebook follows a full regression workflow:

1. Define the sustainability problem, hypothesis, success criteria, and model constraints.
2. Load and inspect the NASA POWER dataset.
3. Clean the data, check missing values and duplicates, and review outliers.
4. Explore the target distribution, weather relationships, and feature correlations.
5. Engineer cyclical day-of-year features and a daily temperature-range feature.
6. Compare a seasonal monthly-average baseline with Linear Regression, Random Forest, Ridge Regression, and an ARIMA appendix model.
7. Evaluate models with hold-out metrics, 5-fold cross-validation, residual diagnostics, feature importances, and SHAP plots.
8. Summarize practical uses, limitations, fairness considerations, and next steps.

## Key Results

The final selected model is the tuned Random Forest Regressor. It gives the best balance of predictive accuracy and explainability, supported by feature importances and SHAP analysis.

MAE and RMSE are in kWh/m2/day.

| Model or check | Evaluation setup | R2 | MAE | RMSE |
| --- | --- | ---: | ---: | ---: |
| Seasonal monthly-average baseline | Hold-out test set | 0.7864 | 0.7981 | 1.0774 |
| Linear Regression | 5-fold cross-validation | 0.9437 | 0.3974 | 0.5561 |
| Ridge Regression | 5-fold cross-validation | 0.9437 | 0.3974 | 0.5561 |
| Random Forest Regressor, tuned | 5-fold cross-validation | 0.9556 | 0.3389 | 0.4929 |
| ARIMA(5, 0, 0) | Chronological time-series split | 0.0573 | 2.0089 | 2.2792 |

Main conclusions:

- The weather-driven models beat the seasonal monthly-average baseline by a wide margin.
- The tuned Random Forest more than halves average error compared with the baseline, reducing MAE from about 0.80 to 0.34 kWh/m2/day.
- The hypothesis is supported: meteorological and seasonal variables add meaningful predictive value beyond month-level seasonality.
- The strongest predictors are seasonal day-of-year features, maximum and mean temperature, cloud cover, humidity, and precipitation.
- Feature ablation shows that cyclical day-of-year encoding is the only engineered feature with a measurable positive effect; `temp_diff` is mostly redundant.
- Residual diagnostics show errors centered around zero, with mild extra spread in mid-range irradiance values where weather conditions are more variable.
- The ARIMA comparison confirms that univariate time-series structure alone is not enough for this task; the useful signal is mainly in the weather covariates.

## Selected Visual Outputs

The notebook exports figures to `outputs/`. Useful summary plots include:

- [Feature ablation CV R2](outputs/19_2.1.1_Feature_Ablation_CV_R2.png)
- [Baseline vs model performance](outputs/20_2.2.2_Baseline_vs_Models_Performance.png)
- [Random Forest feature importance](outputs/16_1._Feature_Importance_for_Random_Forest_Model.png)
- [Predicted vs actual solar irradiance](outputs/17_2._Predicted_vs._Actual_Solar_Irradiance.png)
- [Model comparison with ARIMA](outputs/18_4.5.3_Model_Performance_Comparison_with_ARIMA.png)

## How to Run

Create and activate a Python environment, then install the project dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r src/requirements.txt
```

Open and run the notebook:

```text
notebook/Simone_Rossi_regression_capstone.ipynb
```

The notebook is designed to load the CSV from `data/` and save generated plots to `outputs/`.

## Dependencies

The required Python packages are listed in `src/requirements.txt`:

- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- statsmodels
- shap
- ipykernel

If your environment does not already include Jupyter, install Jupyter or run the notebook through VS Code, Colab, or another notebook interface.

## Scope and Limitations

- The model is trained for Rome only and should not be transferred to other locations without validation or retraining.
- The predictions are daily estimates, not real-time or intraday solar ramp forecasts.
- NASA POWER data is satellite/model derived, so direct ground measurements could differ.
- The model predicts solar irradiance potential, not actual photovoltaic output from a specific installation.
- Forecasts should support human decision-making rather than fully automated energy control.
- Performance should be monitored over time because changing climate patterns may reduce accuracy without periodic retraining.

## Data Source

NASA Prediction of Worldwide Energy Resources (POWER): https://registry.opendata.aws/nasa-power/

The notebook notes that NASA POWER has no restrictions on data access, use, or download.
