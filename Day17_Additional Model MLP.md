# Day 17 : Testing a Small Neural Network

## Small MLP (Test Set)

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

- Final training loss: 0.666 (quite high, barely better than guessing)
- Stopped after only 66 out of a possible 1000 rounds of training

## What Happened

Just like SVM on Day 16, the neural network also gave up and predicted "0" every single time. This is an important finding, and it does not necessarily mean the code is wrong. The likely reasons:

1. **Our dataset is small** (only 279 training rows), and neural networks usually need a lot more data to learn well.
2. **Our two input numbers are on very different scales** (signal value is around 0.3 to 0.7, water condition is 1 to 5), which can confuse models like MLP and SVM unless the inputs are scaled to match.
3. The model seems to have taken an easy approach: since most rows are label 0, always guessing 0 gives a reasonable-looking accuracy without actually learning anything useful.

## Comparing Everything So Far

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Fixed Threshold | 51.7% | 42.9% | 78.3% | 55.4% |
| Logistic Regression | 76.7% | 90.9% | 43.5% | 58.8% |
| SVM | 61.7% | 0% | 0% | 0% |
| Random Forest | 75.0% | 65.4% | 73.9% | 69.4% |
| MLP | 61.7% | 0% | 0% | 0% |

## Takeaway

The simpler models (Logistic Regression and Random Forest) handled this small, mixed-scale dataset much better than the more complex ones (SVM, MLP). This also shows that in machine learning, more complex models usually need more data to actually be worth using, and here, they didn't have enough to work with.
