# Day 15: Testing Our First Models

## Fixed Threshold Baseline (cutoff = 0.44, using only signal value)

| Metric | Value |
|---|---|
| Accuracy | 51.7% |
| Precision | 42.9% |
| Recall | 78.3% |
| F1 Score | 55.4% |

Confusion Matrix:
```
[[13 24]
 [ 5 18]]
```

## Logistic Regression (using signal value + water condition)

| Metric | Value |
|---|---|
| Accuracy | 76.7% |
| Precision | 90.9% |
| Recall | 43.5% |
| F1 Score | 58.8% |

Confusion Matrix:
```
[[36  1]
 [13 10]]
```

## What This Means

These are the numbers we were waiting for. With the correct dataset that has proper multi condition data, the fixed threshold only gets 51.7% right. That is basically a coin flip. The problem is that the best cutoff keeps moving as the water gets murkier, and one fixed number cannot keep up with that.

Logistic regression got 76.7% accuracy because it uses both the signal value and the water condition. This shows that our main idea works. When the model knows the water condition, it performs better than a simple fixed cutoff.

## A Closer Look at the Trade-off

Logistic regression is very precise at 90.9%. When it predicts 1, it is almost always right. But it also misses a lot of actual 1s. Its recall is only 43.5% compared to 78.3% for the threshold. So the threshold catches more 1s but also makes way more mistakes. This is something we need to discuss with our mentor. For this application, is it more important to catch every 1 bit, or to be confident when we say 1?

## Why This Matters

This is the strongest result we have so far. It backs up our core idea. Knowing the water condition helps the model make better decisions than a method that ignores it completely.
