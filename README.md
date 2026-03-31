# 📊 Applied Statistics — AIML Module Project

> A comprehensive applied statistics project covering probability distributions, EDA, and hypothesis testing across three distinct domains: **Probability Theory**, **Sports Analytics (Basketball)**, and **Startup Ecosystem Analysis**.

---

## 📁 Project Structure

```
applied-statistics-project/
│
├── applied_statistics_project.ipynb   # Main Jupyter Notebook
├── applied_statistics_project.html    # HTML export of the notebook
├── Basketball.csv                     # Dataset for Part B (61 teams × 13 features)
├── CompanyX_EU.csv                    # Dataset for Part C (662 startups × 6 features)
└── README.md
```

---

## 🗂️ Project Overview

This project is divided into **three parts**, each targeting a different real-world domain:

| Part | Domain | Marks |
|------|--------|-------|
| Part A | Probability & Distributions | 15 |
| Part B | Sports Analytics (Basketball) | 30 |
| Part C | Startup Ecosystem Analysis | 15 |
| **Total** | | **60** |

---

## 📌 Part A — Probability & Distributions (15 Marks)

Covers fundamental probability and distribution concepts applied to real-world scenarios.

### Questions Covered:

**Q1 — Joint & Conditional Probability**
Using a purchase intent vs. actual order contingency table (n = 2,000):

| Planned to Purchase | Ordered: Yes | Ordered: No | Total |
|---------------------|-------------|-------------|-------|
| Yes | 400 | 100 | 500 |
| No | 200 | 1300 | 1500 |
| **Total** | 600 | 1400 | 2000 |

- **1.A** — Joint probability: planned *and* placed an order
- **1.B** — Conditional probability: placed an order *given* they planned to purchase

**Q2 — Binomial Distribution** *(Electrical Manufacturing — 5% failure rate, n = 10)*
- P(no defective items)
- P(exactly one defective)
- P(two or fewer defective)
- P(three or more defective)

**Q3 — Poisson Distribution** *(Car salesman — avg. 3 cars/week)*
- P(selling at least one car in a week)
- P(selling 2 or more but fewer than 5 cars)
- Cumulative Poisson distribution plot: cars/week vs. cumulative probability

**Q4 — Binomial / Bernoulli** *(Speech bot — 86.8% recognition accuracy, n = 3 orders)*
- P(all three orders recognised correctly)
- P(none of the three orders recognised correctly)
- P(at least two orders recognised correctly)

**Q5 — Real-Life Industry Scenario**
An original industry use case applying Applied Statistics concepts for a data-driven business solution.

---

## 🏀 Part B — Sports Analytics: Basketball (30 Marks)

**Domain:** Sports  
**Context:** Company X manages the men's top professional basketball division of the American league system and wants to identify the best teams to approach for investment partnerships.

### Dataset: `Basketball.csv`

- **Rows:** 61 teams  
- **Columns:** 13 features  
- **Missing values:** None (but requires cleaning — see notes below)

| Column | Description | Notes |
|--------|-------------|-------|
| `Team` | Team name | e.g., Team 1, Team 2 |
| `Tournament` | Tournaments played | — |
| `Score` | Cumulative score | ⚠️ Contains `'-'` placeholders |
| `PlayedGames` | Total games played | ⚠️ Contains `'-'` placeholders |
| `WonGames` | Games won | ⚠️ Contains `'-'` placeholders |
| `DrawnGames` | Games drawn | — |
| `LostGames` | Games lost | — |
| `BasketScored` | Total baskets scored | — |
| `BasketGiven` | Baskets conceded | — |
| `TournamentChampion` | Championship titles won | — |
| `Runner-up` | Runner-up finishes | — |
| `TeamLaunch` | Year team was founded | ⚠️ Inconsistent formats: `1929`, `1931to32`, `1934-35`, `1944_45` |
| `HighestPositionHeld` | Best tournament ranking | — |

> ⚠️ **Data Cleaning Note:** `Score`, `WonGames`, and `PlayedGames` columns contain `'-'` placeholder values that must be handled. `TeamLaunch` has inconsistent year formats (`to`, `-`, `_` separators) requiring standardisation before analysis.

### Tasks:
1. **Data Cleaning & Preparation** — Handle mixed-type columns, standardise `TeamLaunch`, engineer derived features (e.g., win rate, basket differential)
2. **EDA (Univariate, Bivariate, Multivariate)** — Statistical analysis and interactive visualisations to identify:
   - Best performing teams (win rate, championship count)
   - Oldest teams by `TeamLaunch`
   - Highest basket scorers and best defensive teams
   - Custom derived metrics: Win%, Basket Differential, Titles per Tournament, etc.
3. **Data Quality Recommendations** — At least one suggestion each on quality, quantity, variety, velocity, and veracity of data

---

## 🚀 Part C — Startup Ecosystem Analysis (15 Marks)

**Domain:** Startup Ecosystem  
**Context:** Company X (EU tech publisher) hosts the *Startup Battlefield* competition. This analysis evaluates startup performance, funding patterns, and survival rates.

### Dataset: `CompanyX_EU.csv`

- **Rows:** 662 startups  
- **Columns:** 6 features  
- **Missing values:** `Product` (6 nulls), `Funding` (214 nulls — ~32%)

| Column | Description | Unique Values / Notes |
|--------|-------------|----------------------|
| `Startup` | Company name | — |
| `Product` | Product / website | 6 missing values |
| `Funding` | Funds raised in USD | ⚠️ String format: `$630K`, `$1M`, `$19.3M`, `$1.8B` — needs numeric conversion |
| `Event` | Competition event | e.g., `Disrupt SF 2013`, `TC50 2009`, `Disrupt Beijing 2011` |
| `Result` | Competition outcome | Contestant (488), Finalist (84), Audience choice (41), Winner (26), Runner up (23) |
| `OperatingState` | Current company status | Operating (465), Closed (106), Acquired (86), IPO (5) |

> ⚠️ **Data Cleaning Note:** `Funding` is stored as a string with currency symbols and K/M/B suffixes. Convert to a numeric `Funds_in_million` column using:
> ```python
> df1.loc[:,'Funds_in_million'] = df1['Funding'].apply(
>     lambda x: float(x[1:-1])/1000 if x[-1] == 'K'
>     else (float(x[1:-1])*1000 if x[-1] == 'B'
>     else float(x[1:-1]))
> )
> ```

### Tasks:
1. **Data Exploration** — Datatypes inspection, null value audit
2. **Data Preprocessing & Visualisation**
   - Drop null rows
   - Convert `Funding` → `Funds_in_million` (numeric)
   - Box plot for `Funds_in_million`
   - Count outliers above the upper fence (Q3 + 1.5×IQR)
   - Frequency count of `OperatingState` classes
3. **Statistical Analysis**
   - **Hypothesis Test 1:** Is there a significant difference in funds raised between *Operating* vs *Closed* companies? (t-test / Mann-Whitney U)
   - **Hypothesis Test 2:** Do *Winners* have a significantly higher operating rate than *Contestants*? (z-test for proportions)
   - **Filter:** Select events containing the `'disrupt'` keyword from 2013 onwards

---

## 🛠️ Tech Stack

- **Language:** Python 3.x
- **Notebook:** Jupyter Notebook
- **Libraries:**

```
pandas        # Data manipulation & cleaning
numpy         # Numerical operations
matplotlib    # Static plots
seaborn       # Statistical visualisations
plotly        # Interactive visualisations
scipy.stats   # Binomial, Poisson, t-test, Mann-Whitney
statsmodels   # Proportion z-test
```

---

## ⚙️ Setup & Usage

```bash
# Clone the repository
git clone https://github.com/<your-username>/applied-statistics-aiml-project.git
cd applied-statistics-aiml-project

# Install dependencies
pip install pandas numpy matplotlib seaborn plotly scipy statsmodels jupyter

# Launch the notebook
jupyter notebook applied_statistics_project.ipynb
```

---

## 📈 Key Insights (Summary)

- **Part A:** The speech bot's 86.8% per-order accuracy translates to only ~65.5% chance of all three orders being simultaneously correct — a compelling case for accuracy improvement.
- **Part B:** `Basketball.csv` has 61 teams with no null values but requires cleaning: `Score`, `WonGames`, and `PlayedGames` contain `'-'` placeholders, and `TeamLaunch` has four different date formats. Post-cleaning, win rate and basket differential are the most discriminative metrics for identifying investment-worthy teams.
- **Part C:** ~32% of `Funding` values are missing in `CompanyX_EU.csv`, limiting statistical power for funding-based tests. Winners (26 companies) show a notably higher survival/operating rate compared to the 488 general contestants, supported by proportion hypothesis testing.

---

## 📋 Submission Checklist

- [x] `.ipynb` notebook with all code, outputs, and markdown explanations
- [x] `.html` export of the notebook
- [x] All code cells have visible outputs
- [x] Insights and steps documented for every question
- [x] No plagiarism

---

## 📄 License

This project was completed as part of the **Great Learning AIML Programme** coursework.  
Dataset credits go to the original creators. Educational use only.

---

*Made with 📊 and Python*
