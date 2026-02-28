Model Card: Bayesian-Optimised LightGBM Demand Forecast Model
Model Details

Model Type: LightGBM Regressor

Objective: Regression (predict daily sales)

Optimisation: Bayesian Hyperparameter Optimisation (Optuna)

Training Data: Walmart M5 (Single Store – CA_1)

Intended Use

Daily demand forecasting for inventory planning and replenishment optimisation.

Performance (Validation Set)

RMSE: 2.0351

MAE: 1.0443

SMAPE: 134.66%

Baselines

Linear Regression RMSE: 2.1219

Default LightGBM RMSE: 2.0378

Grid Search RMSE: 2.0599

Limitations

Intermittent demand leads to high SMAPE

Model trained on single-store data

No external macroeconomic or competitor signals included

Ethical Considerations

No personal data used

Forecast errors may impact inventory decisions and supply chain efficiency

Over-forecasting may increase waste; under-forecasting may cause stockouts