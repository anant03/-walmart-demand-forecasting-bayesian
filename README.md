# Walmart Demand Forecasting with Bayesian Hyperparameter Optimisation

## Overview

This project applies machine learning to forecast daily retail demand using the Walmart M5 dataset (single-store subset: CA_1).

We compare grid search and Bayesian optimisation for tuning a LightGBM regression model and evaluate performance using time-aware validation.

The objective is to improve demand forecast accuracy to support better inventory planning and replenishment decisions.

---

## Dataset

M5 Forecasting – Accuracy (Kaggle)

Single-store subset (CA_1) used for computational efficiency while maintaining realistic retail forecasting complexity.

Time period: 2011–2016
Target variable: Daily unit sales (`sales`)

Features include calendar variables, price information, and engineered lag/rolling statistics.

A time-based split was used:

* Training set: Historical data
* Validation set: Final 28 days

---

## Approach

* Data preparation and reshaping from wide to long format
* Feature engineering:

  * Lag features (7, 14, 28 days)
  * Rolling mean features
  * Price change features
  * Calendar and SNAP indicators
* Baseline regression model (Linear Regression)
* Advanced model (LightGBM)
* Grid search hyperparameter tuning
* Bayesian hyperparameter optimisation (Optuna)
* Full retraining using best Bayesian parameters
* Performance comparison using RMSE, MAE, and SMAPE

---

## Results

| Model                 | RMSE   | MAE    |
| --------------------- | ------ | ------ |
| Linear Regression     | 2.1219 | 1.0842 |
| Default LightGBM      | 2.0378 | 1.0458 |
| Grid Search           | 2.0599 | 1.0501 |
| Bayesian (Full Train) | 2.0351 | 1.0443 |

Key findings:

* Gradient boosting significantly outperforms linear regression.
* Grid search did not improve generalisation performance.
* Bayesian optimisation achieved the best validation RMSE.
* Default LightGBM parameters were already strong for tabular retail forecasting.

---

## Evaluation Metrics

* RMSE (Root Mean Squared Error)
* MAE (Mean Absolute Error)
* SMAPE (Symmetric Mean Absolute Percentage Error)

Time-aware validation ensured no data leakage across training and evaluation periods.

---

## Repository Structure

* `data/` – raw and processed datasets
* `notebooks/` – step-by-step modelling workflow
* `models/` – saved hyperparameters
* `model_card.md` – model documentation
* `dataset_card.md` – dataset documentation
* `README.md` – project overview

---

## Business Relevance

Improved demand forecasts enable:

* Reduced stockouts
* Lower inventory holding costs
* More accurate replenishment decisions
* Better working capital allocation

Even small improvements in RMSE can have meaningful financial impact at retail scale.

---

## Status

Completed coursework project demonstrating:

* End-to-end machine learning pipeline
* Hyperparameter tuning
* Bayesian optimisation
* Time-aware validation
* Model and dataset documentation
