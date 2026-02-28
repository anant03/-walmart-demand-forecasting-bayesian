# Model Card

---

## Model Description

### Input

The model takes the following inputs for each SKU-day observation:

* Historical sales features:

  * Lag features (7, 14, 28 days)
  * Rolling mean features (7 and 28 days)
* Price-related features:

  * Current selling price
  * Price change from previous day
* Calendar features:

  * Weekday
  * Month
  * Year
  * SNAP indicator
* Store and item identifiers (used implicitly through feature grouping)

Each row represents a single item at a single store on a given date.

---

### Output

The model outputs:

* A single continuous value representing the predicted daily unit sales (`sales`) for a given SKU on a specific date.

The prediction is non-negative and corresponds to expected demand.

---

### Model Architecture

The model is a **LightGBM Regressor**, which is a gradient-boosted decision tree ensemble.

Key characteristics:

* Boosting type: Gradient Boosting Decision Trees (GBDT)
* Objective: Regression (minimisation of RMSE)
* Hyperparameters optimised using Bayesian optimisation (Optuna)
* Final model retrained on the full training dataset (5.6+ million observations)

LightGBM builds trees sequentially, where each tree attempts to correct the residual errors of the previous trees. This allows the model to capture:

* Non-linear relationships
* Feature interactions
* Complex seasonality patterns

---

## Performance

The model was evaluated using a **time-aware validation split**, where the final 28 days of the dataset were held out as validation data.

### Evaluation Metrics

* RMSE (Root Mean Squared Error)
* MAE (Mean Absolute Error)
* SMAPE (Symmetric Mean Absolute Percentage Error)

### Validation Results

| Model                 | RMSE   | MAE    |
| --------------------- | ------ | ------ |
| Linear Regression     | 2.1219 | 1.0842 |
| Default LightGBM      | 2.0378 | 1.0458 |
| Grid Search           | 2.0599 | 1.0501 |
| Bayesian (Full Train) | 2.0351 | 1.0443 |

The Bayesian-optimised LightGBM model achieved the best validation RMSE of **2.0351**.

Performance was measured on the held-out final 28 days of the dataset to prevent temporal leakage.

---

## Limitations

* The model is trained on a single-store subset (CA_1), limiting generalisability across regions.
* The dataset exhibits intermittent demand (many zero-sales days), which can inflate percentage-based metrics.
* The model does not incorporate:

  * Promotion campaign variables
  * External macroeconomic factors
  * Competitor pricing
* No probabilistic uncertainty intervals are provided.
* Performance may degrade under structural demand shifts not present in historical data.

---

## Trade-offs

* The model prioritises predictive accuracy (RMSE minimisation) over interpretability.
* Gradient boosting improves performance compared to linear regression but reduces model transparency.
* Bayesian optimisation improves hyperparameter search efficiency but increases computational cost.
* Using a single-store subset reduces computational burden but limits cross-store scalability.

The model performs well under stable historical demand patterns but may require retraining under demand regime changes.

---

This version:

* Matches your template exactly
* Is academically structured
* Clearly explains architecture
* Includes quantitative performance
* Discusses real trade-offs
