# Workforce Under Automation: AI Exposure and Synthetic Layoff Risk

**DATS 6103 · Fall 2026**  
**Team:** Mak Trnka, Galileo Frank Perricone, and Miguel Sanchez Zanella

## 1. Research Question & Purpose

### Research Question

This project will examine whether job and AI exposure characteristics can predict a profile’s assigned synthetic layoff risk category.

> **Our question:** How well can a random forest classifier and a multinomial logistic regression model predict whether a synthetic worker profile is labeled Low, Medium, or High risk?

### Who Cares and Why

- **Job seekers:** The results may show which job or AI exposure characteristics are associated with higher assigned risk categories in this dataset.
- **Human resources teams and labor agencies:** The results may point to patterns worth investigating with real workforce data.

### Decision the Answer Could Inform

Because the data is synthetic, this analysis cannot guide decisions about individual workers. It can help determine whether the patterns in the dataset are clear enough to warrant further study using real-world data.

> The findings could help researchers or labor agencies decide whether to investigate similar patterns with observed workforce and layoff data.

---

## 2. Data

### Data Source

- **Dataset:** *AI Impact on Jobs and Layoff Risk*
- **Source:** Kaggle
- **Time period and scope:** The dataset is described as containing 20,000 synthetic worker profiles and 16 columns. These counts will be checked after downloading the CSV. The proposal does not specify a time period.

### Unit of Observation

> Each row represents one synthetic worker profile with job and AI exposure characteristics and an assigned layoff risk category.

### Important Variables

| Role | Variable(s) | What they represent |
|---|---|---|
| Outcome or target | Assigned layoff risk category | The synthetic label to predict: Low, Medium, or High |
| Candidate predictors | Industry, job role, company size, routine-task percentage, AI adoption, automated-task percentage, AI use, training hours | Job and AI exposure characteristics that may help distinguish the assigned categories |
| Other relevant fields | Remaining dataset columns | Additional fields will be reviewed after the CSV is downloaded and may be included if they are relevant and appropriate |

### Coverage and Limitations

The profiles and risk labels are synthetic; they do not represent real workers or observed layoffs. The risk labels may also have been generated using the same characteristics we plan to use as predictors. If so, the models could learn the dataset’s label-generation rules rather than patterns that apply to actual workers.

> Results will describe how well the models predict labels in this dataset. They cannot establish the layoff risk of real workers or show that AI exposure causes layoffs.

---

## 3. Exploratory Analysis

Before modeling, we will check the dataset’s structure and look for patterns that may affect the analysis.

- Verify the number of rows and columns, and inspect the available variables.
- Check for duplicate records, missing values, unusual values, and category levels.
- Examine the balance of the Low, Medium, and High risk categories.
- Compare routine-task percentage, automated-task percentage, AI adoption, and industry across the assigned risk categories.
- Use tables and visualizations to identify patterns and possible problems with the data.

> This exploration will help us understand the dataset, assess whether the planned models are suitable, and identify any limits that should shape how we interpret the results.

---

## 4. Modeling Plan

We will compare two supervised classification methods and a simple baseline.

### Method 1: Random Forest Classifier

- **Purpose:** Predict whether a profile is assigned Low, Medium, or High synthetic risk.
- **Why it fits:** A random forest can model patterns across multiple characteristics and can capture relationships that are not strictly linear.
- **Planned inputs and outcome:** Candidate job and AI exposure characteristics as inputs; assigned risk category as the outcome.

### Method 2: Multinomial Logistic Regression

- **Purpose:** Predict the same three risk categories.
- **Why it fits:** This provides a second approach to the classification task and can offer a useful comparison with the random forest.
- **Planned inputs and outcome:** Candidate job and AI exposure characteristics as inputs; assigned risk category as the outcome.

### Baseline and Model Comparison

We will compare both models with a baseline that always predicts the most common risk category. Evaluation will use accuracy, macro-averaged precision, macro-averaged F1, and a confusion matrix.

> We will consider whether each model improves on the baseline, how well it performs across all three categories, and which types of profiles it tends to misclassify. These results will describe performance on synthetic labels only.

---

## 5. How We’ll Present the Findings

We will present the project in a written report and a short oral presentation.

- **Written report:** Describe the research question, dataset, exploratory analysis, models, results, and limitations.
- **Presentation:** Explain the main patterns and model comparison, and clarify what the findings can and cannot tell us.
- **Visuals:** Include exploratory visualizations, model performance comparisons, and examples of classification errors.

> We will explain how well the models predicted the synthetic categories, where they made mistakes, and why the results should not be treated as conclusions about real workers or actual layoffs.

