# Campaign Experiment Analysis

## Business context

A subscription-based digital product company tested a new onboarding and activation campaign against the existing onboarding experience.

- **Control group:** Existing onboarding experience.
- **Treatment group:** New campaign experience.
- **Decision:** Launch, do not launch, continue testing, or launch only for selected segments.

## Business problem statement

Leadership must decide whether the new onboarding and activation campaign should be launched to all users, kept off, tested further, or launched only to selected segments. The decision impacts new users, growth and marketing teams, customer support, finance, and product teams because it can change conversion, user quality, support load, refunds, and short-term subscription revenue. The primary metric expected to improve is paid conversion rate within 30 days. Risks to monitor include refund rate, support ticket rate, days to convert, engagement score, revenue per converted user, and segment-level declines. Evidence required before a recommendation includes clean experiment data, balanced group review, a statistically valid test of the primary metric, and guardrail analysis showing whether conversion gains are sustainable.

## Dataset description

The repository uses the uploaded dataset:

- `data/campaign_experiment_data.xlsx`
- Source sheet: `experiment_data`
- Context sheet: `business_context`
- Raw rows: 1,408
- Unique users used for analysis: 1,400
- Experiment groups after de-duplication: Control = 690, Treatment = 710
- Signup date range: 2025-01-01 to 2025-05-31

## North Star metric selected

**Paid conversion rate within 30 days** is the North Star metric.

Formula:

`converted_to_paid users / total users`

### Why this is the main success metric

The campaign objective is to improve user conversion and early engagement. Paid conversion is the clearest outcome showing that onboarding moved users from signup into revenue-generating subscription behavior.

### Why other metrics are supporting metrics

- Landing page visit rate shows whether users entered the activation funnel.
- Trial start rate shows early intent.
- Onboarding completion rate shows activation quality.
- Engagement score shows early usage strength.
- Average revenue per user and revenue per converted user show revenue quality.
- Refund and support ticket rates are guardrails rather than success metrics because they measure risk and operational cost.

### How it connects to business growth

Higher paid conversion can increase the number of paying customers, improve subscription growth, and expand revenue opportunities.

### What could go wrong if optimized blindly

The campaign could convert low-quality users, increase support load, create refund risk, reduce average revenue per converted user, or harm specific segments even if the overall conversion rate improves.

## KPI tree summary

The KPI tree is saved in:

- `outputs/kpi_tree.png`
- `screenshots/kpi_tree_preview.png`

The tree breaks the North Star metric into three main driver groups:

1. Landing and acquisition activation
2. Trial activation
3. Monetization and plan fit

Guardrails included in the KPI tree:

- Refund rate
- Support ticket rate
- Engagement score
- Revenue quality / average revenue per converted user
- Segment-level decline

## Experiment analysis approach

The analysis was performed in `analysis/experiment_analysis.xlsx`.

Data preparation checks included:

| Check | Finding | Handling |
|---|---:|---|
| Raw rows | 1,408 | Original data copied unchanged into `data/`. |
| Exact duplicate user IDs | 8 IDs / 8 duplicate rows | Removed duplicate occurrences after the first row for analysis and flagged them in `Prepared_Data`. |
| Missing `device_type` | 18 | Filled as `Unknown` for segment analysis. |
| Missing `traffic_source` | 24 | Filled as `Unknown` for segment analysis. |
| Missing `engagement_score` | 14 | Excluded from engagement average denominator only. |
| Missing `days_to_convert` | 1336 | Expected for non-converted users; days average calculated among converted users only. |
| Invalid binary values | 0 | No invalid binary values found. |
| Revenue outliers | 4 positive-revenue outliers | Flagged and retained because they represent actual revenue outcomes. |

Revenue outlier rule: IQR on positive revenue values only. Q1 = $404.02, Q3 = $1,178.66, upper bound = $2,340.63.

## Experiment result summary

The summary workbook is saved in:

- `outputs/experiment_summary.xlsx`

Key overall results after duplicate handling:

| Metric | Control | Treatment | Difference |
|---|---:|---:|---:|
| User count | 690 | 710 | +20 |
| Landing page visit rate | 63.62% | 72.39% | 8.77% |
| Trial start rate | 25.07% | 29.01% | 3.94% |
| Onboarding completion rate | 15.65% | 21.13% | 5.47% |
| Paid conversion rate | 3.19% | 7.04% | 3.85% |
| Average revenue per user | $51.97 | $54.25 | $2.28 |
| Average revenue per converted user | $1,630.10 | $770.41 | $-859.69 |
| Refund rate | 0.00% | 0.42% | 0.42% |
| Support ticket rate | 14.78% | 24.79% | 10.01% |
| Average engagement score | 57.03 | 62.94 | +5.91 |
| Average days to convert | 8.86 | 6.40 | -2.46 |

## Hypothesis test summary

The hypothesis test notes are saved in:

- `analysis/hypothesis_test_notes.md`

Test performed:

- Metric tested: Paid conversion rate
- Test type: One-tailed two-proportion z-test
- Null hypothesis: Treatment paid conversion rate is less than or equal to Control
- Alternative hypothesis: Treatment paid conversion rate is greater than Control
- Significance level: 0.05

Results:

- Control conversion: 22/690 = 3.19%
- Treatment conversion: 50/710 = 7.04%
- Absolute lift: 3.85%
- Relative lift: 120.87%
- z-statistic: 3.2640
- one-tailed p-value: 0.000549
- Decision: Reject the null hypothesis.

## Guardrail metrics considered

The treatment improved conversion, engagement, and days to convert, but guardrails show risk:

- Support ticket rate increased from 14.78% to 24.79%.
- Refund rate increased from 0.00% to 0.42%.
- Average revenue per converted user declined from $1,630.10 to $770.41.
- Social traffic showed weaker treatment performance than control.
- Basic plan users showed minimal conversion lift and lower ARPU.

## Segment-level insights

Plan type:

- Free: conversion 3.06% → 9.29% (6.23% lift), ARPU $22.73 → $51.18.
- Premium: conversion 2.75% → 6.25% (3.50% lift), ARPU $53.86 → $100.56.
- Basic: conversion 3.62% → 3.88% (0.26% lift), ARPU $98.69 → $36.76.

Traffic source:

- Referral: conversion 2.47% → 10.99% (8.52% lift), ARPU $33.31 → $103.00.
- Paid Search: conversion 1.29% → 6.25% (4.96% lift), ARPU $10.91 → $34.78.
- Social: conversion 7.75% → 6.06% (-1.69% lift), ARPU $137.14 → $51.94.

## Final recommendation

**Recommendation: Launch only for selected segments.**

Launch the campaign to segments with stronger evidence and healthier revenue patterns, especially Free and Premium plan users and non-Social traffic sources. Do not full-launch yet because support ticket rate increased materially and average revenue per converted user declined. Continue testing or redesign for Basic plan users and Social/Unknown traffic before scaling to all users.

## Assumptions and limitations

- The experiment is treated as randomized because the dataset identifies Control and Treatment groups, but the assignment mechanism was not independently verified.
- Duplicate user rows are exact duplicates and were removed after the first occurrence.
- Missing `device_type` and `traffic_source` were retained as `Unknown` to avoid dropping users.
- Revenue outliers were flagged but retained.
- Statistical testing focused on conversion; guardrails were evaluated descriptively.
- Long-term retention and lifetime value were not available.

## Screenshots included

| Screenshot file | Shows |
|---|---|
| `screenshots/summary_metrics.png` | Control vs Treatment summary table |
| `screenshots/hypothesis_test_output.png` | Hypothesis test output and calculation evidence |
| `screenshots/kpi_tree_preview.png` | KPI tree preview |

## Repository contents

```text
campaign_experiment_repository/
├── README.md
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx
│   └── hypothesis_test_notes.md
├── outputs/
│   ├── experiment_summary.xlsx
│   ├── kpi_tree.png
│   └── recommendation_memo.md
└── screenshots/
    ├── summary_metrics.png
    ├── hypothesis_test_output.png
    └── kpi_tree_preview.png
```
