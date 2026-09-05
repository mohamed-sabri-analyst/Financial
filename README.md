# Enterprise Financial Suite & Advanced DAX Analytics

A 4-page executive financial suite in Power BI, built from raw, uncleaned ERP/GL accounting data — diagnosing and fixing critical data-integrity flaws using an advanced, DAX-only cleansing layer.

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-1E2761?style=flat-square)
![Power Query](https://img.shields.io/badge/Power_Query-2E7D32?style=flat-square)

---

## 📌 Overview

Most "clean" portfolio dashboards start from tidy source data. This one doesn't. The brief was to take **raw ERP/GL export data** — the kind every real finance team actually has — and turn it into a bulletproof executive reporting suite, without touching the live source database.

## 🔍 Data Problems Diagnosed

Auditing the raw ledger surfaced 3 architectural flaws that broke standard reporting and corrupted KPI cards into negative/impossible values:

1. **Sign-convention conflicts** — Revenue, COGS, and OpEx were all recorded as positive numbers with no debit/credit distinction, causing Power BI to sum expenses into revenue and flip net profit negative.
2. **Budget allocation leakage** — The entire **$26.74M** corporate budget was journaled under a single placeholder category ("Other"), producing artificial 100% variances once filtered by department.
3. **Relational breaks** — Unmapped entity records created orphan data segments, flattening charts to ±100% due to severed relationships.

## 🛠 How It Was Fixed — Advanced DAX Architecture

Instead of editing the source database, a **programmatic data-cleansing layer** was built entirely in DAX:

- **Contextual sign inversion** — `SUMX` combined with conditional logic (`IF(AccountID IN {...}, ABS(), ABS()*-1)`) to correct accounting signs dynamically at query time.
- **Virtual data-bridge architecture** — `TREATAS` inside nested `CALCULATE` statements to bridge disjointed accounting dimensions without physical relationships.
- **Dynamic time-interval aging** — `DATEDIFF` tied to the data's own max date (not the system date) to correctly bucket receivables into aging tiers.
- **Cross-filter interaction anchoring** — recalibrated visual interactions so donut/matrix visuals respond correctly to executive-level slicers.

## 📊 Key Metrics

| Metric | Value |
|---|---|
| Total Revenue | $5.74M |
| Gross Margin | 65% |
| EBITDA | -$7.15M |
| Total Budget Modeled | $26.74M |
| Actual Spend | $26.65M |
| Budget Variance | -0.35% |
| Over-Budget Accounts | 24 |
| Ending Cash Balance | $26.65M |
| Cash Runway | 45.31 months |
| Total AR Outstanding | $1.27M |
| Days Sales Outstanding (DSO) | 30.47 days |
| Open Invoices | 204 |

## 🖥 Dashboard Pages

### 1. Executive P&L Overview
Revenue, margin, and EBITDA trends with an automated waterfall chart mapping the full gross-to-net conversion.

![Executive P&L Overview](screenshots/Executive_P_L_Overview.png)

### 2. Budget vs. Actual Variance Analysis
Fully-reconciled operational spend by department, isolating 24 over-budget accounts via dynamic color semiotics.

![Budget vs. Actual](screenshots/Budget_vs__Actual.png)

### 3. Cash Flow & Runway Tracking
Rolling cumulative ending cash balance and an automated cash-runway estimate for forward-looking liquidity planning.

![Cash Flow & Runway](screenshots/Cash_Flow___Runway.png)

### 4. AR Aging & Collections
Receivables bucketed into 0-30 / 31-60 / 61-90 / 91+ day aging tiers, with geographic risk concentration mapped by account.

![AR Aging & Collections](screenshots/AR_Aging___Collections.png)

## 🛠 Tools & Techniques

Power BI · DAX (`TREATAS`, `SUMX`, `AVERAGEX`, `SWITCH(TRUE())`, `ISINSCOPE`, `DATEDIFF`, `CALCULATE`) · Power Query · M-Code · Relational Modeling · Financial Modeling

## 👤 Author

**Mohamed Sabri Al-Deip** — MIS Analyst | Data Analyst | Power BI Developer
📧 m_sabry91@hotmail.com &nbsp;|&nbsp; 🔗 [LinkedIn](https://www.linkedin.com/in/mohamed-sabri-aldeip) &nbsp;|&nbsp; 🌐 [Portfolio](https://mohamed-sabri-analyst.github.io)
