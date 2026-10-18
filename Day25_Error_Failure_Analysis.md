# Day 25: Error Analysis

## Setup

Today I looked directly at which rows the final SVM model got wrong on the real test set, and checked for a pattern.

## Code used

```python
from sklearn.metrics import confusion_matrix

final_preds = loaded_model.predict(loaded_scaler.transform(X_test))
cm = confusion_matrix(y_test, final_preds)

error_df = X_test.copy()
error_df['NTU'] = df.loc[X_test.index, 'NTU']
error_df['true_label'] = y_test
error_df['predicted_label'] = final_preds
error_df['correct'] = error_df['true_label'] == error_df['predicted_label']

misclassified = error_df[error_df['correct'] == False]
```

## Confusion Matrix

```
[[36 1]
 [ 9 14]]
```

This means: 36 true negatives, 1 false positive, 9 false negatives, 14 true positives, out of 60 test rows.

## Error Summary

- **Total errors:** 10 out of 60 test samples (16.7%), matching the 83.3% accuracy from Day 23.
- **Error type breakdown:** 1 false positive (predicted 1, actually 0) and 9 false negatives (predicted 0, actually 1). The model is much more likely to miss a real "1" bit than to wrongly guess "1" when it should be "0".

## Where the errors happen

| NTU Condition | Number of Errors |
|---|---|
| 3-4 NTU | 1 |
| 4-5 NTU | 4 |
| 5-6 NTU | 5 |

**9 out of 10 errors (90%) happen at the two murkiest water conditions (4-5 NTU and 5-6 NTU).** Only 1 error happens at 3-4 NTU, and there are zero errors at the two clearest conditions (1-2 NTU and 2-3 NTU). This matches exactly what the performance across water conditions study in Day 20 showed, and it also matches the original Day 8 finding, where the old threshold labels started disagreeing more and more as NTU increased.

## Root cause of errors

Looking at the actual misclassified rows, almost all the errors are cases where the true label was 1, but the signal value was on the lower side (values like 0.34 to 0.48), closer to where label-0 values usually sit. As water gets murkier, the two classes start to overlap more in their signal values, so there is less of a clean gap for the model to use. This is a real, physical limitation of the data at high turbidity, not a mistake in how the model was built.

## Recurring Pattern

The clear, consistent pattern is: **the model almost never makes mistakes at low turbidity, and almost all of its mistakes happen at high turbidity, mostly by missing real "1" bits (false negatives) rather than wrongly predicting them (false positives).**

## Limitations & Likely how well it works on new data Boundaries

- The test set only has 9 to 14 rows per NTU condition, so these exact counts (like "4 errors at 4-5 NTU") could look a bit different with more data, even though the overall direction (more errors at higher NTU) is a strong and consistent trend across more than one day's analysis now.
- This dataset only goes up to 5-6 NTU. I do not know how the model would behave in even murkier water beyond that range, since there is no data for it.
- Because the model tends to miss real "1" bits at high turbidity rather than making up false "1"s, if this model were used in a real system, it would most often show up as lost or missing bits at high turbidity, not as wrong extra bits. That is useful context for anyone designing error correction on top of this model.
