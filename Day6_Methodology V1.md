# Day 6: Readiness Check and Mentor Review

## Methodology V1

**Problem:** Classify transmitted bits (0/1) from received analog signal values in underwater optical communication. The method should still work when the water turbidity (NTU) changes.

**Data:** Labelled dataset with received signal value, true bit label, and turbidity/NTU metadata (expected structure per Day 4).

**Preprocessing plan:**

1. Keep the raw data untouched.
2. Audit for missing values, duplicates, invalid values, class balance, and leakage risks (per Day 4 checklist).
3. Only clean where the audit says it is needed, and write down every decision.
4. Stratified 70/15/15 train/validation/test split, fixed random seed for reproducibility.

**Modelling plan:**

1. Fixed threshold baseline.
2. Logistic Regression, SVM, Random Forest (classical ML shortlist from Day 2 literature review).
3. Optional small MLP for completeness.
4. All models trained on the same split and tested the same way.

**Evaluation plan:**

- Metrics: accuracy, precision, recall, F1, confusion matrix, BER/error rate, inference time.
- Comparison table across all methods.
- Robustness check across each NTU level. This is the main experiment of our project.



## 

## 
