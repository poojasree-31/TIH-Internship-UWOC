# Day 22 - Final Model / Pipeline Freeze

## Final model selected

**Logistic Regression** (tuned: `C=0.1`, `solver='lbfgs'`) - selected because of:
- Matching or exceeding all other methods (SVM, Random Forest, MLP) on accuracy/F1 across all evaluations (Days 15-18).
- Fast inference time (0.0023s vs. Random Forest's 0.031s - Day 18).
- Simplicity and interpretability, because it is simple and easy to understand.
- Validated with proper cross-validation tuning (Day 19), not just a single train/test check.

## Preprocessing, data split and evaluation

- **Preprocessing:** no scaling (feature already normalized 0-1), no encoding needed (labels already binary), `bit` column excluded (leakage).
- **Split:** stratified 70/15/15 train/validation/test, `random_state=42`.
- **Evaluation:** accuracy, precision, recall, F1, confusion matrix, BER, inference time - calculated in the same way for all models.

## Model parameters

- Coefficient: 30.753
- Intercept: -13.760
- Implied decision boundary: `feature ≈ 0.4474` (intercept ÷ coefficient) - very close to the 0.44 threshold chosen manually during initial EDA (Day 2), showing the model found almost the same separating point that was noticed earlier.

## Saved files

- `final_model/logistic_regression_final.pkl` - the frozen, trained model, saved via `joblib` for reuse without retraining.
- `processed_data/train.csv`, `val.csv`, `test.csv` - the frozen Dataset V1 splits (Day 11-12).

## Why this model was selected

Logistic Regression was chosen over more complex alternatives (SVM, Random Forest, MLP) because, on the available data, all methods perform identically in terms of accuracy/F1 - meaning the added complexity of the more powerful models provides no measurable benefit. In line with the "appropriate simplicity" principle, the simplest model that matches top performance and offers the best inference speed (aside from the non-ML fixed threshold) was selected as final.
