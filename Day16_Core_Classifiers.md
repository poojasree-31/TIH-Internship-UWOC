# Day 16 — Core Classifiers

## Models Trained

Both trained on `X_train`/`y_train` (same Dataset V1 split as Day 15), evaluated on the identical held-out test set (1,277 rows).

### SVM (default RBF kernel, `random_state=42`)

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

### Random Forest (default settings, `random_state=42`)

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

## Hyperparameters Used

- SVM: default scikit-learn parameters (RBF kernel, C=1.0), `random_state=42`.
- Random Forest: default scikit-learn parameters (100 trees), `random_state=42`.
- No tuning performed yet — that is scoped for Day 19 (controlled hyperparameter experiments), and is not necessary here since both models already achieve maximum possible scores.

## Class-Wise Performance Comparison

All four methods evaluated so far (fixed threshold, Logistic Regression, SVM, Random Forest) produce **identical results**: 1.0 accuracy/precision/recall/F1, and the exact same confusion matrix (799 true negatives, 478 true positives, zero errors). This is consistent with the Day 10 EDA finding that the two classes are completely non-overlapping at the 1–2 NTU condition — there is no room for any classifier to make an error on this particular dataset, regardless of model complexity.
