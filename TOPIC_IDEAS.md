DATS 6103 / FALL 2026 / TEAM DECISION DRAFT
# AI Exposure and Simulated Layoff Risk

**LOWER DATA RISK | SYNTHETIC OBSERVATIONS**

**THE ONE-LINE QUESTION** Can job characteristics and AI-automation measures classify a simulated
worker profile as low, medium, or high layoff risk?

**TEAM** Mak Trnka | Galileo Frank Perricone | Miguel Sanchez Zanella

## 01 THE QUESTION
**Prediction:** The target is ***Layoff_Risk (Low / Medium / High)***. For a data-mining instructor or workforce researcher
testing methods, the decision is ***whether an interpretable classifier or a flexible ensemble better recovers patterns in
simulated AI-exposure data***. This is not a tool for actual personnel decisions.

## 02 THE DATA
Download the linked Kaggle CSV and save a fixed copy in data/raw/. Published size: 20,000 rows x 16 columns; each
row is one synthetic employee/job profile. Fields include industry, role, company size, routine-task share, AI
adoption, automated tasks, and training hours. The file lacks observed job losses, identifiable employers, and
validated economic conditions. Main obstacle: the target labels are synthetic and may follow a simple, invented
scoring rule.

## 03 EXPLORATION
Audit duplicates, missingness, categorical levels and risk-class balance; plot distributions of routine-task share and
automated-task share by class, plus AI-adoption and industry cross-tabs. Examine whether any single variable nearly
determines the label before modeling.

## 04 MODELING
Compare ***multinomial logistic regression*** (interpretable effects) with a ***random forest*** (nonlinear interactions),
against a majority-class baseline. Use an 80/20 stratified split, cross-validation, and preprocessing fitted on training
folds only. Evaluate macro-F1 and a confusion matrix.

## 05 ACCOUNT OF THE FINDINGS
Produce a reproducible written report and a short oral presentation with EDA plots, model comparison, errors by
class, and sensitivity to dominant features. The conclusion can establish performance within the synthetic dataset
only, not actual AI-caused layoffs or a worker's real risk.

**DATASET LINK Kaggle:** [AI Impact on Jobs and Layoff Risk Dataset](https://www.kaggle.com/datasets/shivasingh4945/ai-impact-on-jobs-and-layoff-risk-dataset)
Source counts are published descriptions and will be checked against the downloaded CSV before submission.
