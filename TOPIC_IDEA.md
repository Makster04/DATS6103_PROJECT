DATS 6103 / FALL 2026 / TEAM DECISION DRAFT

# Forecasting the Next Breakout Exports

**BINARY CLASSIFICATION | ANNUAL EXPORT DATA**

**THE ONE-LINE QUESTION** Among commodities currently outside their country’s top 10% of exports by dollar value, which features best predict entry into the top 10% the following year?

**TEAM** Mak Trnka | Galileo Perricone | Miguel Sanchez

## 01 THE QUESTION

**Prediction** — For each eligible commodity, we will predict whether it **enters its country’s top 10%** the following year (1) or **remains below the cutoff** (0).

**Audience and decision** — Export-promotion agencies could use the forecast to prioritize exporter outreach. Market research teams could use it to choose which emerging products to investigate.

## 02 THE DATA

The United Nations’ *Global Commodity Trade Statistics* CSV contains **8,225,871 rows and 10 columns**. Each source row records one country’s annual trade in a commodity for a given trade flow. We will use eight fields: country, year, commodity code, trade flow, dollar value, weight, commodity category, and quantity unit. Each modeling row will represent one country–commodity pair in one forecast year.

**Coverage and limitations** — Missing product records can shift national rankings. We will check coverage by country and year, leave unverifiable outcomes unlabeled, and examine missing weights by quantity unit. A commodity can also enter the top 10% when exports of higher-ranked products fall.

## 03 EXPLORATION

We will select export records, exclude aggregate totals, check for duplicates and gaps, and flag percentage growth rates with a zero starting value. We will rank commodities by dollar value within each country and year. Using training years only, we will compare entry rates by commodity category and by how close each product was to the previous year’s cutoff.

## 04 MODELING

We will compare **binary logistic regression** and a **random forest classifier** using eight predictors: three annual export growth rates, two years of export value shares, two years of export weight shares, and commodity category.

We will train and validate in chronological order through **2012**, fitting preprocessing on training data only. To identify which features help most, we will remove one predictor group at a time, retrain each model, and measure the change in validation F1.

On the **2013–2016 test years**, we will compare both models with a majority-class baseline and a rule that selects products closest to the previous year’s cutoff. Our primary metric is **F1 for products entering the top 10%**. It balances **precision** (how many shortlisted products actually entered) and **recall** (how many actual entrants the model identified). We will report both measures and a confusion matrix for each model.

## 05 ACCOUNT OF THE FINDINGS

An **HTML report** and a **short team presentation** will show which predictor groups helped most and how many entrants each model found compared with the cutoff rule at the same shortlist size. Country–commodity examples will illustrate false alarms and missed entrants. The report will disclose AI use, and the GitHub repository will include the analysis and instructions to reproduce it.

**DATASET LINK** — [United Nations Global Commodity Trade Statistics on Kaggle](https://www.kaggle.com/datasets/unitednations/global-commodity-trade-statistics)
