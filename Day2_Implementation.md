# Day 2 — Initial Implementation & Analysis

## Dataset Used

`anaotherGUI/1-2NTU.csv` from the UWOC_useing_photoresistor project — 8,512 rows, 3 columns:
- `labels` - true transmitted bit (0 or 1)
- `feature` - received analog signal value
- `bit` - an existing threshold-based prediction from the original project

## Data Quality Check

- No missing values in any column.
- Class balance: 5,321 samples labelled 0, 3,191 labelled 1 (~62% / 38% split - moderately imbalanced, so F1 and confusion matrix are tracked alongside accuracy).
- `feature` column stats: values range from 0.337 to 0.625, with most values clustered either near the low end ~0.34–0.36 or the high end ~0.51–0.60.

## Exploratory Analysis

Plotted histograms of `feature`, split by true `labels` 0 vs 1. Result: the two classes form two **completely separate, non-overlapping clusters** - Label 0 sits between ~0.335-0.36, Label 1 sits between ~0.51-0.60, with a clear gap in between and zero overlap.

## Baseline: Fixed Threshold

Applied a manual threshold at 0.44 (chosen from the middle of the visible gap):

- **Accuracy: 1.0**
- **F1 Score: 1.0**
- **Confusion Matrix:** `[[5321, 0], [0, 3191]]` - zero misclassifications.

## Initial ML Model: Logistic Regression

Trained a Logistic Regression model on `feature` to predict `labels`, using an 80/20 train-test split.

- **Accuracy: 1.0**
- **F1 Score: 1.0**

## Analysis & Key Finding

Both the simple fixed threshold and Logistic Regression achieve perfect classification on this dataset. This is because, at the 1-2 NTU turbidity level, the received signal values for bit 0 and bit 1 are cleanly separated with no overlap - there is no ambiguity for either method to resolve.

## Challenges / Limitations Identified

- The core hypothesis of this project - that ML outperforms a fixed threshold as turbidity increases - **cannot be demonstrated using this dataset alone**, since raw signal data is only available for the 1-2 NTU range. Higher turbidity ranges (2–3, 3–4, 4–5, 5–6 NTU) exist in the project only as result plot images, not as raw CSV data.
- Because both methods score identically here, this dataset serves mainly as a sanity check that the pipeline (loading, EDA, baseline, ML model, evaluation) works correctly end-to-end.

## Next Steps

- Flag the missing raw NTU-level data to the mentor and ask whether additional higher-turbidity data will be provided.
- If possible, obtain or request raw signal data at higher NTU levels to properly test where ML begins to outperform the fixed threshold.
- In the meantime, extend evaluation with SVM and Random Forest on the current dataset for completeness, and prepare the reproducible pipeline so it's ready to run on higher-turbidity data as soon as it's available.
