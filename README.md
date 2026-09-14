# HR Workforce & Attrition Analysis — Geoflex Workforce Solutions

An end-to-end HR analytics case study: cleaning eight fragmented HR datasets, modeling them into a relational structure, and building an 8-page Power BI dashboard to answer real workforce questions for a fictional multinational staffing company operating in Nigeria and Kenya.

> **Portfolio project.** This is a self-directed / instructional case study built on a provided HR dataset, not professional work completed for a real employer. It's designed to mirror the kind of assignment a junior data analyst would receive on the job.

---

## Table of Contents

1. [Business Problem](#business-problem)
2. [Executive Summary](#executive-summary)
3. [Key Analytical Stories](#key-analytical-stories)
4. [Tech Stack & Tools](#tech-stack--tools)
5. [Data Preparation & Quality](#data-preparation--quality)
6. [Key Visuals](#key-visuals)
7. [Key Insights](#key-insights)
8. [Recommendations](#recommendations)
9. [Project Challenges](#project-challenges)
10. [Project Limitations](#project-limitations)
11. [Business Value](#business-value)
12. [Repository Structure](#repository-structure)

---

## Business Problem

Geoflex Workforce Solutions is a fictional staffing and workforce-outsourcing company with operations across Nigeria and Kenya. Between 2019 and 2025 it expanded rapidly — opening branches, hiring thousands of employees, and running recruitment and training programs — but employee data was stored across eight disconnected systems with no shared governance. By the time this project starts, those systems hold duplicate records, missing values, invalid contact details, and inconsistent formatting, which makes company-wide reporting unreliable.

The brief: act as a Junior Data Analyst, clean and integrate the data, and answer the questions leadership actually needs answered — where attrition is concentrated, which recruitment channels work, and which departments or branches need attention — before any of it can support real workforce decisions.

This project focuses specifically on **attrition, recruitment effectiveness, and branch/department performance**, since those are the questions the underlying business-question workbook and dashboard were built to answer.

---

## Executive Summary

**1. Attrition is concentrated, not evenly spread.**
Metric: 14.5% company-wide attrition (362 of 2,500 employees), ranging from 7.4% (Ilorin branch) to 23.1% (Busia branch), and from 13.3% (Supply Chain) to 18.3% (Customer Service) by department.
Insight: the headline rate hides a wide spread — a handful of units run well above average.
Implication: a blanket retention program would waste effort; the data supports targeting specific departments and branches first.

**2. Organic recruitment sources convert candidates better than paid job boards.**
Metric: Walk-In (28.0%) and Campus Recruitment (17.9%) hire rates vs. Job Portal (14.2%) and Indeed (12.5%), measured across sources with 950+ applicants each for the high-volume comparison.
Insight: at comparable scale, free/organic and campus-based channels are converting applicants into hires more efficiently than paid boards.
Implication: recruitment spend may be worth reviewing against these conversion rates.

**3. A large share of recorded exits cluster early — and a further share carry literal negative tenure values.**
Metric: 100 of 362 exits (28%) are recorded in the 0–1 year tenure bucket; a further 148 (41%) fall into a "<0" bucket, meaning the dataset records a negative tenure (an exit date before the hire date) for those employees.
Insight: early attrition looks like a genuine pattern, and the negative-tenure records are a data-validation catch worth flagging separately rather than folding into one combined percentage.
Implication: this is presented as two separate findings, not one polished number — see [Story 3](#3-a-large-share-of-recorded-exits-cluster-in-year-one--and-a-further-share-carry-literal-negative-tenure-values) below.

No financial savings, cost figures, or operational improvements are claimed anywhere in this project — the source data doesn't include payroll cost-per-hire, engagement scores, or exit-interview detail needed to calculate them.

---

## Key Analytical Stories

### 1. Attrition Risk Is Concentrated in Specific Branches and Departments, Not Spread Evenly

**Situation**
Leadership had one company-wide attrition figure (14.5%) and no visibility into whether it was evenly distributed across Geoflex's 40 branches and multiple departments, which made it impossible to know where a retention response would actually help.

**Task**
The objective was to determine whether attrition was concentrated in specific parts of the business, and if so, where.

**Action**
I compared attrition rate by department and by branch inside Power BI rather than relying on the single blended average. I checked branch headcounts (65–83 employees each for the branches in question) to confirm the comparison wasn't distorted by small-sample branches. I ranked departments and branches from highest to lowest attrition, then cross-referenced the outliers against the ExitReason breakdown to see whether voluntary or involuntary departures explained the gap.

**Result**
Customer Service (18.3%) and Administration (17.9%) run 3.4–3.8 percentage points above the 14.5% company average. Busia, Kenya (23.1%) and Lokoja, Nigeria (21.2%) run 6.7–8.6 points above their peer branches. Supply Chain (13.3%) and Ilorin branch (7.4%) sit well below. **Finding:** attrition is not a company-wide problem. **Evidence:** a 15.7-point spread across branches and a 5-point spread across departments. **Implication:** retention resources are better spent on these four specific units first, rather than a blanket initiative.

---

### 2. Free and Referral-Based Recruitment Sources Convert Candidates at Nearly Double the Rate of Paid Job Boards

**Situation**
Geoflex recruits through eight channels — Walk-In, Referral, Campus Recruitment, Company Website, LinkedIn, Job Portal, Indeed, and an unspecified "NIL" source — with no documented comparison of how efficiently each one converts applicants into hires.

**Task**
I set out to determine which recruitment sources converted applicants most efficiently, to see whether recruiting effort was aligned with results.

**Action**
I calculated a hire rate (Total Hired ÷ Total Applicants) for each source rather than using raw hire counts, since raw counts reward volume over efficiency. I separated the five high-volume sources (Campus Recruitment, Company Website, Referral, LinkedIn, Job Portal — each with 950–1,020 applicants) from the low-volume ones (Walk-In, NIL, Indeed — each under 35 applicants), so a 5-hire sample wasn't compared directly against a 175-hire sample. I then ranked all eight sources by hire rate and checked whether the pattern held at scale.

**Result**
Among the high-volume channels, Campus Recruitment (17.9%) and Company Website (17.3%) convert meaningfully better than Job Portal (14.2%) and Indeed (12.5%) — a 3–5 point gap between channels of comparable size. **Finding:** organic and campus-based sourcing outperforms paid job-board sourcing at scale. **Evidence:** the gap holds even after excluding the small-sample sources. **Implication:** this is worth investigating further — including a cost-per-hire comparison this dataset doesn't include — before the next recruiting budget cycle.

---

### 3. A Large Share of Recorded Exits Cluster in Year One — But Nearly Half the Exit Records Contain a Tenure Data Error

**Situation**
The ExitRecords table includes a tenure-at-exit breakdown, normally used to tell whether attrition is an onboarding problem or a longer-term retention problem.

**Task**
The analysis focused on understanding when, in an employee's tenure, exits were most likely to happen — and on confirming the underlying tenure data could actually be trusted before drawing that conclusion.

**Action**
I reviewed the exit tenure distribution and found a "<0" (negative) tenure category holding 148 of 362 records (41%) — a value that isn't logically possible, since it implies an exit date recorded before the hire date. Rather than fold this into the headline number, I flagged it as a data-integrity issue, consistent with the kind of date-logic checks the project's own data-validation questions (checking for leave requests where an end date precedes a start date, for example) were designed to catch elsewhere in the dataset. I reviewed the 0–1 year bucket (100 records) separately, since those values are logically valid.

**Result:** 100 of 362 exits (28%) are confirmed early exits within the first year. A further 148 records (41%) can't currently be trusted due to the tenure error. **Finding:** early attrition is a plausible real pattern, but the data can't yet support a single combined "68% of exits happen early" figure with full confidence. **Evidence:** the "<0" bucket is a logical impossibility, not just an outlier. **Implication:** this needs two responses — a first-year retention review for the confirmed cases, and a date-validation pass on ExitRecords for the flagged ones.

---

## Tech Stack & Tools

- **Microsoft Excel** — initial data inspection, duplicate and missing-value audits, and exploratory checks across all 8 source tables.
- **Power Query** — data cleaning and transformation: removing duplicates, standardizing text case, trimming whitespace, filling blank fields, and standardizing date formats.
- **Power BI** — data modeling across the 8 related tables, DAX measures, and the 8-page interactive dashboard.
- **DAX** — calculated measures behind the dashboard KPIs (attrition rate, hire rate by source, training completion rate, attendance/present rate, payroll totals and averages, year-over-year headcount growth).
- **MySQL** — database and table creation, primary/foreign key relationships, and SQL queries (JOINs, ranking, aggregation) to answer the department- and branch-level ranking questions defined in the project brief (e.g., ranking employees by salary within department, ranking branches by performance).

No other tools (Python, Tableau, R, etc.) were used in this project.

---

## Data Preparation & Quality

**Source data:** 8 tables extracted from legacy HR systems — `Employees`, `Attendance`, `ExitRecords`, `Recruitment`, `Promotions`, `TrainingRecords`, `PerformanceReviews`, `LeaveRequests`.

**Duplicate records identified and removed:**

| Table | Duplicates Removed | Unique Records Remaining |
|---|---|---|
| Employees | 25 | 2,515 |
| Attendance | 497 | 912,503 |
| ExitRecords | 30 | 362 |
| Recruitment | 120 | 5,000 |
| Promotions | 50 | 730 |
| TrainingRecords | 100 | 6,201 |
| PerformanceReviews | 151 | 17,499 |
| LeaveRequests | 80 | 5,005 |

**1,053 duplicate records removed in total, across all 8 tables, before any analysis began.**

**Missing / invalid values (Employees table):**
- Department_ID missing in 80 records (3.2%)
- Email missing in 78 records (3.1%)
- Phone missing in 87 records (3.5%)

Note: the "invalid email" and "invalid phone" figures in the source workbook match the missing-value counts exactly (78 and 87), which indicates blank fields were being treated as invalid rather than as a separate category of malformed data. I've reported them as one issue rather than stacking the counts.

**Cleaning actions performed:**
- Removed duplicate rows across all 8 tables.
- Standardized employee names to Proper Case and trimmed stray whitespace from every text column.
- Filled missing Department IDs using available lookup information where a match existed.
- Used fill-down for blank cells in sequential fields, and used explicit "Nil" / "Unknown" placeholders only where no real value could be identified — this is visible in the final dashboard (22 recruitment records tagged "NIL" source, 12 employees tagged "Unknown" employment status), rather than being silently dropped or guessed.
- Standardized every date column to one consistent format.
- Validated employee-branch assignments, payroll completeness, attendance value ranges, and leave date logic (start date before end date).

**Data model:** the 8 tables are linked at the employee level through a shared `EmployeeID`, with Department and Branch used as lookup dimensions. This relationship structure is what supports the dashboard's cross-table views — for example, filtering attrition rate by department, or drilling from a branch summary into an individual Employee Profile page.

---

## Key Visuals

The dashboard is built as 8 linked Power BI pages. Screenshots for each are in [`/images`](./images).

### Executive Overview
![Executive Overview](images/executive-overview.png)
The landing page: total headcount (2,500, +16.8% YoY), active employees, total promotions, applicant volume, and the headline attrition rate (14.5%). Also shows workforce split by country (63.8% Nigeria / 36.2% Kenya) and the top 5 departments by headcount. **Takeaway:** the company is growing, but the attrition number here is a starting point, not the full picture — see the Attrition Analysis page for where it's concentrated.

### Administration Dashboard
![Administration Dashboard](images/administration-dashboard.png)
Attendance and leave operations: 913K total attendance records, 5,005 leave requests (60.6% approval rate), and $5.83M total payroll across departments. **Takeaway:** Marketing and Sales carry the two highest department payroll totals company-wide.

### Talent Acquisition
![Talent Acquisition](images/talent-acquisition.png)
The recruitment funnel (5,000 applicants → 817 hired) and a hire-rate breakdown by source. **Takeaway:** this is the page behind [Story 2](#2-free-and-referral-based-recruitment-sources-convert-candidates-at-nearly-double-the-rate-of-paid-job-boards) — Walk-In and Campus Recruitment convert best.

### Development & Performance
![Development & Performance](images/development-performance.png)
Training completion (60.8% overall, 58.8%–66.5% by department) and performance review scores (average 75.1 out of 150). **Takeaway:** completion and performance scores are unusually flat across departments — see [Key Insights](#key-insights).

### Attrition Analysis
![Attrition Analysis](images/attrition-analysis.png)
The core attrition view: 14.5% rate, 362 exits, attrition by department, exit reasons, and the exit-tenure breakdown. **Takeaway:** this is the most important page in the dashboard — it's the source for both [Story 1](#1-attrition-risk-is-concentrated-in-specific-branches-and-departments-not-spread-evenly) and [Story 3](#3-a-large-share-of-recorded-exits-cluster-in-year-one--but-nearly-half-the-exit-records-contain-a-tenure-data-error).

### Branch Comparison
![Branch Comparison](images/branch-comparison.png)
All 40 branches ranked by headcount, attendance, attrition, and payroll, with a performance/salary/absence scatter view. **Takeaway:** Busia and Lokoja stand out as attrition outliers here, and the payroll scale difference between Kenya and Nigeria branches is visible on this page too.

### Employee Demographics
![Employee Demographics](images/employee-demographics.png)
Workforce composition by work mode, age group, hire year, and employment status. **Takeaway:** the employment-status split (only 400 of 2,500 marked "Active") is the source of one of the data-governance flags in [Key Insights](#key-insights).

### Employee Profile
![Employee Profile](images/employee-profile.png)
A drill-through, row-level employee directory (ID, department, branch, role, hire date, status). **Takeaway:** this page demonstrates the dashboard's relational structure — it pulls consistently from every linked table for a single employee.

**Strongest screenshots to lead with in the repo:** Executive Overview, Attrition Analysis, Talent Acquisition, and Branch Comparison — these four carry the findings referenced in the analytical stories above.

---

## Key Insights

- Training completion (58.8%–66.5%) and average performance score (74.4–75.5 out of 150) barely vary across 12 departments, suggesting the training content and/or the performance-review scale may not currently be differentiating department-level performance.
- Only 1.3% of performance reviews land in the "High" (100–150) band, with the large majority in "Average" (50–99) — worth checking whether the rating scale or manager calibration is compressing scores toward the middle.
- The workforce is split almost evenly across 6 employment types (15.8%–18.4% each) and 3 work modes (32.9%–33.8% each) — no single category dominates, which is useful context when interpreting any employment-type-specific finding.
- Only 400 of 2,500 employees (16%) carry an "Active" EmploymentStatus, while Terminated, Resigned, and Retired together account for 1,072 records (43%) — well above the formal 14.5% Attrition Rate KPI. This suggests the EmploymentStatus field and the ExitRecords table aren't fully reconciled with each other.
- Kenya branch payroll figures (e.g., Nakuru $450K, Nyeri $434K) run roughly 8–10x higher than similarly sized Nigeria branches (e.g., Ilorin $35K) despite comparable headcounts (65–75 staff per branch). This pattern is more consistent with an unreconciled currency figure than an actual regional pay gap, and would need Finance sign-off before being used in any compensation comparison.
- Relocation (63) and Termination (59) are the two most common documented exit reasons — ahead of voluntary Resignation (51) — indicating involuntary and relocation-driven departures make up a meaningful share of recorded attrition, not just voluntary turnover.
- Promotions peak twice a year, in March and October (72 each), rather than following a flat monthly pattern, which lines up with the kind of cycle a formal review calendar would produce.

---

## Recommendations

1. **Finding:** Customer Service, Administration, and the Busia and Lokoja branches run attrition well above company average. **Recommended action:** prioritize these four units for a focused retention review (exit interviews, manager feedback, workload check) before any company-wide initiative. **Purpose:** concentrate limited retention resources where the data shows the clearest need.

2. **Finding:** Campus Recruitment and the Company Website convert applicants at a meaningfully higher rate than Job Portal and Indeed, at comparable volume. **Recommended action:** review recruitment budget allocation against these hire rates, alongside a cost-per-hire comparison this dataset doesn't currently include. **Purpose:** improve recruiting efficiency without assuming spend needs to increase.

3. **Finding:** A large share of exits cluster in an employee's first year, and a further share of exit records carry an invalid tenure value. **Recommended action:** introduce a structured first-year check-in process, and separately, audit ExitRecords for exit dates that fall before the recorded hire date. **Purpose:** address the likely early-attrition pattern and the data-quality issue currently limiting confidence in tenure reporting.

4. **Finding:** Training completion and average performance scores barely vary across departments. **Recommended action:** review whether the current 0–150 performance scale and training curriculum are capturing real department-level differences. **Purpose:** confirm these systems are functioning as intended before relying on them for further decisions.

5. **Finding:** Only 16% of employees are marked "Active," which diverges sharply from the formal 14.5% Attrition Rate KPI. **Recommended action:** reconcile the Employees.EmploymentStatus field against the ExitRecords table so both report a consistent view of current headcount. **Purpose:** restore confidence in headcount and attrition reporting before it's used for planning.

6. **Finding:** Kenya branch payroll figures appear 8–10x higher than similarly sized Nigeria branches. **Recommended action:** confirm with Finance whether payroll is reported in a common currency across countries, and standardize if not. **Purpose:** ensure payroll and compensation comparisons across countries are valid.

None of these recommendations are guaranteed to solve the underlying issue — they're the next logical step the data supports, not a confirmed fix.

---

## Project Challenges

- **Duplicate records across all 8 tables (1,053 total).** Resolved with Power Query's duplicate-removal step before any analysis began, so counts and rates downstream wouldn't be inflated.
- **Missing values in the Employees table.** Department_ID gaps were filled where a lookup could resolve them; Email and Phone gaps were left flagged rather than guessed, since there was no reliable source to reconstruct real contact data.
- **Inconsistent text formatting.** Names and categorical fields were standardized to Proper Case and trimmed of stray whitespace — inconsistent casing would otherwise silently fragment groupings like "department" or "branch" in Power BI (e.g., "sales" and "Sales" counted as two different values).
- **Linking 8 separate tables.** The dashboard's Employee Profile drill-through page needed a consistent `EmployeeID` across every table, which meant the cleaning step had to happen before modeling — duplicate or malformed IDs would have broken the relationships.
- **Conflicting or questionable figures.** While reviewing the dashboard, I noticed the "invalid email/phone" counts exactly match the "missing email/phone" counts (documented above), and that the ExitRecords tenure breakdown includes a "<0" bucket that isn't logically possible. Rather than resolve these silently, I documented both as open data-quality notes in this README instead of folding them into a cleaner-looking headline number.

---

## Project Limitations

- This is a portfolio/case-study project built on a provided instructional dataset, not a live corporate system — figures reflect the dataset as given, not real Geoflex operations.
- No cost, salary-band, or exit-interview text data was available, so the recruitment and attrition recommendations are directional, not backed by a full cost-benefit calculation.
- Currency units aren't labeled per branch, which limits how far the payroll and salary comparisons across Nigeria and Kenya can be trusted (see [Key Insights](#key-insights)).
- The exit-tenure data anomaly (the "<0" bucket) isn't resolved within this dataset, so early-attrition figures are reported alongside that caveat rather than as a single clean number.

---

## Business Value

This project gives HR and business leaders a way to see where attrition risk actually concentrates by department and branch, compare recruitment channels on conversion efficiency rather than raw volume, check whether training and performance systems are differentiating employees as intended, and catch data-governance gaps (status-field mismatches, currency inconsistencies, date-logic errors) before those numbers get used for workforce planning.

---

## Repository Structure

```text
HR-Analytics/
│
├── README.md                      ← this file
│
├── images/                        ← dashboard screenshots referenced above
│   ├── executive-overview.png
│   ├── administration-dashboard.png
│   ├── talent-acquisition.png
│   ├── development-performance.png
│   ├── attrition-analysis.png
│   ├── branch-comparison.png
│   ├── employee-demographics.png
│   └── employee-profile.png
│
├── documentation/                 ← the project brief and business-question workbook
│   ├── Problem_Statement.docx
│   └── Business_Questions.docx
│
├── data/                          ← raw and cleaned source tables (add your Employees,
│                                     Attendance, ExitRecords, Recruitment, Promotions,
│                                     TrainingRecords, PerformanceReviews, LeaveRequests
│                                     files here — raw/ and cleaned/ subfolders recommended)
│
└── dashboard/                     ← the .pbix Power BI file
```

Only include a folder if you have something real to put in it — an empty `data/` or `dashboard/` folder with no files is worse than not having the folder at all.
