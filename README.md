# Hotel Booking Cancellation Analysis

Exploratory and diagnostic analysis of 34,210 hotel reservations, identifying
which booking characteristics predict cancellation and what a revenue team could
do about each one.

**Headline:** 45.5% of bookings in this extract were cancelled. Cancellation risk
is driven far more by **booking channel and lead time** than by price.

## What the analysis found

**Channel matters more than price.** Online travel agencies generate 60% of
booking volume at a 59% cancellation rate. Corporate (20%), direct (23%) and
offline agency (24%) bookings cancel at roughly a third of that. Relationship-based
bookings hold; anonymous ones do not.

**Lead time risk is non-linear.** Cancellation peaks at 58.8% for bookings made
31-90 days ahead, then *falls* to 46.2% beyond 180 days. Short-notice bookings
(0-7 days) are the most reliable at 19.4%. The intuitive "further ahead means
riskier" rule is wrong — mid-range bookings are the problem, because the customer
has time to reconsider but has not committed hard.

**Price is not the driver.** ADR correlates with cancellation at just 0.20, and
ADR distributions for cancelled and fulfilled bookings largely overlap. Special
requests (-0.12) and repeat-guest status (-0.15) are protective — engagement
signals commitment.

## A finding that needs a caveat

Non-refundable deposits show a **94.6% cancellation rate** — the opposite of what
a deposit is supposed to do. This almost certainly reflects hotel-initiated
cancellations or data-entry convention rather than customer abandonment, and it
sits on only 391 bookings. It is reported as an anomaly requiring policy
investigation, not as evidence that deposits cause cancellations.

## Recommendations drawn from the analysis

- Tiered deposit policy: minimal under 7 days, moderate at 8-30, strict at 31+
- Increase OTA commission loading by 3-5% to offset channel risk
- Direct booking incentives at 10-15% discount to shift channel mix
- Expand corporate and group contracts (5-10% cancellation) for revenue stability

## Method notes

Cleaning removed 30% of rows: 9,761 duplicates, 88 zero-adult bookings and 400
records with ADR at or below zero. Outliers in ADR and lead time were **retained**
— high ADR reflects genuine premium inventory and long lead times reflect genuine
early corporate booking, so removing them would discard the highest-value
segments rather than clean errors.

## Running it

```bash
pip install -r requirements.txt
# download the dataset into data/ (see data/README.md)
jupyter notebook notebooks/01_cancellation_analysis.ipynb
```

## Limitations

- **The 86% vs 22% city/resort split is specific to this 2016 extract** and is
  much wider than the gap in the full published dataset. It should be treated as
  a property of this subset, not a general finding about hotel types.
- Single-year data cannot separate seasonal effects from trend.
- A t-test is used to compare cancellation rates between hotel types. With a
  binary outcome a chi-square or two-proportion test is the more standard choice;
  at this sample size the conclusion is unaffected, but the test is not the
  textbook one.
- The analysis is descriptive. No predictive model is fitted, so nothing here
  supports real-time risk scoring — that is named as the next step, not a result.

## Licence

MIT. The dataset is published under its own terms by the original authors.
