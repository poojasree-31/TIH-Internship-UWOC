# Day 6 - Pre-Dataset Readiness & Mentor Review

## Methodology V1

**Problem:** Classify transmitted bits (0/1) from received analog signal values in underwater optical communication, robust to varying turbidity (NTU).

**Data:** Labelled dataset with received signal value, true bit label, and turbidity/NTU metadata (expected format per Day 4).

**Preprocessing plan:**
1. Preserve raw data untouched.
2. Audit for missing values, duplicates, invalid values, class balance, and data leakage risks (per Day 4 checklist).
3. Clean only where justified by audit findings - document every decision.
4. Stratified 70/15/15 train/validation/test split, fixed random seed for being able to get the same result again.

**Modelling plan:**
1. Fixed-threshold baseline.
2. Logistic Regression, SVM, Random Forest (classical ML shortlist from Day 2 literature review).
3. Optional small MLP for completeness.
4. All models trained on the same split, tested identically.

**Evaluation plan:**
- Metrics: accuracy, precision, recall and F1, confusion matrix, BER/error rate, inference time.
- Comparison table across all methods.
- Robustness analysis across individual NTU levels (core for this project experiment).

**Constraints:**
- Software-only; no hardware integration or physical data collection.
- Individual execution - no dividing technical work among interns.

## Updated Experiment Plan

Following the Day 5 experiment log template, each model run will be logged with method, hypersettings, split details, and all metrics - enabling direct, fair comparison once results come in.

## Mentor Corrections (After Feedback)

*(To be filled in after the actual mentor review meeting - record any changes to the split strategy, metrics, or constraints, and update Methodology V1 accordingly.)*
