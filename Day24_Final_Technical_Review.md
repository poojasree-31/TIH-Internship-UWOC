# Day 24: Technical Review

## Final Method & Validation Results

- **Final method:** SVM (`rbf` kernel, scaled features via `StandardScaler`), selected for the best accuracy (83.3%) and F1 (73.7%) of all five models tested, plus a sensible performance drop across turbidity levels.
- **Final test results:** Accuracy 83.3%, Precision 93.3%, Recall 60.9%, F1 73.7%, confirmed on reload in Day 23.
- **Real performance across water conditions study (Day 20):** Using actual data from all 5 turbidity conditions, SVM beat the fixed threshold method at every single condition, and got worse gradually (100% → 100% → 88.9% → 71.4% → 61.5%) as water got murkier, while the threshold's accuracy jumped around unpredictably without following a clear pattern.

## Reproducible Input-to-Output Workflow

```
Raw CSV (internship Dataset, combined multi-NTU data)
 → Data audit & quality checks (Day 8)
 → Cleaning decisions applied (no missing values, no duplicates, 'binary bit R' excluded as leakage)
 → NTU mapped to numeric NTU_level feature (Day 11)
 → 70/15/15 split that keeps the 0 and 1 balance similar split (Day 11, random_state=42)
 → Feature scaling fitted on training data only (Day 19)
 → Model training (SVM, rbf kernel, default hyperparameters on scaled data)
 → Evaluation on test test set, including per-condition breakdown (Day 20)
 → Frozen model + scaler artefacts (final_model/svm_final.pkl, final_model/scaler_final.pkl)
 → Reload and re-validation (Day 23)
```

All steps are captured in the project notebook and can be re-run full from the raw CSV to the final saved model.

## Correction Note

An earlier version of this project (through Day 28 of the first attempt) was built entirely on a one-condition subset of the data (only 1-2 NTU, taken from a different file than the one the mentor actually intended). That version showed 100% accuracy for every single model, because the data had no overlap between the two classes at that one easy condition. This made it look like the project had already succeeded, but it meant the project's central question (does ML help as the water gets murkier) was never actually tested.

This restart uses the correct combined dataset covering all 5 real turbidity conditions. The real results are lower (83.3% accuracy instead of 100%), but they are useful, and they actually answer the question this internship project set out to answer.

## Remaining Open Questions

1. How well would this model work well on new data to turbidity levels beyond 5-6 NTU, which this dataset does not cover.
2. Whether a larger dataset (more than ~80 rows per condition) would change the exact numbers, especially at the murkier conditions where the test set only has 9 to 14 rows per group.

## Final Error-Analysis & Reporting Requirements (Confirmed Scope)

- Detailed error/failure analysis to be conducted on Day 25, focused on where and why the SVM model still makes mistakes, especially at higher NTU levels.
- Final report (Day 26) to clearly explain both the original mistake (wrong dataset used in the first attempt) and the corrected, real findings, since this honesty is part of good scientific practice.

## Mentor Corrections

*(To be filled in after the actual Intern Discussion / Mentor Review meeting.)*
