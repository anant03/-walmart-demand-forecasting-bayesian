# Datasheet: Walmart M5 Forecasting Dataset (CA_1 Subset)

---

## Motivation

* **For what purpose was the dataset created?**
  The dataset was created for the Kaggle M5 Forecasting – Accuracy competition. The purpose was to benchmark forecasting methods for retail demand prediction across multiple products and stores.

* **Who created the dataset and on behalf of which entity? Who funded the creation?**
  The dataset was released by Walmart in collaboration with Kaggle for a public machine learning competition. The competition was organised by Kaggle, and the dataset reflects anonymised transactional sales data from Walmart stores.

---

## Composition

* **What do the instances represent?**
  Each instance represents daily unit sales of a specific SKU (item) at a specific store.

* **How many instances are there?**
  The full dataset contains over 30,000 SKUs across multiple stores and years.
  This project uses a filtered subset corresponding to a single store (CA_1), resulting in:

  * ~5.6 million training observations
  * ~85,000 validation observations

* **Is there any missing data?**
  Yes.

  * Missing price values exist in early time periods before products were introduced.
  * These were handled using forward-filling within each item group and remaining missing values were set to zero.

* **Does the dataset contain confidential or sensitive information?**
  No.
  The dataset contains anonymised transactional sales data and does not include personal customer information, protected communications, or legally confidential data.

---

## Collection Process

* **How was the data acquired?**
  The data originates from Walmart’s internal retail transaction systems and was anonymised before being released for the Kaggle competition.

* **If sampled, what was the sampling strategy?**
  This project uses a deterministic subset: all SKUs belonging to Store CA_1. No random sampling was applied at the dataset level (sampling was only used during hyperparameter tuning for computational efficiency).

* **Over what time frame was the data collected?**
  The dataset covers daily sales from 2011 to 2016.

---

## Preprocessing / Cleaning / Labelling

* **Was preprocessing performed?**
  Yes. The following preprocessing steps were applied:

  * Conversion from wide format (daily columns) to long time-series format
  * Merging with calendar metadata
  * Merging with sell price data
  * Forward-filling missing price values within item groups
  * Creation of lag features (7, 14, 28 days)
  * Creation of rolling mean features
  * Creation of price change features
  * Time-based train/validation split (last 28 days reserved for validation)

* **Was raw data saved?**
  Yes. The original Kaggle files were preserved in the `data/raw/` directory (not committed to GitHub due to size and licensing considerations).

---

## Uses

* **What other tasks could the dataset be used for?**

  * Retail demand forecasting
  * Time-series modelling research
  * Price elasticity modelling
  * Inventory optimisation simulation
  * Hierarchical forecasting

* **Are there risks or considerations affecting future uses?**
  Yes.

  * Demand is intermittent (many zero-sales days), which can distort percentage-based metrics.
  * The dataset reflects historical patterns and may not generalise to future structural changes.
  * The data is limited to transactional features and does not include promotional campaign details or macroeconomic factors.

  Users should ensure:

  * Proper time-aware validation is used.
  * Models are monitored for drift if deployed in production.

* **Are there tasks for which the dataset should not be used?**
  The dataset should not be used to make claims about consumer behaviour demographics, as it contains no customer-level information. It should also not be used for real financial trading or investment decisions without additional contextual validation.

---

## Distribution

* **How has the dataset been distributed?**
  The dataset was distributed via Kaggle as part of the M5 Forecasting – Accuracy competition.

* **Is it subject to license or terms of use?**
  Yes. Use of the dataset is subject to Kaggle’s competition rules and terms of service. The dataset should not be redistributed independently.

---

## Maintenance

* **Who maintains the dataset?**
  The dataset is hosted and maintained by Kaggle. It is not actively updated, as it represents a historical competition dataset.

---