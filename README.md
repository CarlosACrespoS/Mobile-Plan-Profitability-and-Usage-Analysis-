📱 Megaline Plan Profitability & Usage Analysis


![Python](https://img.shields.io/badge/Python-3.12-blue) ![Pandas](https://img.shields.io/badge/Pandas-Data%20Engineering-150458) ![SciPy](https://img.shields.io/badge/SciPy-Statistical%20Inference-8CAAE6) ![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)

An end-to-end billing-engine reconstruction and statistical validation pipeline evaluating tariff-plan profitability, customer usage segmentation, and regional revenue performance for Megaline, a prepaid telecom operator.

## 📌 Executive Summary & Strategic Wrap-Up

### 📝 Executive Overview
This project rebuilds Megaline's actual monthly billing logic from five raw transactional sources — calls, messages, internet sessions, user profiles, and plan catalogs — to calculate real revenue per user, then puts every resulting claim through formal statistical validation. The analysis deliberately goes past the surface-level "which plan wins" question: it separates *which plan wins on average* from *where the untapped revenue actually is*, cross-checks the story against churn and demographic data, and documents a correction to an initial directional assumption about the NY-NJ market — a decision-relevant error caught and fixed within this same analysis.

### ⚡ Analysis Phase-by-Phase Flashback
- **Phase 1 (Data Sanitization & Temporal Alignment):** Converted 4 date fields to native `datetime`, extracted the `month` component for monthly billing aggregation, and standardized `user_id` typing across all tables.
- **Phase 2 (Business Logic & Feature Engineering):** Applied Megaline's per-minute rounding policy, aggregated calls/SMS/data by user-month, converted MB to GB, and merged everything into a single 2,293-record master dataframe.
- **Phase 3 (Revenue Engineering):** Implemented a row-wise billing function replicating the real fixed-fee + overage structure to produce a `total_revenue` figure per user, per month.
- **Phase 4 (Behavioral Storytelling & Visual Analytics):** Built consumption bar charts, usage boxplots, and a revenue-distribution boxplot comparing both plans — establishing that Ultimate has essentially no internal spread to explore, while Surf's distribution is wide and right-skewed.
- **Phase 5 (Revenue Efficiency & Customer Segmentation):** Quantified revenue-per-GB and revenue-per-minute by plan, isolated Surf's heavy-usage tail, cross-checked it against churn (chi-square), and tested whether age predicts revenue.
- **Phase 6 (Hypothesis Testing & Statistical Validation):** Ran Levene's test + independent t-tests (with explicit effect direction, not just significance) on both the plan comparison and the regional comparison.
- **Phase 7 (Executive Conclusions & Business Impact):** Converted every validated statistical result into a specific, actionable commercial recommendation — including a documented correction of the original NY-NJ conclusion.

### 💡 Key Insights & Business Value
- **Ultimate is the real ARPU leader, not Surf:** average revenue per user is **$72.31 (Ultimate) vs. $60.71 (Surf)**, confirmed via Welch's t-test (P ≈ 0.0000). Ultimate is also more revenue-efficient per unit of usage — **$4.18/GB and $0.168/min vs. Surf's $3.64/GB and $0.142/min.**
- **Surf's value is a segment, not the whole plan:** just **25.3% of Surf's billing months generate 56.2% of its total revenue.** That heavy-usage tail — identifiable in real time via `gb_used` (r = 0.779 with revenue) — is the actual commercial opportunity, not the average Surf user.
- **A directional finding was corrected mid-project:** an earlier pass of this analysis assumed the **NY-NJ** market was Megaline's highest-value region. The validated result is the opposite — **NY-NJ underperforms the rest of the country by ~$5.30/user-month (P = 0.0436)** — which flips the original infrastructure-investment recommendation from "invest" to "investigate."
- **Not every tested variable was a finding, and that's reported honestly:** age shows no relationship with revenue (r = 0.037), and churn shows no significant difference between heavy and non-heavy Surf users (chi-square P = 0.83, sample too small to support a retention claim).

### 🚀 Proactive Recommendations & Strategic Action Plan

| 💰 Plan Strategy | 🎯 Growth & Targeting | 📍 Market Investment |
|---|---|---|
| Lead acquisition marketing with **Ultimate** — higher, more predictable ARPU and better revenue-per-unit efficiency. | Build a real-time upsell trigger on `gb_used` to catch Surf users approaching the heavy-tier threshold ($80/mo) before they hit overage. | Do **not** commit infrastructure or marketing budget to NY-NJ on a "high-value market" premise — that premise is factually wrong per this analysis. |
| Price and position Surf as a flexible entry plan, not a revenue-maximizing one. | Trigger upsell messaging on consumption behavior, not demographics — age has no predictive value (r = 0.037). | Commission a market-level study (competitor pricing/coverage) to explain NY-NJ's underperformance before any investment decision. |
| Justify heavy-tier retention offers on revenue stabilization, not on an unsupported churn-reduction claim. | Extend the churn analysis with a longer observation window — the current 34-event sample is too small for a standalone churn model. | Re-run the regional test on future data to confirm the NY-NJ gap is structural, not a one-time artifact. |

### 📊 Target Business KPIs & Expected Impact

| Strategic Initiative | Primary Target KPI | Statistical Basis |
|---|---|---|
| Surf Heavy-Tier Upsell Trigger | Conversion of Surf → Ultimate/mid-tier among users crossing $80/mo | 25.3% of Surf billing months = 56.2% of Surf revenue; `gb_used` r = 0.779 with revenue |
| Ultimate-Led Acquisition Push | ARPU growth via acquisition-channel mix | ARPU gap of $11.60/user-month, P ≈ 0.0000, Welch's t-test |
| NY-NJ Market Investigation | Root-cause diagnosis before any budget allocation | Regional ARPU gap of −$5.30/user-month, P = 0.0436, Student's t-test |

### 🗂 Project Repository Details
- **Repository Slug:** `mobile-plan-profitability-and-usage-analysis`
- **Primary Goal:** Determine which Megaline tariff plan (Surf or Ultimate) generates more revenue, whether that answer changes by region, and where the real untapped revenue sits.
- **Key Achievements:**
  - **Billing Engine Reconstruction:** Rebuilt Megaline's exact fixed-fee + overage invoicing logic from 5 raw transactional tables into a reusable `calculate_revenue()` function.
  - **Self-Correcting Statistical Rigor:** Identified and corrected a directional error in the original NY-NJ regional finding, with the correction documented as part of the analysis rather than silently fixed.
  - **Actionable Segmentation:** Quantified and defined a specific, targetable high-value customer segment within the lower-ARPU plan, rather than stopping at a plan-level average.

## 💻 Tech Stack & Environment Settings
- **Language:** Python 3.12
- **Data Processing:** pandas, numpy
- **Statistical Inference:** scipy.stats (Levene's test, independent/Welch's t-test, chi-square test of independence)
- **Data Visualization:** matplotlib, seaborn
- **Environment:** Jupyter Notebook

## 📁 Repository Structure
```
mobile-plan-profitability-and-usage-analysis/
├── Mobile_Plan_Profitability_and_Usage_Analysis.ipynb   # Full analysis pipeline (executed, outputs included)
├── megaline_users.csv                                    # User profiles, plan, city, churn status
├── megaline_calls.csv                                     # Call logs
├── megaline_internet.csv                                  # Internet session logs
├── megaline_messages.csv                                  # SMS logs
├── megaline_plans.csv                                      # Plan catalog (rates, included allowances)
├── requirements.txt                                       # Reproducible environment dependencies
├── README.md
└── .gitignore                                              # Excludes venv/ and generated chart images
```

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/CarlosACrespoS/mobile-plan-profitability-and-usage-analysis

# Navigate to the project directory
cd mobile-plan-profitability-and-usage-analysis

# Create and activate a virtual environment (recommended)
python -m venv venv_megalin
source venv_megalin/bin/activate   # Windows: venv_megalin\Scripts\activate

# Install required dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook Mobile_Plan_Profitability_and_Usage_Analysis.ipynb
```
