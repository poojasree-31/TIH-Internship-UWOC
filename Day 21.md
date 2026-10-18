# Day 20: performance across water conditions Study (Testing Across Real Turbidity Levels)

## Why I did this

Back in the early version of this project, I did not have real data for different water conditions, so I had to fake it by adding random noise to pretend the water was murkier. Now that I have the correct dataset, which has real data for 5 actual turbidity levels (1-2 NTU up to 5-6 NTU), I do not need to fake anything anymore. Today I tested how the old threshold method and my new best model (SVM with scaled features) actually perform at each real NTU condition.

## Code used

```python
X_test_with_ntu = X_test.copy()
X_test_with_ntu['NTU'] = df.loc[X_test.index, 'NTU']
X_test_with_ntu['true_label'] = y_test
X_test_with_ntu['threshold_pred'] = (X_test['Analog Voltage'] > 0.44).astype(int)
X_test_with_ntu['svm_scaled_pred'] = model_svm_scaled.predict(scaler.transform(X_test))

print(X_test_with_ntu.groupby('NTU').apply(
 lambda g: pd.Series({
 'rows': len(g),
 'threshold_accuracy': accuracy_score(g['true_label'], g['threshold_pred']),
 'svm_scaled_accuracy': accuracy_score(g['true_label'], g['svm_scaled_pred'])
 })
))
```

(Note: pandas showed a small `DeprecationWarning` about `groupby.apply`. This is just a future-version warning from the pandas library itself, not an error, and does not affect the results.)

## Results

| Water Condition | Rows in Test | Threshold Accuracy | SVM (scaled) Accuracy |
|---|---|---|---|
| 1-2 NTU | 10 | 50.0% | **100.0%** |
| 2-3 NTU | 14 | 28.6% | **100.0%** |
| 3-4 NTU | 9 | 55.6% | **88.9%** |
| 4-5 NTU | 14 | 71.4% | 71.4% |
| 5-6 NTU | 13 | 53.8% | 61.5% |

## What I Found

This is one of the most important results from my project.

**SVM beats or matches the threshold method at every single water condition.** At the two clearest conditions (1-2 NTU and 2-3 NTU), SVM gets perfect accuracy, while the old threshold method is barely better than a coin flip (50% and 28.6%).

**The threshold method does not follow any clear pattern.** Its accuracy jumps around unevenly: 50%, then drops to 28.6%, then goes up to 55.6%, then up to 71.4%, then back down to 53.8%. This tells me the threshold was never really reliable, even at conditions where I expected it to do okay. A single fixed cutoff point (0.44) just cannot adapt to how the signal shifts as water gets murkier.

**SVM does follow a sensible pattern: it gets gradually worse as water gets murkier.** 100% at 1-2 NTU and 2-3 NTU, then 88.9% at 3-4 NTU, then dropping to 71.4% and 61.5% at the two murkiest conditions. This result makes sense because it does its best when the signal is clean, and its performance naturally drops as the problem gets genuinely harder. That is a much more trustworthy pattern than the threshold's random-looking ups and downs.

## What This Means

This result directly matches what I found back in Day 8, where the mistake rate of the old threshold-based labels jumped from 0% at 1-2 NTU to 50% at 4-5 NTU. The threshold approach was never built to handle murky water, and today's test proves that with real numbers, condition by condition.

The scaled SVM model is a clear improvement over the threshold at every single condition, and it gets worse in a sensible, gradual way instead of failing unpredictably. This is strong evidence that a machine learning model is genuinely better suited for this task than the original fixed-threshold hardware approach, especially as turbidity increases.

## What's next

Even at the murkiest condition (5-6 NTU), SVM still beats the threshold (61.5% vs 53.8%), but both start struggling. With only 9 to 14 test rows per condition, these exact percentages could shift a bit with more data, but the overall trend (ML model staying strong longer, threshold being unreliable everywhere) is a solid and real finding to bring to the mentor.
