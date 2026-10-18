# Day 16 : Testing Two More Models

## SVM (Test Set)

| Metric | Value |
|---|---|
| Accuracy | 61.7% |
| Precision | 0.0% |
| Recall | 0.0% |
| F1 Score | 0.0% |

Confusion Matrix:
```
[[37 0]
 [23 0]]
```

**Important problem found:** SVM never once predicted a "1". It just guessed "0" every single time. Because there are more 0s than 1s in our data, this lazy strategy still gets an accuracy that may look okay (61.7%), but it's but it did not identify any of the actual 1s. This is exactly why we always check precision and recall too, not just accuracy, a model can look okay on accuracy alone while actually being broken.

## Random Forest (Test Set)

| Metric | Value |
|---|---|
| Accuracy | 75.0% |
| Precision | 65.4% |
| Recall | 73.9% |
| F1 Score | 69.4% |

Confusion Matrix:
```
[[28 9]
 [ 6 17]]
```

Random Forest did well, close to Logistic Regression's accuracy (75% vs 76.7%), but with a clearly better balance between precision and recall (F1 of 69.4% vs Logistic Regression's 58.8%). It actually caught more of the true 1s than Logistic Regression did.

## What We Have Learned So Far

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Fixed Threshold | 51.7% | 42.9% | 78.3% | 55.4% |
| Logistic Regression | 76.7% | 90.9% | 43.5% | 58.8% |
| SVM | 61.7% | 0% | 0% | 0% |
| Random Forest | 75.0% | 65.4% | 73.9% | 69.4% |

Random Forest looks like the strongest, most balanced performer so far. SVM needs more attention (likely needs tuning or scaling) before it can be considered a fair option.
