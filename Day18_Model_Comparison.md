# Day 18 — Model / Method Comparison & Mentor Review

## Comparison Table (All Methods, Held-Out Test Set)

| Model | Accuracy | Precision | Recall | F1 | Inference Time (s) |
|---|---|---|---|---|---|
| Fixed Threshold | 1.0 | 1.0 | 1.0 | 1.0 | 0.000660 |
| Logistic Regression | 1.0 | 1.0 | 1.0 | 1.0 | 0.002285 |
| SVM | 1.0 | 1.0 | 1.0 | 1.0 | 0.006944 |
| Random Forest | 1.0 | 1.0 | 1.0 | 1.0 | 0.030835 |
| MLP | 1.0 | 1.0 | 1.0 | 1.0 | 0.005204 |

## Discussion

**Accuracy/quality:** All five methods are statistically identical on this dataset — every method scores a perfect 1.0 on all four classification metrics, with zero misclassifications each. This is expected given the Day 10 EDA finding that the two classes are completely non-overlapping at the available 1–2 NTU condition.

**Inference time (the real differentiator):** This is where methods actually diverge:
- **Fixed Threshold** is fastest by a wide margin (0.00066s) — it's just a single comparison operation, no model to run.
- **Logistic Regression** (0.0023s) and **MLP** (0.0052s) are next, both lightweight once trained.
- **SVM** (0.0069s) is a bit slower.
- **Random Forest** (0.0308s) is by far the slowest — roughly 47x slower than the fixed threshold — because it evaluates multiple decision trees per prediction.

**Overfitting:** No signs of overfitting — all models generalize perfectly to the held-out test set, but this is because the underlying classification task is trivially separable, not necessarily because any model generalizes exceptionally well in a harder setting.

**Data limitations:** The core limitation remains unchanged from Day 8: all data is from a single turbidity condition (1–2 NTU). This comparison cannot yet show where ML-based methods would outperform a simple threshold, since that gap is expected to appear only as turbidity increases and the signal becomes noisier — which this dataset doesn't capture.

**Failure patterns:** None observed — zero misclassifications across all five methods.

## Shortlisted Candidate(s) for Deeper Experiments (Day 19-20)

Given that accuracy/F1 cannot differentiate the models on this dataset, **inference time becomes the deciding factor**:

- **Primary candidate: Logistic Regression** — matches the fixed threshold's near-instant speed while remaining a genuine ML model (unlike the threshold, it can incorporate additional features like turbidity once available), making it the most practical choice for a lightweight, deployable classifier.
- **Fixed Threshold** remains the reference baseline for comparison, per the project's stated objective.
- Random Forest is deprioritized for further tuning given its high inference cost with no accuracy benefit on this data; it will be revisited only if future higher-turbidity data reveals it captures patterns simpler models miss.

## Note for Mentor Review

This comparison confirms the pipeline (baseline → ML models → evaluation → comparison) works correctly end-to-end, but the dataset's single-condition nature prevents a meaningful test of the project's central hypothesis. Requesting mentor guidance on next steps: proceed with hyperparameter tuning on this dataset as a formality (Day 19-20), or prioritize obtaining multi-NTU raw data first.
