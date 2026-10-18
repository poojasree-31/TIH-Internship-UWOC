# Day 19: finding better model settings

## What I did today

In Day 17 and Day 18, SVM and MLP both failed badly. They just kept predicting "0" for every single row, giving 0% precision and 0% recall even though their accuracy looked okay. I had a guess about why this was happening: the two input features, Analog Voltage (around 0.3 to 0.7) and NTU_level (1 to 5), are on very different scales. Some models get confused when one feature's numbers are much bigger than another's.

So today I did two things:
1. Scaled the features using `StandardScaler` and re-tested SVM and MLP on the scaled data.
2. Used `GridSearchCV` to search for better settings (model settings) for Random Forest and Logistic Regression.

## Code used

```python
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import GridSearchCV

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

model_svm_scaled = SVC(random_state=42)
model_svm_scaled.fit(X_train_scaled, y_train)

model_mlp_scaled = MLPClassifier(hidden_layer_sizes=(8,), max_iter=1000, random_state=42)
model_mlp_scaled.fit(X_train_scaled, y_train)

param_grid_rf = {'n_estimators': [50, 100, 200], 'max_depth': [None, 5, 10], 'min_samples_split': [2, 5]}
grid_rf = GridSearchCV(RandomForestClassifier(random_state=42), param_grid_rf, cv=5, scoring='f1')
grid_rf.fit(X_train, y_train)

param_grid_lr = {'C': [0.01, 0.1, 1, 10], 'solver': ['liblinear', 'lbfgs']}
grid_lr = GridSearchCV(LogisticRegression(), param_grid_lr, cv=5, scoring='f1')
grid_lr.fit(X_train, y_train)
```

## Results

### SVM and MLP after scaling

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| SVM (before scaling) | 61.7% | 0% | 0% | 0% |
| **SVM (after scaling)** | **83.3%** | **93.3%** | **60.9%** | **73.7%** |
| MLP (before scaling) | 61.7% | 0% | 0% | 0% |
| **MLP (after scaling)** | **80.0%** | **78.9%** | **65.2%** | **71.4%** |

This supports what I thought from Day 17. Scaling the features completely fixed the predicting only the more common class problem. Both models went from being useless (0% precision and recall) to being some of the best models in the whole project.

### Random Forest tuning

Best parameters found: `max_depth=5, min_samples_split=5, n_estimators=200`

| Version | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Random Forest (default settings, Day 16) | 75.0% | 65.4% | 73.9% | 69.4% |
| Random Forest (tuned) | 75.0% | 66.7% | 69.6% | 68.1% |

Tuning did not really improve Random Forest. The F1 score actually dropped slightly, from 69.4% to 68.1%. The default settings were already close to the best this model can do on this data.

### Logistic Regression tuning

Best parameters found: `C=10, solver='liblinear'`

| Version | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Logistic Regression (default settings, Day 15) | 76.7% | 90.9% | 43.5% | 58.8% |
| Logistic Regression (tuned) | 75.0% | 72.2% | 56.5% | 63.4% |

Tuning changed the balance here. Accuracy went down slightly (76.7% to 75.0%), but recall went up a lot (43.5% to 56.5%), and F1 improved overall (58.8% to 63.4%). The tuned version catches more real "1" bits, at the cost of a few more false alarms.

## Updated overall comparison (best version of each model)

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Fixed Threshold | 51.7% | 42.9% | 78.3% | 55.4% |
| Logistic Regression (tuned) | 75.0% | 72.2% | 56.5% | 63.4% |
| **SVM (scaled)** | **83.3%** | **93.3%** | **60.9%** | **73.7%** |
| Random Forest (default) | 75.0% | 65.4% | 73.9% | 69.4% |
| MLP (scaled) | 80.0% | 78.9% | 65.2% | 71.4% |

## What I Learned Today

The biggest finding today is that **SVM (with scaled features) is now the best model overall**, with the highest accuracy (83.3%) and the highest F1 score (73.7%) of any model tested so far. This is a complete turnaround from Day 16, where SVM was one of the two failed models.

This also taught me something important: a model "failing" does not always mean the model itself is bad. Sometimes it is a data preparation problem. Here, simply putting both features on the same scale was enough to fix two broken models.

Going forward, **SVM (scaled)** is my new primary candidate, with MLP (scaled) as a strong second option. I will carry the scaled SVM model into the performance across water conditions testing in Day 20.
