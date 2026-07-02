# 📊 German Credit Risk Analysis

**A weighted, multi-factor credit risk scoring model built in Excel to classify loan applicants by risk level.**

This project analyzes 1,000 real-world loan applicant records to design and implement an independent credit risk scoring framework — assigning each applicant a weighted risk score and classifying them into **High**, **Medium**, or **Low** risk categories based on their financial and demographic profile.

---

## 📌 Project Motivation

Credit risk assessment is a core function in retail and consumer banking — lenders need a systematic, defensible way to estimate the likelihood that a borrower will default. Publicly available "labeled" risk datasets often hide the scoring logic entirely, which limits what can actually be learned from them.

This project takes the opposite approach: starting from **raw, unlabeled applicant data** (the [UCI/Kaggle German Credit Risk dataset](https://www.kaggle.com/datasets/uciml/german-credit)) and **independently designing the risk scoring methodology from scratch** — including component selection, normalization, weighting, and category thresholds — to mirror how a risk analyst would approach an unscored portfolio.

---

## 🎯 Objectives

- Clean and prepare a real-world applicant dataset containing missing and categorical data
- Design a transparent, multi-factor risk scoring model (not a black-box classifier)
- Score and classify 1,000 applicants into risk tiers
- Surface portfolio-level insights: risk distribution, spending behavior by risk tier, and loan purpose trends
- Build the entire model as a **live, dynamic Excel workbook** — not static output — so assumptions can be adjusted and results recalculate instantly

---

## 🧮 Methodology

### Dataset
1,000 loan applicant records with the following attributes: Age, Sex, Job skill level, Housing status, Savings account level, Checking account level, Credit amount, Loan duration, and Loan purpose.

**Data cleaning:** ~18% of records were missing a "Savings account" value and ~39% were missing "Checking account" data. Rather than dropping these rows (which would have removed a significant share of the dataset), missing values were encoded as a distinct `"none"` category — treated as a neutral, mid-range signal in the scoring model rather than assumed-good or assumed-bad.

### Risk Scoring Model
Each applicant is scored on five weighted components, each normalized to a 0–100 **"strength"** scale (100 = financially strongest):

| Component | Weight | Logic |
|---|---|---|
| **Loan Burden** (Credit Amount ÷ Duration) | 30% | Higher monthly repayment burden lowers the strength score |
| **Savings Account Level** | 25% | Categorical strength mapping (rich → strongest, little/none → weakest) |
| **Checking Account Level** | 20% | Categorical strength mapping |
| **Job Skill Level** | 15% | Higher-skilled employment mapped to greater income stability |
| **Housing Stability** | 10% | Home ownership treated as more stable than renting |

```
Weighted Score = (Loan Burden Strength × 30%) + (Savings Strength × 25%)
               + (Checking Strength × 20%) + (Job Strength × 15%)
               + (Housing Strength × 10%)
```

**Risk Category thresholds:**
| Score Range | Category |
|---|---|
| 0 – 33 | High Risk |
| 34 – 66 | Medium Risk |
| 67 – 100 | Low Risk |

All weights, category mappings, and thresholds are stored as **editable input cells** (not hardcoded into formulas), so the model can be re-tuned and instantly recalculated.

---

## 🛠️ Tools & Techniques

- **Microsoft Excel** — full workbook built with linked, dynamic formulas (`VLOOKUP`, `AVERAGEIF`, `COUNTIF`), not static hardcoded values
- **Conditional formatting** to visually flag risk categories
- **Pivot-style summary tables** and native Excel charts (pie and bar) for portfolio-level insights
- Model structured across separate **Data / Assumptions / Scoring / Dashboard** layers — a standard financial-modeling convention that separates raw inputs from logic and outputs

---

## 📂 Workbook Structure

| Sheet | Purpose |
|---|---|
| **Summary Dashboard** | Portfolio-level KPIs, risk distribution chart, average profile by risk tier, loan purpose breakdown |
| **Assumptions** | All model weights, strength-score lookup tables, and risk thresholds — fully editable |
| **Risk Scoring** | Row-by-row applicant scoring with live formulas referencing Raw Data and Assumptions |
| **Raw Data** | Cleaned source dataset (1,000 applicants) |

---

## 🔑 Key Findings

- Of 1,000 applicants, **2.3% scored as High Risk**, **85.4% as Medium Risk**, and **12.3% as Low Risk** — the model produces a realistic, non-extreme distribution rather than clustering applicants at the tails.
- **High-risk applicants carry the largest average loan amounts** (~$5,516) but over the **shortest average duration** (~11 months) — a combination of high principal and compressed repayment timelines that materially raises monthly repayment burden, the single largest driver in the model.
- Low-risk applicants borrow smaller amounts on average (~$2,048) despite similar loan durations to the medium-risk group — suggesting loan sizing, not just duration, is a key differentiator of risk in this portfolio.
- **Car loans (337)** and **radio/TV purchases (280)** are the two most common loan purposes, together accounting for over 60% of all applications.

---

## 💡 What This Project Demonstrates

- Ability to design a **from-scratch scoring methodology** rather than relying on a pre-labeled target variable
- Careful handling of **missing/incomplete real-world data** without simply discarding it
- Building **auditable, formula-driven financial models** in Excel — an industry-standard skill in risk, banking, and financial analytics roles
- Translating a raw dataset into **decision-relevant portfolio insights**, not just a technical exercise

---

## 📁 Files

| File | Description |
|---|---|
| `German_Credit_Risk_Analysis.xlsx` | Full working Excel model — Dashboard, Assumptions, Risk Scoring, and Raw Data sheets |

---

*Dataset source: German Credit Risk dataset (Kaggle/UCI Machine Learning Repository), used for independent educational analysis.*
