# Disney-segment-financial-reporting

A relational database modeling Disney's three business segments — **Entertainment**, **ESPN**, and **Experiences** — built to demonstrate cross-segment financial analysis using SQL.

---

## Overview

This project simulates the kind of segment-level financial reporting an analyst at Disney would work with on a recurring basis. The database is structured around Disney's actual reported segment taxonomy and populated with synthetic data approximated from Disney's public 10-K annual filings and quarterly earnings releases (FY2021–FY2023).

The goal was to build a clean, query-ready data model that mirrors how segment P&L data is structured in enterprise financial systems, and to write SQL that produces the reports a financial planning and analysis team would actually use.

---

## Database Schema

Four tables connected by foreign key relationships:

| Table | Description |
|---|---|
| `segments` | Disney's three business segments |
| `fiscal_periods` | Quarterly periods from FY2021 through FY2023 |
| `revenue` | Revenue by segment, period, and revenue type |
| `operating_expenses` | Expenses by segment, period, and expense category |

**Revenue types by segment:**
- Entertainment: Subscription, Advertising, Licensing & Other
- ESPN: Affiliate, Advertising, Other
- Experiences: Theme Parks, Consumer Products, Cruises & Other

**Expense categories by segment:**
- Entertainment: Content Costs, SG&A, Tech & Infrastructure
- ESPN: Programming Rights, SG&A, Production Costs
- Experiences: Park Operations, SG&A, Cost of Sales

---

## Queries

### 1. Total revenue by segment and quarter
Aggregates revenue across all revenue types to produce a quarterly top-line view for each segment.

### 2. Annual operating income by segment
Calculates revenue minus operating expenses per segment per fiscal year, producing a simplified segment P&L summary.

### 3. Segment share of total company revenue
Uses a window function (`SUM ... OVER PARTITION BY`) to compute each segment's percentage contribution to total Disney revenue by year — useful for tracking how the revenue mix shifts over time.

### 4. Year-over-year revenue change by segment
Uses `LAG()` to compare each segment's annual revenue against the prior year, surfacing growth trends across the three-year window.

---

## Tools

- **SQLite3** — database engine
- **DB Browser for SQLite** — optional GUI for exploring results
- **SQL** — all queries written in standard SQLite-compatible syntax

---

## Data Sources

Revenue and expense figures are synthetic values approximated from Disney's publicly available financial disclosures:
- Disney Annual Reports (10-K filings) — [SEC EDGAR](https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=DISNEY&type=10-K)
- Disney Investor Relations — [thewaltdisneycompany.com/investor-relations](https://thewaltdisneycompany.com/investor-relations/)

Figures are rounded and simplified for modeling purposes and are not intended to replicate exact reported values.

---

## How to Run

**Option 1 — Terminal (macOS/Linux)**
```bash
sqlite3 disney_reporting.db < disney_segment_reporting.sql
sqlite3 disney_reporting.db
```
Then paste any query from the bottom of the `.sql` file at the `sqlite>` prompt.

**Option 2 — DB Browser for SQLite**
1. Open DB Browser and create a new database
2. Go to Execute SQL and paste the full contents of `disney_segment_reporting.sql`
3. Run queries individually in the same tab

---

## Author

Rob Haldeman  
B.A. Economics, Rowan University — May 2026  
www.linkedin.com/in/roberthaldemanjr | haldemanrob@gmail.com
