Example of how to make the README template for this project, following our instructor's rules, to look like mine [https://github.com/Makster04/FINAL_CAPSTONE_PROJECT/blob/main/README.md]

Our instructors order:
It should cover, in roughly this order:
- the question, and the decision it informs
- where the data came from and what is missing from it
- what you did to the data, with reasons
- the models, the baseline, and how they were evaluated
- what the analysis does and does not support
- limitations specific to your data, not generic ones


# [Project Title]: [The Question Your Model Answers]

**DATS 6103 – Introduction to Data Mining · Team Project · Fall 2026**
**Team:** [Name 1] · [Name 2] · [Name 3]

📄 **Report:** [`report/report.html`](report/report.html)

---

## The Question

[One or two sentences: what is being predicted or discovered.]

- **For whom:** [who uses the answer]
- - Stakeholder #1
- - Stakeholder #2
- - Stakeholder #3
- **The decision it changes:** [what they would do differently with it]
- **The costlier mistake:** [which error matters more, and why]
- **Primary metric:** [Recall / F1 / PR-AUC / RMSE / MAE], chosen because [it reflects the costlier mistake]

---

## The Data

| | |
|---|---|
| **Source** | [Dataset name](link) |
| **How to get it** | [Committed in `data/raw/`] or [run `python src/get_data.py`] |
| **Size** | [N rows × M columns] |
| **One row is** | [one loan application / one patient visit / one county-year / …] |
| **Target** | `[column_name]` |

### What's missing from it
- [Who or what is not in the data: populations, time periods, variables you would want]
- [Missingness in key columns, and whether it looks random or systematic]

---

## Data Preparation

| Step | What we did | Why |
|------|-------------|-----|
| Train/test split | [80/20, stratified on target; or time-based if temporal] | [...] |
| Dropped columns | [IDs, post-outcome / leaky fields] | [...] |
| Missing values | [median imputation], fitted on training data only | [...] |
| Encoding / scaling | [one-hot, StandardScaler], fitted on training data only | [...] |
| Feature engineering | [...] | [...] |

All fitted steps sit inside a scikit-learn `Pipeline`, so they never see the test set.

---

## Exploration

- [Target distribution / class balance]
- [Strongest relationships with the target]
- [Anything that shaped the modeling choices]

---

## Models and Evaluation

### Baseline
[Majority class ("[class]") / mean of target] → [primary metric] = [x]

### Models
| Model | Why it suits the question |
|-------|---------------------------|
| [Model A] | [...] |
| [Model B] | [...] |

### Evaluation protocol
- Test set ([20]%) set aside before any fitting, and scored once at the end.
- Tuning by [5]-fold [stratified] cross-validation on the training set only.

---

## Results (test set)

| Model | [Primary metric] | Beats baseline? |
|-------|------------------|-----------------|
| Baseline | [ ] | — |
| [Model A] | [ ] | [Yes / No] |
| [Model B] | [ ] | [Yes / No] |

*Values are copied from the report, where they are computed.*

### What we tried and dropped
| Tried | Why we dropped it |
|-------|-------------------|
| [Model / feature / approach] | [...] |

---

## What the Analysis Does and Does Not Support

**Supports:** [The claim, at exactly the strength the test results carry.]

**Does not support:**
- [e.g., causal claims from observational data]
- [e.g., populations or periods absent from the data]

### Limitations
- [Specific to this dataset, not generic]

---

## How to Run

```bash
git clone https://github.com/[user]/[repo].git
cd [repo]
pip install -r requirements.txt
python src/get_data.py                      # skip if data/ is committed
jupyter nbconvert --to html --execute report/report.ipynb
# or, for Quarto: quarto render report/report.qmd
```

Python [3.11] · Random seed: `42`

---

## Repository Structure

```
├── data/
│   └── raw/
├── src/
│   └── get_data.py
├── report/
│   ├── report.ipynb      # or report.qmd — source of every number
│   └── report.html
├── requirements.txt
└── README.md
```

---

## AI Disclosure
[Level per the course's four-level standard, and what the assistant was used for.]
*or:* We did not use an AI assistant on this project.

---

## Conclusion
[Two or three sentences answering the question, stated only as strongly as the evidence allows.]
