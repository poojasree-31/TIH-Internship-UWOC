# Day 23: Software Performance / Final Validation

## What I did today

Today I reloaded the saved model and scaler from scratch, exactly how it would work in a real using it in a real system, and ran it on the test set one more time to confirm the frozen pipeline still works correctly and to check its size and speed.

## Code used

```python
loaded_model = joblib.load('final_model/svm_final.pkl')
loaded_scaler = joblib.load('final_model/scaler_final.pkl')

X_test_scaled_final = loaded_scaler.transform(X_test)

start = time.time()
final_preds = loaded_model.predict(X_test_scaled_final)
elapsed = time.time() - start

print("Final Test Accuracy:", accuracy_score(y_test, final_preds))
print("Final Test Precision:", precision_score(y_test, final_preds, zero_division=0))
print("Final Test Recall:", recall_score(y_test, final_preds, zero_division=0))
print("Final Test F1:", f1_score(y_test, final_preds, zero_division=0))
```

## Final Validation Results (Frozen Pipeline, test set)

| Metric | Value |
|---|---|
| Test Accuracy | 83.3% |
| Test Precision | 93.3% |
| Test Recall | 60.9% |
| Test F1 | 73.7% |
| Total prediction time (60 test samples) | 0.0014 seconds |
| Per-sample prediction time | ~23.3 microseconds |
| Model file size | 5,771 bytes (~5.6 KB) |
| Scaler file size | 935 bytes (~0.9 KB) |

These numbers exactly match the results from Day 19, which confirms the saved model file and scaler file were frozen correctly and reload without any loss of accuracy.

## Comparison Against the Original starting method

| Method | Accuracy | F1 | Per-Prediction Speed | Model Size |
|---|---|---|---|---|
| Fixed Threshold | 51.7% | 55.4% | ~2 microseconds (no model, just one comparison) | None, just a constant |
| SVM (final model) | 83.3% | 73.7% | ~23.3 microseconds | ~6.7 KB total (model + scaler) |

The fixed threshold is faster since it does not need to load any file at all, but the difference (microseconds) does not matter in practice. The SVM model is still extremely lightweight and fast, and it gives a big real improvement in both accuracy and F1 over the threshold.

## Accuracy vs. Complexity / Runtime Trade-Off

- Going from the fixed threshold to SVM costs almost nothing in terms of speed or memory (a few extra microseconds, a few extra kilobytes), but gains 31.6 percentage points of accuracy and 18.3 points of F1.
- The one added step compared to Logistic Regression or the threshold is that SVM needs the saved scaler to prepare any new input the same way the training data was prepared. This is a small extra step but an important one. If it is skipped, the model's predictions will be wrong.
- Given how small and fast this model is, there is no real software performance cost to choosing SVM over the simpler threshold approach. It works much better for this project.

## Note for Future Hardware Consideration

Although actual hardware using it in a real system is outside this project's scope, these numbers (around 6.7 KB total size, microsecond-level prediction time) suggest the frozen model and scaler would be light enough to run on small embedded devices in a future version of this system, if that becomes a future goal.
