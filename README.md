# Forecasting the Next Breakout Exports

**DATS 6103 · Fall 2026**  
**Team:** Mak Trnka, Galileo Frank Perricone, and Miguel Sanchez Zanella

## 1. Research Question & Purpose

### Research Question

Each year, a country’s export rankings show which commodities bring in the most money. We will use past trade records to forecast which products could join that leading group next year.

> **Our question:** Among commodities currently outside their country’s top 10% of exports by dollar value, which features best predict entry into the top 10% the following year?

### Who Cares and Why

- **Export-promotion agencies** can use a watchlist to prioritize outreach to exporters of promising products.
- **Market research teams** can use the same watchlist to decide which commodities deserve a closer look.

### Decision the Answer Could Inform

Both groups have limited time to review products. One approach is to watch the commodities that finished just below last year’s cutoff. Another is to use export growth, export shares, and commodity category to build a watchlist.

> For the same number of products reviewed, which approach identifies more commodities that enter the top 10% the following year?

---

## 2. Data

### Data Source

- **Dataset:** *Global Commodity Trade Statistics*
- **Source:** United Nations, available through [Kaggle](https://www.kaggle.com/datasets/unitednations/global-commodity-trade-statistics).
- **Size and scope:** The CSV contains **8,225,871 rows and 10 columns**. We use annual product-level export records and exclude aggregate totals to avoid double counting.
- **Study period:** We use forecast years through **2011** for training, **2012** for validation, and **2013–2016** for final testing.

### Unit of Observation

A source row records one country’s annual trade in one commodity for a given trade flow, such as exports or imports.

> Each modeling row represents **one country–commodity pair in one forecast year**. For example, a 2013 forecast uses information available through 2012. The product’s 2013 rank determines the outcome.

### Important Variables

We use eight source fields: country, year, commodity code, trade flow, dollar value, weight, commodity category, and quantity unit. From these fields, we build the binary outcome and eight predictors.

| Role | Variable(s) | What they represent |
|---|---|---|
| Outcome | Entry into the top 10% | Among products previously below the cutoff, **1** means the product enters its country’s top 10% the following year. **0** means it remains below the cutoff. |
| Predictors 1–3 | Three annual export growth rates | The year-over-year percentage change in the product’s export value for each of the three preceding years. |
| Predictors 4–5 | Two annual export value shares | The product’s share of its country’s reported export value in each of the two most recent years. |
| Predictors 6–7 | Two annual export weight shares | The product’s share of its country’s reported export weight in those same two years. |
| Predictor 8 | Commodity category | The broader group to which the product belongs. |
| Identification and quality checks | Country, year, commodity code, trade flow, and quantity unit | Identify export records, link products across years, and check whether missing weights are more common for particular quantity units. |

### Coverage and Limitations

Our coverage check identified **100 countries** with at least one eligible commodity in the training period, in 2012, and in each test year from 2013 through 2016. Missing product records can shift national rankings, and missing or estimated weights can distort weight shares. We will leave the outcome unlabeled when a product’s following-year rank cannot be verified.

> A breakout measures a change in **rank within a country’s export mix**. A commodity can enter the top 10% because its own exports grew or because higher-ranked exports fell.

---

## 3. Exploratory Analysis

Before modeling, we will use the training data to examine how often products enter the top 10% and what those products looked like a year earlier.

- Check for duplicate country–commodity–year records, missing years, and zero starting values that make percentage growth undefined.
- Examine country and commodity coverage over time and check missing weights by quantity unit.
- Compare how often eligible products **enter the top 10%** versus **remain below the cutoff**.
- Compare entry rates across commodity categories and by distance from the previous year’s cutoff.
- Examine relationships among export growth, value shares, and weight shares using a correlation heatmap.

> A chart of entry rates by prior rank will show how informative the cutoff already is. That gives us a practical benchmark for judging the forecasts.

---

## 4. Modeling Plan

We will compare two supervised classification methods using the same eight predictors, eligible products, and forecast years.

### Method 1: Random Forest Classifier

- **Purpose:** Estimate which commodities are likely to enter the top 10% the following year.
- **Why it fits:** A random forest can capture nonlinear relationships and interactions. For example, recent growth may be more informative for a product that already accounts for a larger share of national export value.
- **Inputs and outcome:** Three annual growth rates, two value shares, two weight shares, and commodity category predict whether a product enters the top 10%.

### Method 2: Binary Logistic Regression

- **Purpose:** Estimate the probability that a commodity enters the top 10% the following year.
- **Why it fits:** Logistic regression provides an interpretable comparison. Its coefficients describe how each predictor relates to the estimated odds of entry while holding the other predictors constant.
- **Inputs and outcome:** We use the same eight predictors and binary outcome as the random forest so the models can be compared directly.

### Baseline and Model Comparison

- **Majority-class baseline:** Always predict the most common outcome in the training data.
- **Closest-to-cutoff baseline:** Select the products ranked just below the previous year’s top 10%. Match each model’s watchlist size within each country and forecast year.
- **Validation:** Fit preprocessing on training data only. Use 2012 to select each model’s classification threshold. Remove one feature group at a time and measure the change in validation F1 to assess its contribution.
- **Final evaluation:** Refit the models using data through 2012 and evaluate them on **2013–2016**. Our primary metric is **F1 for products entering the top 10%**. We will also report precision, recall, and a confusion matrix for each model.

> **Precision** tells us what share of the watchlist actually entered the top 10%. **Recall** tells us what share of all actual entrants the watchlist captured. **F1** summarizes the balance between the two.

---

## 5. How We’ll Present the Findings

We will present the project in a written report and a short oral presentation.

- **Written report:** An HTML report will document the data preparation, exploratory analysis, model comparisons, limitations, and AI use. The GitHub repository will include the analysis and instructions for reproducing it.
- **Presentation:** We will open with the watchlist decision, explain how a product qualifies as a new top-10% export, and show how each model performed against the cutoff rule.
- **Visuals:** A two-year rank diagram will illustrate entry. A bar chart will show entry rates by distance from the cutoff. A feature comparison chart will show changes in validation F1, and confusion matrices will show false alarms and missed entrants.

> We will close by showing which feature groups contributed most and how many new top-10% exports each approach identified for the same amount of review.