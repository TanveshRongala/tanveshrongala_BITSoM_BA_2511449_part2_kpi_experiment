# Hypothesis Test Notes

## Business decision connection

Leadership needs to decide whether the new onboarding and activation campaign should be launched broadly, withheld, tested further, or launched only in selected segments. The hypothesis test focuses on the primary success metric: **paid conversion rate within 30 days**.

## Metric being tested

**Paid conversion rate**

Formula:

`converted_to_paid users / total users`

This metric was chosen because the business objective is to improve user conversion. Paid conversion is closer to business growth than upstream behaviors such as landing page visits or trial starts.

## Hypotheses

### Null hypothesis

H0: Treatment paid conversion rate is less than or equal to Control paid conversion rate.

`p_treatment <= p_control`

### Alternate hypothesis

H1: Treatment paid conversion rate is greater than Control paid conversion rate.

`p_treatment > p_control`

## Test direction

**One-tailed test**

Reason: the business question is whether the treatment improves conversion enough to justify launch. A decline or no improvement does not support launch.

## Significance level

α = 0.05

## Test method

One-tailed two-proportion z-test comparing the paid conversion rate of Control and Treatment users.

## Test inputs

| Input | Control | Treatment |
|---|---:|---:|
| Users | 690 | 710 |
| Paid conversions | 22 | 50 |
| Paid conversion rate | 3.19% | 7.04% |

## Test output

| Output | Value |
|---|---:|
| Absolute lift | 3.85% |
| Relative lift | 120.87% |
| Pooled conversion rate | 5.14% |
| Pooled standard error | 0.011807 |
| z-statistic | 3.2640 |
| one-tailed p-value | 0.000549 |
| two-tailed p-value reference | 0.001099 |
| 95% confidence interval for difference | 1.56% to 6.15% |

## Decision rule

Reject the null hypothesis if the one-tailed p-value is less than 0.05.

## Statistical decision

The p-value is 0.000549, which is below 0.05. Therefore, reject the null hypothesis.

## Business interpretation

The treatment group shows a statistically significant improvement in paid conversion rate: 3.19% in Control vs 7.04% in Treatment. This supports the conclusion that the new campaign improves conversion.

However, the launch recommendation should not be based only on conversion. Guardrails show risk:

- Support ticket rate increased from 14.78% to 24.79%.
- Refund rate increased from 0.00% to 0.42%.
- Average revenue per converted user declined from $1,630.10 to $770.41.
- Social traffic and Basic plan segments do not show strong enough evidence for broad rollout.

## Recommendation implication

The hypothesis test supports that the campaign can improve conversion, but guardrails support a more cautious decision: **launch only for selected segments and continue testing risky segments**.
