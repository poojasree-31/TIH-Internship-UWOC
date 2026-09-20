# Day 19 - Controlled Hyperparameter / Parameter Experiments

## How the tuning was done

Tuned the selected model (Logistic Regression, per Day 18) using `GridSearchCV` with 5-fold cross-validation on the training set, using F1 score.

**Parameter grid:**
- `C` (inverse regularization strength): [0.01, 0.1, 1, 10, 100]
- `solver`: ['lbfgs', 'liblinear']

Total: 10 combinations tested systematically, each evaluated via 5-fold cross-validation.

## Results

| Setting | Value |
|---|---|
| Best parameters | `C=0.1`, `solver='lbfgs'` |
| Best cross-validated F1 | 1.0 |
| Validation Accuracy | 1.0 |
| Validation F1 | 1.0 |

## What this means

Tuning did not change the results - the model already achieves perfect scores regardless of regularization strength or solver choice, which makes sense because the classes are already clearly separated (per Day 10 EDA). This is expected, not a sign the search was ineffective: with zero classification errors possible on this dataset, no hyperparameter configuration can improve or worsen the result.

## Validation only

As required, the test set (`X_test`/`y_test`) was **not** touched during this tuning process - only training data (via cross-validation) and the validation set were used for model selection. The test set remains kept for Day 23's final validation.

## Best settings saved

- **Model:** Logistic Regression
- **Parameters:** `C=0.1`, `solver='lbfgs'`
- This configuration will be used as the tuned candidate for the Day 20 robustness study and beyond.
