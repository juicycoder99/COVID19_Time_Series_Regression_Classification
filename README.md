# COVID-19 in China — Regression, Classification and Clustering

End-to-end time-series analysis of daily COVID-19 confirmed cases across Chinese provinces, covering sliding-window regression, direction classification, and geographic clustering.

## Overview

Using daily confirmed COVID-19 cases for Chinese provinces, the project works through four parts.
The full implementation and analysis is in [`covid19_regression_classification.ipynb`](covid19_regression_classification.ipynb).

### 1. Data preparation
Slide a six-day window over Beijing's series: the first five days are the predictors `x1`..`x5` and
the sixth day is the target `y`. Saved to `Beijing_covid19_regression.csv`.

### 2. Regression
Predict the sixth day from the previous five. Train/test split, then linear regression and LASSO,
reporting the test MSE. Analyse the LASSO error as `alpha` varies over `[0, 1, 10, 100 … 1000]`
(the error rises and plateaus once the coefficients are fully shrunk).

### 3. Classification
Label each window `goup` / `godown` / `stable` from the sign of `y - x5` (saved to
`Beijing_covid19_classification.csv`). Apply logistic regression and analyse its accuracy across the
`penalty` (`l1`, `l2`) and `C` hyperparameters, with a table, a plot and a short discussion.

### 4. Clustering
Test the hypothesis *"nearby provinces show similar case counts"* by clustering the provinces with
k-means two ways — by their daily case series and by their geographic coordinates — and comparing
the two partitions (adjusted Rand index ≈ 0). The clusterings disagree, so the hypothesis is not
supported: case similarity is driven by outbreak magnitude (Hubei is an outlier), not by distance.

## Running it

```bash
pip install numpy pandas matplotlib scikit-learn
jupyter notebook covid19_regression_classification.ipynb
```

## Files

| File | Description |
|------|-------------|
| `covid19_regression_classification.ipynb` | Full implementation and analysis (Parts 1–4) |
| `PROJECT_BRIEF.pdf` | Project brief (goals, objectives, outcomes) |
| `daily_confirmed_cases.csv` | Daily confirmed cases per province |
| `coordinates.csv` | Latitude/longitude of the provinces |
| `Beijing_covid19_regression.csv` | Generated sliding-window regression dataset (Part 1) |
| `Beijing_covid19_classification.csv` | Generated classification dataset (Part 3) |
