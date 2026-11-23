# Cleaning log

| Area | Issue | Rows affected | Action |
|---|---|---:|---|
| subscriptions | plan_tier has inconsistent capitalisation | 101 | lower-cased to basic/plus/premium |
| subscriptions | churners who skipped the cancel-reason question | 382 | labelled 'not_provided' (active customers stay null) |
| usage | exact duplicate customer-month rows | 160 | kept first copy, dropped the rest |
| usage | blank minutes_active | 503 | imputed (0 if no workouts, else workouts x 30); flagged in minutes_imputed |
| subscriptions | active customers whose usage stops after month 1 (usage_stopped_early) | 139 | kept as recorded; flagged for sensitivity analysis |

## Checks that passed

- No duplicate customer_id; row counts match the project brief (4,200 / 30,685 raw rows).
- churned, churn_date and cancel_reason are consistent; no churn before signup or after 2025-12-31.
- monthly_price is fully determined by plan type and tier.
- All usage customers exist in subscriptions; no usage before signup or after cancellation.
- classes_booked is 0 on every Basic-plan row (structural, not disengagement).
- 28 look-alike customer pairs have different usage histories, so they are distinct people.
