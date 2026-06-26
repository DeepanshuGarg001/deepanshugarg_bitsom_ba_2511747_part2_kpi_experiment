# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

## 1. Business Context
Our subscription-based digital product company launched a new onboarding and activation campaign to improve user conversion and early engagement. Users were split into two groups:
- **Control group:** Existing onboarding experience
- **Treatment group:** New campaign experience

The primary decision to be made is whether this new treatment should be rolled out to all users. This decision impacts new signups, our customer support teams, and our overall revenue generation.

## 2. Dataset Description
The dataset provided (`campaign_experiment_data.xlsx`) contains 1,400 rows of user-level data over a 30-day period. Key attributes include:
- `user_id`, `signup_date`, `experiment_group`, `region`, `device_type`, `traffic_source`, `plan_type`
- Binary behavioral flags: `visited_landing_page`, `started_trial`, `completed_onboarding`, `converted_to_paid`, `refund_requested`
- Continuous metrics: `revenue_30d`, `support_tickets_30d`, `days_to_convert`, `engagement_score`

**Data Preparation:** 
Missing values in categorical columns (`device_type`, `traffic_source`) were filled with "Unknown". Missing `engagement_score` was imputed with the median score. Missing `days_to_convert` was kept as null for non-converted users. Duplicates based on `user_id` were removed, and invalid binary flags were handled. Revenue outliers were capped at the 99th percentile.

## 3. North Star Metric Selected
**Paid Conversion Rate**
This was selected because it represents the most direct link to business growth. While upstream metrics like 'Trial start rate' or 'Onboarding completion rate' are important, optimizing for them blindly could lead to high drop-offs before actual revenue is realized. Paid Conversion Rate ensures the campaign generates paying customers, not just free users.

## 4. KPI Tree Summary
The KPI tree visualizes how the North Star metric breaks down into actionable drivers:
- **North Star:** Paid Conversion Rate
- **Primary Drivers:** Onboarding Completion Rate, Trial Start Rate, User Engagement
- **Sub-Drivers:** Landing Page Visit Rate, Signups
- **Guardrail Metrics:** Refund Rate, Support Ticket Rate, Average Days to Convert

*The KPI tree image can be found in `outputs/kpi_tree.png`.*

## 5. Experiment Analysis Approach
We aggregated the cleaned dataset by `experiment_group` to calculate our core metrics. We also performed a segment-level breakdown across `region`, `device_type`, and `plan_type` to understand how the campaign performed across different user cohorts. The analysis was output to an Excel workbook for detailed review.

## 6. Hypothesis Test Summary
We ran a Two-Proportion Z-Test to evaluate the impact on our North Star metric.
- **Null Hypothesis:** The Paid Conversion Rate for the Treatment group is equal to or less than the Control group.
- **Alternate Hypothesis:** The Paid Conversion Rate for the Treatment group is greater than the Control group.
- **Result:** The Treatment group saw a conversion rate of 7.04% compared to 3.19% for the Control group. With a p-value of 0.0009 (alpha = 0.05), the results are statistically significant, and we reject the null hypothesis.

*Detailed notes are available in `analysis/hypothesis_test_notes.md`.*

## 7. Guardrail Metrics Considered
- **Support Ticket Rate:** Increased from 14.8% to 24.8%.
- **Refund Rate:** Increased marginally from 0.0% to 0.42%.
- **Average Days to Convert:** Decreased from 8.86 days to 6.40 days.

## 8. Final Recommendation
**Launch**
Despite the increased support ticket rate, the substantial and statistically significant lift in the Paid Conversion Rate (a 120% relative increase) makes the campaign a success. The business should launch the new onboarding experience while simultaneously investigating and addressing the UX issues causing the spike in support tickets.

## 9. Assumptions and Limitations
- **Assumption:** The users in the Control and Treatment groups were randomly assigned and represent a statistically similar cohort of overall traffic.
- **Assumption:** The 30-day window is sufficient to capture the full conversion cycle for the majority of users.
- **Limitation:** We do not have qualitative feedback to understand *why* the support tickets spiked.
- **Limitation:** The average revenue per converted user dropped in the Treatment group. If this trend holds long-term, it could offset the gains from the increased conversion rate.

## 10. Screenshots Included
The following screenshots can be found in the `screenshots/` directory:
- `summary_metrics.png` (Control vs Treatment summary table)
- `hypothesis_test_output.png` (Test output and calculation evidence)
- `kpi_tree_preview.png` (KPI tree image)
