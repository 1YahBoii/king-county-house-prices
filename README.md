# King County House Prices

Cleaning, exploring and modelling **21,613 house sales** in King County, Washington (including Seattle), May 2014 – May 2015, to estimate a house's market price from its features.

*Final project of IBM's **Data Analysis with Python** course (Coursera), part of the IBM Data Science Professional Certificate. Analysis and documentation are my own.*

![Python](https://img.shields.io/badge/Python-3-blue) ![pandas](https://img.shields.io/badge/pandas-data-150458) ![scikit-learn](https://img.shields.io/badge/scikit--learn-models-F7931E)

## 1. Business understanding
A real estate investment trust wants to start buying residential property and needs to estimate market prices.

## 2. Analytic approach
Price is a dollar amount, so this is a **regression** problem. I started from single-feature baselines, added features and curvature step by step, and judged the final models on a held-out test set.

## 3. Data
21 columns per sale: price, bedrooms, bathrooms, living and lot area, floors, waterfront, view, condition, grade, year built and renovated, location (zipcode, latitude, longitude) and neighbourhood averages.

## 4. Data preparation
- Dropped two ID columns with no information about price.
- Filled missing `bedrooms` (13 rows) and `bathrooms` (10 rows) with the column mean rather than dropping the houses.

## 5. Exploratory analysis
- **Strongest correlations with price:** living area (0.70), grade (0.67), above-ground area (0.61).
- **Waterfront houses** are clearly pricier and more variable. Non-waterfront houses show more outliers, but there are 21,450 of them against 163 waterfront homes.
- Longitude and zipcode alone are almost unrelated to price.

## 6. Modeling and 7. Evaluation
| Model | R² | Scored on |
|---|---|---|
| Longitude only | 0.0005 | training |
| Living area only | 0.493 | training |
| 11 features, linear | 0.658 | training |
| 11 features, pipeline (scale → polynomial → linear) | 0.751 | training |
| Ridge, α = 0.1 | 0.648 | **test** |
| Polynomial (degree 2) + Ridge | **0.700** | **test** |

The final models were scored on **3,242 houses they never saw**. Polynomial features were fitted on the training rows only, so no test data leaked into training. The honest result is **0.70**. The pipeline's 0.75 is a training score.

## 8. Conclusions and next steps
- Size and build quality drive price more than anything else.
- Adding curvature to Ridge improved the test R² from 0.65 to 0.70.
- **Next:** engineer features (house age, a renovated flag, sale month) and tune Ridge's alpha with cross-validated grid search.

## Tools
Python · pandas · NumPy · seaborn · matplotlib · scikit-learn · Jupyter

## Files
- `king_county_house_prices.ipynb` — the full analysis with code, outputs and charts.
