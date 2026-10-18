# Day 22: Final Model and Pipeline

## Final Method Selected

**SVM (Support Vector Machine) with scaled features**: I chose it because of:
- Best accuracy (83.3%) and best F1 score (73.7%) of all five methods tested, across Days 15-19.
- A sensible, gradual drop in performance as water gets murkier (Day 20), unlike the fixed threshold which jumped around unpredictably.
- Still very fast at prediction time (0.0013s per prediction, Day 18), well within what a real underwater system would need.
- A clear improvement over the fixed threshold at every single turbidity condition tested.

## Why Not the Other Models

- **Fixed Threshold:** weakest method overall, especially as turbidity increases. This was the original hardware approach, and the whole point of the project was to show an ML model can do better.
- **Logistic Regression (tuned):** solid, but lower recall (56.5%) and lower F1 (63.4%) than SVM.
- **Random Forest:** balanced, but slower at making a prediction (0.0061s) and slightly lower F1 (69.4%) than SVM.
- **MLP (scaled):** close second to SVM (F1 71.4%), but SVM still came out ahead on both accuracy and F1.

## Frozen Preprocessing, Split & Evaluation method

- **Preprocessing:** features scaled using `StandardScaler`, fit only on the training data and reused (never refit) on validation/test data, to avoid data answer information accidentally getting into the inputs. `binary bit R` column excluded from training (it is the old threshold-based guess, not a real input).
- **Split:** with a similar balance of 0s and 1s 70/15/15 train/validation/test, `random_state=42`, done once in Day 11 and reused for every model since.
- **Evaluation:** accuracy, precision, recall, F1, confusion matrix, prediction time, computed the same way for every model so the comparison is fair.

## Model Details

- Model type: `SVC` from scikit-learn, with the default `rbf` (radial basis function) kernel.
- Number of support vectors: 59 for class 0, 56 for class 1 (out of 279 training rows). This means the model relies on about 41% of the training data as "support points" to define the line or rule the model uses to separate the two classes, which is reasonable for a dataset this size.
- The model only works correctly on scaled input, so the saved `scaler_final.pkl` must always be used to transform any new input before calling `.predict()`.

## Saved files

- `final_model/svm_final.pkl`: the frozen, trained SVM model, saved via `joblib`.
- `final_model/scaler_final.pkl`: the frozen `StandardScaler`, needed to prepare any new input the same way the training data was prepared.
- `processed_data/X_train.csv`, `X_val.csv`, `X_test.csv`, `y_train.csv`, `y_val.csv`, `y_test.csv`: the frozen data splits, so results can always be reproduced.

## Why I Chose This Model

SVM was chosen over the other models because it is the only one that was best, or tied for best, on every metric that matters here: accuracy, F1, and how sensibly it gets worse as the water gets murkier. It needed one extra preprocessing step (feature scaling) compared to Random Forest, but that is a small, well-understood step, and it is already frozen into the saved pipeline so it will be applied automatically and correctly every time.
