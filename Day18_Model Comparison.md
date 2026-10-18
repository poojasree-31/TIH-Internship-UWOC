# Day 18: Model Comparison

## What I did today

By now I had trained five different models on the same train/test data. Today's job was to put all of them side by side in one table, so I can see clearly which one actually works best.

I also measured how fast each model makes a prediction, because in a real underwater communication system, speed matters too, not just accuracy.

## Code used

```python
import time

models = {
 "Fixed Threshold": None,
 "Logistic Regression": model_lr,
 "SVM": model_svm,
 "Random Forest": model_rf,
 "MLP": model_mlp
}

results = []
for name, model in models.items(): start = time.time()
 if name == "Fixed Threshold": preds = (X_test['Analog Voltage'] > 0.44).astype(int)
 else: preds = model.predict(X_test)
 elapsed = time.time() - start

 results.append({
 "Model": name,
 "Accuracy": accuracy_score(y_test, preds),
 "Precision": precision_score(y_test, preds, zero_division=0),
 "Recall": recall_score(y_test, preds, zero_division=0),
 "F1": f1_score(y_test, preds, zero_division=0),
 "Inference Time (s)": elapsed
 })

comparison_df = pd.DataFrame(results)
print(comparison_df)
```

## Final comparison table

| Model | Accuracy | Precision | Recall | F1 | prediction time (s) |
|---|---|---|---|---|---|
| Fixed Threshold | 51.7% | 42.9% | 78.3% | 55.4% | 0.000404 |
| Logistic Regression | 76.7% | 90.9% | 43.5% | 58.8% | 0.000903 |
| SVM | 61.7% | 0% | 0% | 0% | 0.001333 |
| Random Forest | 75.0% | 65.4% | 73.9% | 69.4% | 0.006135 |
| MLP | 61.7% | 0% | 0% | 0% | 0.000987 |

## What this table tells me

**On accuracy**, Logistic Regression comes out on top at 76.7%, with Random Forest very close behind at 75.0%. Both of these are clearly better than the old fixed threshold method (51.7%).

**On precision and recall**, the two models tell a different story:
- Logistic Regression has very high precision (90.9%) but low recall (43.5%). This means when it says "bit = 1," it is almost always right, but it misses more than half of the actual 1s.
- Random Forest is more balanced, with 65.4% precision and 73.9% recall. It catches more of the real 1s, but makes a few more mistakes while doing it.

**SVM and MLP both failed** in the same way. They got "okay-looking" accuracy (61.7%) only because they gave up and predicted the majority class (0) every single time. Their precision and recall for class 1 is 0%, which means they are not usable models, even though their accuracy number alone looks decent. This shows that accuracy by itself can be misleading.

**On speed**, every model is extremely fast, well under a hundredth of a second per prediction. Random Forest is the slowest of the group (0.006s) because it runs many small decision trees internally, but even that is fast enough for this kind of system. Speed is not really a deciding factor here since all five models are fast enough in practice.

## Which model(s) I am shortlisting

Based on this table, I am shortlisting **two models** to take forward for tuning: 1. **Random Forest**: because it has the best balance across all four metrics (accuracy, precision, recall, F1), and it does not have the predicting only the more common class problem.
2. **Logistic Regression**: because it has the highest accuracy and extremely high precision, which could be useful if the project cares more about not making false "1" predictions.

I am dropping SVM and MLP from further tuning for now, since both failed to learn the minority class at all in their current form. In Day 19, I plan to test if scaling the features (since Analog Voltage is around 0.3-0.7 but NTU_level is 1-5, a very different range) can fix this problem for SVM and MLP.

## Takeaway for Day 18

What I have found so far is that the fixed threshold method the original hardware used is actually the weakest of all five approaches once the water gets murkier. Simple machine learning models like Logistic Regression and Random Forest both beat it by a clear margin, which is exactly the kind of result this internship project was trying to show.
