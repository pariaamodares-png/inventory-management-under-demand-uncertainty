# Data-Driven Inventory Management under Demand Uncertainty

A case study combining demand forecasting and inventory policy simulation using a subset of the M5 Walmart sales dataset.

## Project Overview

This project investigates how historical sales data can support inventory decisions under demand uncertainty.

The workflow combines:

* Data cleaning and restructuring
* Exploratory demand analysis
* Time-series feature engineering
* Next-day demand forecasting
* Random Forest and XGBoost
* Safety stock calculation
* Reorder point calculation
* Inventory replenishment simulation

The analysis focuses on the SKU `HOBBIES_1_268` as a case study.

## Dataset

The project uses a subset of the publicly available M5 Walmart sales dataset from the M5 Forecasting – Accuracy competition.

The analysis uses:

* Historical daily sales
* Calendar information
* Weekly product prices

## Methodology

1. Load and clean the sales, calendar, and price data.
2. Reshape daily sales from wide to long format.
3. Integrate sales with calendar and price information.
4. Explore overall demand patterns.
5. Select `HOBBIES_1_268` as the case-study SKU.
6. Create lag and rolling-demand features.
7. Split the data chronologically into 80% training and 20% testing sets.
8. Compare a naive baseline, Random Forest, and XGBoost.
9. Evaluate forecasts using MAE and RMSE.
10. Calculate safety stock and reorder point.
11. Simulate inventory replenishment with a 7-day lead time.

## Forecasting Results

|     Model     |   MAE  |  RMSE  |
| ------------- | -----  | -----  |
| Baseline      | 11.764 | 17.385 |
| Random Forest |  8.594 | 12.863 |
| XGBoost       |  8.633 | 12.726 |

Random Forest achieved the lower MAE, while XGBoost achieved the lower RMSE on the held-out test period.

## Inventory Results

|        Metric            |      Value      |
| ------------------------ | --------------  |
| Selected SKU             | `HOBBIES_1_268` |
| Usable observations      |           1,905 |
| Training observations    |           1,524 |
| Test observations        |             381 |
| Lead time                |          7 days |
| Service level assumption |             95% |
| Safety stock             |           62.12 |
| Reorder point            |          129.32 |
| Order quantity           |          134.41 |
| Minimum inventory        |            6.19 |
| Final inventory          |          187.89 |
| Stockout days            |               0 |

## Inventory Policy

The reorder point is based on lead-time demand plus safety stock.

The current order quantity is set using a simple 14-day average-demand heuristic:

`Order Quantity = Average Daily Demand × 14`

Therefore, the current version should be considered a **data-driven inventory policy simulation**, rather than a full cost-based inventory optimization model.

## Limitations

* The detailed forecasting and inventory analysis focuses on one SKU.
* The project uses a subset of the original M5 dataset.
* The forecasting task is limited to next-day demand.
* Only a naive baseline, Random Forest, and XGBoost are evaluated.
* No hyperparameter optimization or rolling time-series cross-validation is performed.
* The lead time is assumed to be fixed at 7 days.
* The 95% service level is an assumption.
* The order quantity is heuristic rather than cost-optimized.
* Holding, ordering, shortage, and lost-sales costs are not explicitly modeled.
* The inventory simulation allows at most one outstanding replenishment order.
* A historical stockout rate of 0% in the simulation does not imply that the policy is optimal or guarantees future service levels.

## Future Work

Potential extensions include:

* Cost-based inventory optimization
* EOQ and joint reorder-point/order-quantity optimization
* Probabilistic demand forecasting
* Prediction intervals and uncertainty quantification
* Variable lead times
* Intermittent-demand forecasting
* Multi-SKU inventory optimization
* Multi-store analysis
* Rolling or expanding-window model validation
* Incorporating event and promotional information into forecasting

## Tools

| Tool         | Purpose                         |
| ------------ | ------------------------------- |
| Python       | Programming language            |
| Pandas       | Data manipulation               |
| NumPy        | Numerical computation           |
| Matplotlib   | Data visualization              |
| Scikit-learn | Machine learning and evaluation |
| XGBoost      | Gradient boosting model         |
| Google Colab | Development environment         |


## Data Source

M5 Forecasting – Accuracy dataset, Walmart sales data.
The dataset is publicly available through the M5 competition resources.
