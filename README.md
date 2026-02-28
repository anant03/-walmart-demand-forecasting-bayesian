# Bayesian-Optimised Demand Forecasting for Retail Inventory Planning

---

## NON-TECHNICAL EXPLANATION OF YOUR PROJECT

Retailers must predict how many units of each product will sell each day to avoid stockouts and excess inventory. Poor forecasts lead to lost sales or unnecessary storage costs. This project builds a machine learning model to predict daily product demand using historical sales data from Walmart. The model uses advanced optimisation techniques to improve forecasting accuracy. By comparing traditional grid search with Bayesian optimisation, the project demonstrates how intelligent hyperparameter tuning can enhance predictive performance and support better inventory planning decisions in retail environments.

---

## DATA

The dataset used in this project is the **M5 Forecasting – Accuracy** dataset from Kaggle, originally released by Walmart.

It contains:

* Daily unit sales for thousands of products
* Store-level information
* Calendar variables
* Product pricing data

For computational efficiency, this project uses a subset corresponding to a single store (CA_1) from 2011–2016.

The dataset is publicly available through Kaggle and is subject to Kaggle’s competition terms of use.

---

## MODEL

The model used is **LightGBM (Light Gradient Boosting Machine)**, a tree-based ensemble learning algorithm.

LightGBM was chosen because:

* It performs well on structured tabular data
* It captures non-linear relationships
* It handles large datasets efficiently
* It is widely used in retail forecasting applications

The model predicts daily unit sales for each product using historical demand patterns, price information, and calendar features.

---

## HYPERPARAMETER OPTIMISATION

Several hyperparameters influence LightGBM performance, including:

* Learning rate
* Number of leaves
* Maximum tree depth
* Number of estimators
* Subsampling parameters

Two optimisation approaches were compared:

1. **Grid Search** – Exhaustive evaluation over a predefined parameter grid
2. **Bayesian Optimisation (Optuna)** – Adaptive search using probabilistic modelling

Bayesian optimisation was used to efficiently explore the hyperparameter space and identify configurations that minimise validation RMSE.

The final model was retrained on the full training dataset using the best Bayesian parameters.

---

## RESULTS

Model performance was evaluated using a time-aware validation split (last 28 days held out).

Evaluation metrics:

* RMSE (Root Mean Squared Error)
* MAE (Mean Absolute Error)
* SMAPE (Symmetric Mean Absolute Percentage Error)

| Model                 | RMSE       |
| --------------------- | ---------- |
| Linear Regression     | 2.1219     |
| Default LightGBM      | 2.0378     |
| Grid Search           | 2.0599     |
| Bayesian (Full Train) | **2.0351** |

Key insights:

* Gradient boosting significantly outperforms linear regression.
* Grid search did not improve generalisation performance.
* Bayesian optimisation achieved the best validation accuracy.
* Default LightGBM parameters were already strong for this dataset.

Even modest improvements in forecast accuracy can translate into meaningful cost savings in real-world retail inventory systems.

---

## (OPTIONAL: CONTACT DETAILS)

For questions or collaboration inquiries:

GitHub: [https://github.com/anant03](https://github.com/anant03)
Email: [anant.nigam@gmail.com](mailto:anant.nigam@gmail.com)
