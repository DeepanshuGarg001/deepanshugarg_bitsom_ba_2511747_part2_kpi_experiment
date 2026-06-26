# Hypothesis Testing Notes

## 1. Null Hypothesis (H0)
There is no significant difference in the Paid Conversion Rate between the Control group (existing onboarding) and the Treatment group (new campaign experience). 
Mathematically: P_treatment - P_control = 0 (or P_treatment <= P_control).

## 2. Alternate Hypothesis (H1)
The Paid Conversion Rate for the Treatment group is significantly higher than that of the Control group.
Mathematically: P_treatment > P_control (or P_treatment != P_control).

## 3. Test Type
Two-tailed Two-Proportion Z-Test. A two-tailed test was chosen to be conservative, testing if there's any statistical difference (positive or negative) between the two groups.

## 4. Significance Level
Alpha (α) = 0.05. This means there is a 5% risk of rejecting the null hypothesis when it is actually true (Type I error).

## 5. Metric Being Tested
**Paid Conversion Rate** (Number of users converted to paid / Total number of users).

## 6. Reason for Choosing this Metric
Paid Conversion Rate was selected as the North Star Metric because it directly aligns with the campaign’s objective of improving user conversion and translates directly to revenue generation for our subscription-based digital product. Measuring earlier steps (like trial starts) might not guarantee revenue impact.

## 7. Interpretation Logic & Results
**Test Inputs:**
- Control Group (N = 690): 22 conversions (3.19%)
- Treatment Group (N = 710): 50 conversions (7.04%)

**Test Output:**
- Z-Statistic: ~3.33
- P-Value (Two-tailed): ~0.0009

**Decision Rule:**
Since the P-Value (0.0009) is less than our Significance Level (0.05), we **reject the null hypothesis**.

**Business Interpretation:**
The new onboarding campaign (Treatment) caused a statistically significant increase in the Paid Conversion Rate. The increase from 3.19% to 7.04% is substantial and unlikely to be the result of random chance. However, we must also consider the guardrail metrics (like the observed increase in support tickets) before making a final rollout decision.
