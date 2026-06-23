# Recommendation Memo: Onboarding and Activation Campaign

## Executive summary

The new onboarding and activation campaign significantly improves the North Star metric, paid conversion rate, from 3.19% in Control to 7.04% in Treatment. The one-tailed two-proportion z-test produced p = 0.000549, so the conversion lift is statistically significant.

However, the treatment also increases support burden and weakens revenue quality. Support ticket rate rises from 14.78% to 24.79%, and average revenue per converted user falls from $1,630.10 to $770.41. Because of these guardrail risks, the recommendation is not a full launch.

**Final recommendation: Launch only for selected segments.**

## North Star metric

The North Star metric is **paid conversion rate within 30 days**.

This metric best represents whether the onboarding campaign moves new users into paid subscription behavior. It connects directly to business growth because a higher paid conversion rate increases the paying customer base.

Supporting metrics include landing page visit rate, trial start rate, onboarding completion rate, engagement score, average revenue per user, and average revenue per converted user. These explain where conversion gains are coming from and whether the gains are high quality.

Blindly optimizing paid conversion could create low-quality conversions, refunds, support tickets, or lower revenue per converted user.

## KPI tree explanation

The KPI tree is saved as `outputs/kpi_tree.png`.

The KPI tree breaks the North Star metric into three main driver groups:

1. **Landing and acquisition activation**
   - Landing page visit rate
   - Traffic source quality
   - Device experience

2. **Trial activation**
   - Trial start rate
   - Onboarding completion rate
   - Days to first value

3. **Monetization and plan fit**
   - Plan selection mix
   - Revenue per converted user
   - Days to convert

Guardrails include refund rate, support ticket rate, engagement score, revenue quality, and segment-level decline.

## Experiment result summary

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

## Hypothesis test interpretation

- H0: Treatment paid conversion rate is less than or equal to Control.
- H1: Treatment paid conversion rate is greater than Control.
- Test type: One-tailed two-proportion z-test.
- α = 0.05.
- z-statistic = 3.2640.
- p-value = 0.000549.

Because p < 0.05, the treatment conversion improvement is statistically significant.

## Guardrail analysis

### Refund rate

Refund rate increased from 0.00% to 0.42%. The absolute number is small, but because Control had zero refunds, this must be monitored before broad launch.

### Support ticket rate

Support ticket rate increased from 14.78% to 24.79%. This is the largest guardrail risk because it indicates higher operational cost and possible onboarding confusion.

### Days to convert

Average days to convert improved from 8.86 days to 6.40 days. This is a positive guardrail.

### Engagement score

Average engagement score improved from 57.03 to 62.94. This suggests the treatment is driving stronger early usage.

### Revenue quality

Average revenue per user increased only slightly from $51.97 to $54.25, while average revenue per converted user declined from $1,630.10 to $770.41. This suggests the treatment may be converting more lower-value users.

## Segment-level insight

Plan type is the most important segmentation signal:

- Free: conversion 3.06% → 9.29% (6.23% lift), ARPU $22.73 → $51.18.
- Premium: conversion 2.75% → 6.25% (3.50% lift), ARPU $53.86 → $100.56.
- Basic: conversion 3.62% → 3.88% (0.26% lift), ARPU $98.69 → $36.76.

Traffic source also shows mixed results:

- Referral: conversion 2.47% → 10.99% (8.52% lift), ARPU $33.31 → $103.00.
- Paid Search: conversion 1.29% → 6.25% (4.96% lift), ARPU $10.91 → $34.78.
- Social: conversion 7.75% → 6.06% (-1.69% lift), ARPU $137.14 → $51.94.

Social traffic underperforms, while Referral, Paid Search, Organic, and Email traffic generally show better treatment conversion patterns.

## Final recommendation

**Launch only for selected segments.**

Recommended rollout:

- Launch to **Free** and **Premium** plan users.
- Prioritize non-Social traffic sources, especially Referral, Organic, Paid Search, and Email.
- Avoid full launch to Basic plan users until the campaign improves revenue quality.
- Do not launch broadly to Social or Unknown traffic until additional testing explains the decline.

## Risks and limitations

- Random assignment was assumed but not independently verified.
- Long-term retention and lifetime value are unavailable.
- Support tickets and refunds are measured only within the available 30-day window.
- Revenue outliers were retained because they appear to be real business outcomes.
- Segment-level sample sizes are smaller than the overall test, so segment recommendations should be monitored after rollout.

## Next steps

1. Run a targeted rollout for Free and Premium plan users.
2. Add onboarding instrumentation to understand support ticket drivers.
3. Redesign or personalize the campaign for Basic plan users.
4. Run a follow-up test for Social traffic.
5. Monitor support ticket rate, refund rate, ARPU, ARPCU, engagement score, and conversion by segment after rollout.
