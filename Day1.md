# Day 1 : Understanding the Problem

## Objective & Problem Statement

To communicate underwater, we can't use WiFi or radio waves, because water absorbs electromagnetic waves quickly, giving them very short range underwater. So instead, this project uses **light** to send data underwater : bits are transmitted as light pulses (light on = 1, light off = 0).

The main problem: impurities in water : measured by **turbidity, in NTU (Nephelometric Turbidity Units)** : scatter and absorb the light. Because of this, the receiver doesn't get a clean "on/off" signal. Instead, it gets a **wobbly analog number** (e.g. 0.3, 0.6, 0.9) and has to guess which bit was actually sent.

The naive approach is to pick one fixed cutoff number (say, 0.5) : anything above is classified as "1", anything below as "0". But as the water gets murkier (higher NTU), this fixed cutoff stops working well, because the signal shifts and gets noisier, and the "0" and "1" signal ranges start to overlap.

**Goal:** Build machine learning models that can look at the received signal value (and the turbidity level) and correctly classify whether the original bit was 0 or 1 : even as turbidity changes : and show that they outperform the simple fixed-cutoff method.

## Inputs and Output

- **Inputs:** received analog signal value (`Analog Voltage`); turbidity/NTU condition (`NTU` column).
- **Output/target:** transmitted bit label : `Binary bit S` (the bit that was actually sent).

## Overall Software Pipeline

```
Raw Signal Data (Analog Voltage, Binary bit S, NTU)
 ↓
Data Cleaning & Quality Audit
 ↓
Train / Validation / Test Split (stratified by NTU + label)
 ↓
Baseline (Fixed Threshold) ──┐
 ↓ │
ML Models (LogReg, SVM, │
RF, MLP) │
 ↓ │
Evaluation (Accuracy, F1, │
BER, Inference Time) ←───────┘
 ↓
Robustness Analysis Across REAL NTU Levels (1-2, 2-3, 3-4, 4-5, 5-6 NTU)
 ↓
Final Model + Report
```

## Success Criteria

A model is counted as successful if it matches or exceeds the fixed-threshold baseline's accuracy/F1 while remaining more works well (staying accurate for longer) as turbidity increases across the real 1-2 NTU through 5-6 NTU range available in this dataset.

## Technical Questions & Assumptions Requiring Clarification

1. Is `binary bit R` simply a prior threshold-based guess, and should it be excluded from model training to avoid using information that gives away the answer (same as the earlier dataset's `bit` column)?
2. With only ~399 total rows (about 80 per NTU level), is this sample size enough for reliable train/val/test splits, or should results be treated as early?
3. Should the model treat NTU as a categorical input feature, or should separate models be trained per NTU level?
4. Is `Analog value` (the raw 0-255 reading) or `Analog Voltage` (the scaled 0-1 reading) the preferred input feature, given they carry the same information?
5. How should uneven number of the two labels be handled, given that higher-NTU conditions appear to have far more 0-labels than 1-labels (e.g. 4-5NTU and 5-6NTU)?
6. What's the expected metric priority : accuracy, F1, or BER : for judging "success" of a model, especially at higher NTU levels where errors are expected?
7. Should the final report highlight the mismatch between `binary bit R` and `Binary bit S` as evidence of the threshold method's real-world failure, since this is now visible directly in the data?
8. Given the small sample size, should results be cross-validated (e.g. k-fold) rather than relying on a single train/test split, to get more reliable estimates?

## Requirements

- A labelled dataset containing received signal values, transmitted bit labels, and turbidity (NTU) information. **(Confirmed now available for all 5 conditions.)**
- Software-only implementation : no physical hardware setup or data collection required.
- Tools: Python, Jupyter/Google Colab, NumPy, Pandas, Matplotlib, Scikit-learn.
- Deliverables: literature review, EDA, baseline + ML model comparison, performance across different water conditions analysis, final report and presentation.

## Dataset Understanding

The dataset used going forward is the combined internship dataset, covering **five real turbidity conditions**: 1-2NTU, 2-3NTU, 3-4NTU, 4-5NTU, and 5-6NTU : approximately 80 rows per condition, 399 rows total.

Columns:
- `S No` : row index.
- `binary bit R` : the received/guessed bit from an existing threshold-based method (likely to be excluded from model training, similar to the earlier dataset's leaking `bit` column : to confirm on Day 8).
- `Binary bit S` : the true transmitted bit (0 or 1) : this is the target/label.
- `Analog value` : raw sensor reading (0-255 range).
- `Analog Voltage` : scaled signal value (0-1 range), computed from `Analog value`.
- `NTU` : which turbidity condition this row was recorded under.


## Technical Concepts

- **Turbidity / NTU**: a measure of water cloudiness caused by suspended particles; higher NTU means murkier water and more light scattering/absorption.
- **Fixed threshold**: a single cutoff value used to classify a continuous signal into 0 or 1; simple but breaks down as noise/turbidity increases.
- **Logistic Regression**: a linear model that estimates the probability of a bit being 1 based on the signal value.
- **SVM (Support Vector Machine)**: finds the best boundary that separates 0s and 1s, even when the classes aren't perfectly separable.
- **Random Forest**: an ensemble of decision trees that can capture non-linear patterns in how signal value relates to the true bit.
