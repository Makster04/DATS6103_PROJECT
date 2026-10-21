Example of how to make the README template for this project, following our instructor's rules, to look like mine [https://github.com/Makster04/FINAL_CAPSTONE_PROJECT/blob/main/README.md]

Our instructors order:
It should cover, in roughly this order:
- the question, and the decision it informs
- where the data came from and what is missing from it
- what you did to the data, with reasons
- the models, the baseline, and how they were evaluated
- what the analysis does and does not support
- limitations specific to your data, not generic ones


# Predicting Next Quarter's Economic Regime from Lagged Macro Indicators

**DATS 6103 – Introduction to Data Mining · Team Project · Fall 2026**
**Team:** [Name 1] · [Name 2] · [Name 3]

📄 **Report:** [`report/report.html`](report/report.html)

---

## The Question

Can lagged macroeconomic indicators predict whether the U.S. economy will be in **Boom, Stability, Slowdown, or Recession** next quarter?

- **For whom:** corporate finance leaders (CFOs) setting budgets and hiring plans.
- **The decision it changes:** whether to tighten spending and hiring ahead of a downturn, or hold course.
- **The costlier mistake:** missing a coming Recession. A false alarm means caution that turns out to be unnecessary; a missed recession means being caught over-extended. Models are therefore judged mainly on **Recession recall and F1**, not overall accuracy.

---

## The Data

| | |
|---|---|
| **Sources** | Federal Reserve Economic Data (FRED); Bureau of Labor Statistics (BLS) |
| **Coverage** | 1970–2024, quarterly |
| **One row is** | one quarter |
| **Size** | ~220 quarters × 30+ indicators |
| **Target** | regime label in `Regime_Labels.csv`, defined by [labeling rule] |

Files in `data/`:
- `Prediction_Indicators.csv` — the indicators as downloaded
- `lags.csv` — lagged versions of each indicator, built by `src/build_features.py`
- `Regime_Labels.csv` — the target, built by `[script]` using [labeling rule]

### What's missing from it
- **Real-time data.** FRED serves revised figures. A forecaster in 2007 saw first-release numbers that were later revised, so the model learns from information nobody had at the time.
- **Recessions.** 1970–2024 contains only a handful of recession episodes, so the Recession class is small and the test period holds only [n] recession quarters.
- [Indicators that begin after 1970 and are mostly imputed in early years]

---

## Data Preparation

| Step | What we did | Why |
|------|-------------|-----|
| Merge | Joined the three files on `observation_date` | One row per quarter |
| Clean | Dropped duplicate rows and fully empty columns | — |
| Features | 25+ per quarter: lags (1–4 quarters), rolling means and standard deviations, stress flags | Regime shifts build over several quarters |
| Missing values | Filled with column means **computed on the training window only** | Keeps later values from leaking into earlier quarters |

All fitted steps (imputation, scaling) sit inside a scikit-learn `Pipeline` and are refit on each training window.

---

## Exploration

- [How often each regime occurs, and how rare Recession is]
- [Which indicators visibly move before regime changes]
- [Anything that shaped the modeling choices]

---

## Models and Evaluation

### Baseline
Predict the most common regime ([Stability]) every quarter → Recession recall = 0, accuracy = [x].

### Models
| Model | Why it suits the question |
|-------|---------------------------|
| Multinomial logistic regression | Interpretable coefficients; tests whether a linear model is enough |
| XGBoost classifier | Captures nonlinear interactions between indicators |

### Evaluation protocol
- **Sliding-window cross-validation** for tuning: train on past quarters, validate on the next block, roll forward. The model never trains on the future.
- **Held-out test period** ([20XX]–2024), scored once at the end.
- Class imbalance handled with **class weights** inside each training window.

---

## Results (held-out test quarters)

| Model | Recession recall | Recession F1 | Accuracy |
|-------|------------------|--------------|----------|
| Baseline | 0 | 0 | [ ] |
| Logistic regression | [ ] | [ ] | [ ] |
| XGBoost | [ ] | [ ] | [ ] |

*Values are copied from the report, where they are computed.*

- **Confusion matrix:** [Where the errors fall. Earlier runs predicted Stability and Boom well and confused Recession with Slowdown; confirm on the final run.]
- **What drives predictions:** [Top indicators from logistic coefficients and XGBoost feature importance.]

### What we tried and dropped
| Tried | Why we dropped it |
|-------|-------------------|
| Two-stage pipeline: forecast each indicator a quarter ahead (VAR, Prophet, XGBoost regressor), then classify the forecasts | It added a second source of error, and a wrong prediction could not be traced to either stage. Classifying directly from lagged values is simpler and [performed comparably]. |
| SMOTE oversampling | It creates synthetic quarters by interpolating between real ones, which has no meaning in a time series, and applied before the split it leaks information. Class weights address imbalance without inventing data. |

---

## What the Analysis Does and Does Not Support

**Supports:** [e.g., lagged indicators carry information about next quarter's regime beyond the baseline, if the test results show it.]

**Does not support:**
- Causal claims about what triggers recessions; feature importance shows association, not cause.
- Confidence about any single future recession, since the test period contains only [n] recession quarters.
- Real-world forecasting accuracy, since the model was trained and tested on revised rather than real-time data.

---

## How to Run

```bash
git clone https://github.com/[user]/[repo].git
cd [repo]
pip install -r requirements.txt
python src/build_features.py
jupyter nbconvert --to html --execute report/report.ipynb
```

Python [3.11] · Random seed: `42`

---

## Repository Structure

```
├── data/
│   ├── Prediction_Indicators.csv
│   ├── lags.csv
│   └── Regime_Labels.csv
├── src/
│   └── build_features.py     # builds lags.csv and Regime_Labels.csv
├── report/
│   ├── report.ipynb          # source of every number
│   └── report.html
├── requirements.txt
└── README.md
```

---

## AI Disclosure
[Level per the course's four-level standard, and what the assistant was used for.]

---

## Conclusion
[Two or three sentences answering the question, stated only as strongly as the test results allow.]
