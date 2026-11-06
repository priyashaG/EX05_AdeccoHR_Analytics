# Adecco India: HR Analytics Case Study (Employee Attrition)

An analysis of employee attrition across 1,470 staff records, finding who is leaving, which factors are associated with it, and what HR can do about it. Every figure in this repository is computed from `data/DATASET.csv`; the Excel workbook uses live `COUNTIFS` formulas on that data, so each number can be traced.

## Executive Summary

- **Company attrition: 16.1%** (237 exits out of 1,470 employees).
- **Junior staff (Job Level 1, age under 30): 35.1%** attrition, 2.2x the company rate.
- **Overtime is the strongest controllable driver:** 30.5% attrition with overtime vs 10.4% without. At Level 1 the gap is 52.6% vs 15.8%.
- **Early tenure under a new manager:** 28.3% attrition for staff with 1 year or less under their current manager, vs 11.2% above 3 years.
- **Estimated replacement cost: about $8.2M** across the 237 exits. This is an *assumption* (0.6 x annual income of leavers, editable in the workbook), not a measured figure.

## Repository Structure

```
adecco-hr-analytics/
├── data/
│   └── DATASET.csv                          # 1,470 records, 35 columns (source data)
├── working_files/
│   └── Adecco_HR_Analytics_Working_File.xlsx # Formula-driven analysis workbook
├── screenshots/
│   └── adecco_hr_dashboard_clean.png        # Static dashboard image
├── presentation/
│   └── Adecco HR Analytics Case Study.pptx  # 11-slide case study deck
└── README.md
```

## Dataset and Method

- 1,470 employee records, 35 columns (demographics, job level and role, satisfaction scores, income, tenure, manager tenure, travel, overtime flag, attrition flag).
- Departments in the data: Sales, Research & Development, Human Resources. Job levels 1 to 5. Nine job roles.
- **The data has no daily in/out times.** Overtime is therefore measured with the `OverTime` flag (Yes/No), not hours per day.
- Attrition rate = employees with `Attrition = Yes` divided by employees in the group.
- Relative risk = cohort attrition rate divided by its baseline group's rate.
- Risk bands (editable in the workbook): Critical at 2.5x or more, High at 1.75x or more, Moderate at 1.25x or more, otherwise Low.
- The replacement-cost multiplier (0.6) is an assumption and is a blue input cell in `Executive_Summary`.

## Key Findings

### Flight-risk cohorts

| Cohort | Staff | Attrition | Baseline | Relative risk |
|---|---|---|---|---|
| Level 1 + Overtime | 156 | 52.6% | 15.8% (Level 1, no overtime) | 3.3x |
| Single, age under 30 | 131 | 41.2% | 10.5% (Married, 30+) | 3.9x |
| Level 1, under 2 years at company | 136 | 44.1% | 20.4% (Level 1, 2+ years) | 2.2x |
| 1 year or less with current manager | 339 | 28.3% | 11.2% (over 3 years) | 2.5x |
| Frequent business travel | 277 | 24.9% | 8.0% (non-travel) | 3.1x |

Cohorts overlap, so the rates are not additive.

### Department and role

| Department | Attrition |
|---|---|
| Sales | 20.6% (92 of 446) |
| Human Resources | 19.0% (12 of 63) |
| Research & Development | 13.8% (133 of 961) |

Highest-risk roles: Sales Representative 39.8% (33 of 83), Laboratory Technician 23.9% (62 of 259), Human Resources 23.1% (12 of 52). Lowest: Research Director 2.5%, Manager 4.9%.

### Early tenure, pay and stock options

Level 1 staff with under 2 years at the company leave at 44.1% (vs 20.4% for 2+ years). Pay and stock options also matter, measured across **all staff**: monthly income under 3,000 shows 28.6% attrition vs 11.5%; no stock options 24.4% vs 9.9%. Within Level 1 alone the gaps are 29.4% vs 19.1% (pay) and 37.0% vs 16.8% (stock options).

### What the data does *not* support

An earlier draft of this project argued that Level 1 staff leave because of promotion "stagnation". The data does not back that up: promotion gap and salary hike show weak or no association with attrition (see `Cohort_Risk_Factors`, rows labelled "Low / not a driver"). The story is early-tenure churn plus pay and stock options.

## Excel Workbook

| Sheet | Contents |
|---|---|
| Executive_Summary | Headline KPIs, replacement-cost assumption, core-driver table |
| Dashboard | KPI tiles and three native charts |
| Cohort_Risk_Factors | 15 cohorts with counts, rates, baselines, relative risk and risk band |
| Department_Risk_Matrix | Department and job-role attrition with chart |
| Heatmaps | Level x Overtime, Level x Age band, Work-life balance x Overtime |
| Notes_Definitions | Definitions and assumptions |
| Data | The 1,470-row source data |

The summary tables are built with `COUNTIFS` formulas rather than native PivotTables.

## Recommended Actions

| Quarter | Action | Targets |
|---|---|---|
| Q1: Workload caps | Weekly overtime alerts; mandatory recovery days after peak periods | Overtime cohort (30.5% vs 10.4%) |
| Q2: Pay & careers | Review pay and stock options for low-income Level 1 staff; clear Level 1 to Level 2 path | Level 1 pay gap |
| Q3: Mentorship | 30-60-90 day onboarding and skip-level reviews in the first year | Staff with 1 year or less under a manager |
| Q4: Hybrid work | 2-3 remote days for staff with long commutes; cap frequent business travel | Frequent travellers (24.9% vs 8.0%) |

## Limitations

- **Association, not causation.** For example, if overtime staff left at the no-overtime rate, about 84 of the 237 exits would not have occurred, but this does not prove overtime causes exits.
- Cohorts overlap and some are small (check the `n` shown beside each rate).
- The replacement cost is an assumption, not an observed cost.
- The dashboard PNG is a static image; it has no interactive filters.
- Results apply to this dataset only. If your brief specifies a different file, recompute the figures by replacing the `Data` sheet.
