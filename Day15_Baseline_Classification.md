# Day 15 — Baseline Classification & Mentor Review

## Baselines Built

### 1. Fixed-Threshold Baseline (threshold = 0.44)

Evaluated on the held-out test set (1,277 rows):

| Metric | Value |
|---|---|
| Accuracy | 1.0 |
| Precision | 1.0 |
| Recall | 1.0 |
| F1 Score | 1.0 |
| BER (approx.) | 0.0 |

Confusion Matrix:
```
[[799   0]
 [  0 478]]
```

### 2. Logistic Regression Baseline

Trained on `X_train`/`y_train`, evaluated on the same held-out test set:

| Metric | Value |
|---|---|
| Accuracy | 1.0 |
| Precision | 1.0 |
| Recall | 1.0 |
| F1 Score | 1.0 |

Confusion Matrix:
```
[[799   0]
 [  0 478]]
```

## Interpretation

Both baselines achieve perfect classification on the held-out test set, with zero false positives or false negatives. This matches the class-separability findings from Day 10 EDA — since the two classes occupy entirely non-overlapping signal ranges at the 1–2 NTU condition, both a simple threshold and a linear model can separate them perfectly.

## Modelling Direction Confirmed

- Both baselines are now correctly validated (trained/tuned on train data, evaluated on unseen test data) rather than evaluated on the full dataset as in earlier preliminary checks.
- Since both baselines already max out all metrics, Week 3's remaining classifiers (SVM, Random Forest, optional MLP) are expected to perform identically on this dataset — this is expected and will be explicitly noted rather than treated as a surprising or negative result.
- Modelling direction going forward: continue building the full suite of classifiers as required by the workflow (for completeness and comparison-table purposes), while flagging to the mentor that meaningful differentiation between methods will only be possible once multi-NTU raw data is available.
