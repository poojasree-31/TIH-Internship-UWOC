# Day 25 - Detailed Error / Failure Analysis

## Setup

Since real test data yields zero errors, this analysis uses the highest simulated noise level from Day 20 (σ = 0.08) to inspect how and why the frozen Logistic Regression model fails under degraded (simulated turbidity) conditions.

## Error summary

- **Total errors:** 154 out of 1,277 test samples (~12.1%), consistent with the ~87.9% accuracy reported in Day 20 at this noise level.
- **Errors by true class:** 83 errors on true label 0 (false positives), 71 errors on true label 1 (false negatives) - fairly balanced, no strong bias toward misclassifying one class over the other.

## Why the errors happened

Every misclassification is explained by the same mechanism: added noise pushed the signal value **across the model's decision boundary (≈0.4474)**.

- Rows originally in the label-0 cluster (~0.34-0.36) that received large positive noise crossed above 0.4474 and got predicted as 1.
- Rows originally in the label-1 cluster (~0.52-0.53) that received large negative noise dropped below 0.4474 and got predicted as 0.

This is confirmed by the drift statistics: the noisy values of misclassified rows sit tightly clustered around the boundary (mean drift ≈ 0.001 from the boundary itself, std ≈ 0.05), meaning **the model isn't failing randomly - it's failing exactly where the noise was strong enough to cross the boundary**, which is the expected, explainable behavior of a linear classifier under Gaussian noise.

## Common pattern

There is one single recurring failure pattern: **boundary-crossing due to additive noise**, with no evidence of a separate or unusual failure mode (e.g. no systematic bias toward one class, no unexplained outlier errors far from the boundary - the max drift was ~0.106, still a plausible single-noise-draw event).

## Limitations

- This entire analysis is based on **simulated Gaussian noise**, not real turbidity effects. Real turbidity may cause non-linear, asymmetric, or systematically biased signal shifts (e.g. consistently pulling values in one direction, or affecting one bit value more than the other) rather than simple symmetric random noise.
- Because of this, the model's real-world failure pattern under actual higher-NTU conditions **may differ a lot** from what's shown here - this analysis shows the method and expected behavior under a reasonable proxy, but should not be taken as a prediction of real-world failure modes.
- The model's likely generalization boundary, based on this proxy study, is roughly noise σ ≥ 0.03, where performance first starts to measurably drop from perfect.
