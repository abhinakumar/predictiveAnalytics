# predictiveAnalytics
# 🔥 Forest Fire Burned Area Prediction

Predicting wildfire severity in Montesinho Natural Park, Portugal, using meteorological data and Fire Weather Index (FWI) components. A complete data science pipeline: cleaning → EDA → statistical analysis → model comparison → evaluation.

## Problem

Wildfires cause serious ecological and economic damage. This project asks: **can we predict the burned area of a forest fire from weather conditions and FWI indices alone?**

## Dataset

- **Source:** [UCI Machine Learning Repository — Forest Fires Data Set](https://archive.ics.uci.edu/dataset/162/forest+fires) (Cortez, P. & Morais, A., 2007)
- **Size:** 517 records, 13 attributes (weather, FWI indices, spatial grid location, burned area)
- **License:** CC BY 4.0 — Cortez, P. & Morais, A. (2007). Forest Fires [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5D88D

## Repository Structure

```
├── data/
│   ├── forestfires.csv          # raw dataset
│   └── forestfires_clean.csv    # cleaned dataset
├── figures/                     # all generated plots
├── outputs/
│   ├── model_comparison.csv
│   └── results.json
├── forest_fire_project.ipynb    # full analysis notebook (run top to bottom)
├── analysis.py                  # equivalent script version
├── Forest_Fire_Project_Report.docx
└── README.md
```

## Method

1. **Cleaning:** removed 4 duplicate rows, checked for missing values (none), retained legitimate large-fire outliers, applied log1p transform to the heavily right-skewed target.
2. **EDA:** target distribution, seasonal/day-of-week patterns, correlation heatmap, spatial severity map, feature-vs-target scatter plots.
3. **Statistical analysis:** Pearson correlation tests per feature, weekend-vs-weekday t-test, month ANOVA.
4. **Modeling:** 7 regression models compared (Linear, Ridge, Lasso, Decision Tree, Random Forest, Gradient Boosting, SVR) with an 80/20 split and 5-fold cross-validation.
5. **Evaluation:** MAE, RMSE, R² on held-out test data; feature importance via Random Forest.

## Key Results

| Model | Test MAE | Test RMSE | Test R² |
|---|---|---|---|
| **SVR (RBF)** | **0.988** | 1.314 | -0.033 |
| Decision Tree | 1.032 | 1.292 | 0.001 |
| Linear Regression | 1.074 | 1.267 | 0.039 |
| Ridge Regression | 1.076 | 1.265 | 0.042 |
| Lasso Regression | 1.090 | 1.262 | 0.046 |
| Random Forest | 1.130 | 1.312 | -0.030 |
| Gradient Boosting | 1.214 | 1.522 | -0.386 |

SVR (RBF) generalizes best; tree ensembles overfit on this small (513-row) dataset. Test R² stays near zero across all models — a known, published property of this dataset, not a modeling shortfall.


## Limitations

- Small dataset (513 usable records) limits model capacity.
- No fuel-load, vegetation, or firefighting-response data — known major drivers of fire size.
- Single park, 2000–2003 — generalization to other regions/eras is untested.

## Future Work

- Reframe as a classification task (small vs. large fire).
- Incorporate satellite vegetation/fuel-moisture indices.
- Apply resampling for skewed regression targets (e.g. SMOGN).

## Citation

> P. Cortez and A. Morais. *A Data Mining Approach to Predict Forest Fires using Meteorological Data.* In J. Neves, M. F. Santos and J. Machado (Eds.), New Trends in Artificial Intelligence, Proceedings of EPIA 2007, pp. 512-523, 2007.

## Author

Abhinav — M.Tech Data Science & Analytics, Lovely Professional University

