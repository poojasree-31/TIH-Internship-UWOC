# Day 17 — Additional Model (Small MLP)

## Model Trained

A small MLP (Multi-Layer Perceptron) with one hidden layer of 8 neurons, trained on `X_train`/`y_train`, evaluated on the same held-out test set as prior days.

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

## Training/Validation Behaviour

- Final training loss: **0.004** — low and stable, indicating clean convergence rather than instability or erratic optimization.
- Converged in **209 iterations** (well under the 1000 max), meaning the model didn't need to be pushed near its iteration limit to fit the data.
- No overfitting signal expected or observed, since the task itself (separating two non-overlapping clusters) is trivially easy for any reasonable classifier.

## Comparison Against Standard ML Models

The MLP performs identically to Logistic Regression, SVM, and Random Forest (all scoring 1.0 across every metric, with the same confusion matrix: 799 true negatives, 478 true positives, zero errors). Given this, the added complexity of a neural network provides no benefit over simpler models on the current dataset — this is expected and consistent with prior days' findings, not a modelling issue.

## Saved Artefacts

- MLP model object (`model_mlp`) — to be saved via `pickle` or `joblib` for the final software pipeline package.
