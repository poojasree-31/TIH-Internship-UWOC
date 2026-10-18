# Day 26: Final Software Files and Report Draft

## Repository Package Contents

```
TIH-Internship-UWOC/
├── README.md
├── Day1_Understanding.md ... Day25_Error_Failure_Analysis.md (daily deliverables)
├── UWOC_Bit_Classification.ipynb (full pipeline notebook: audit → EDA → preprocessing → modelling → tuning → robustness → error analysis)
├── internship Dataset (the correct, combined 5-NTU-condition CSV)
├── processed_data/
│ ├── X_train.csv, X_val.csv, X_test.csv
│ └── y_train.csv, y_val.csv, y_test.csv
├── final_model/
│ ├── svm_final.pkl
│ └── scaler_final.pkl
```

## README / Setup & Run Instructions (to add to repo README)

```markdown
## Setup
1. Open `UWOC_Bit_Classification.ipynb` in Google Colab.
2. Upload `internship Dataset` when prompted (the combined CSV covering all 5 turbidity conditions, 1-2 NTU through 5-6 NTU).
3. Run all cells in order. The notebook covers data audit, EDA, preprocessing,
 baseline/ML model training, hyperparameter tuning, real multi-condition
 robustness testing, and error analysis.

## Reproducing the Final Model
- The frozen final model is saved at `final_model/svm_final.pkl`, and its
 matching feature scaler is at `final_model/scaler_final.pkl`.
- Load both with: ```python
 import joblib
 model = joblib.load('final_model/svm_final.pkl')
 scaler = joblib.load('final_model/scaler_final.pkl')
 ```
- To predict on new data, the input must be scaled first with the same scaler: ```python
 new_data_scaled = scaler.transform(new_data)
 model.predict(new_data_scaled)
 ```

## Important Note
An earlier version of this project was built using the wrong dataset (a
single-turbidity-condition file). That version is no longer used. This
repository reflects the corrected project, built on the full 5-condition
dataset.
```

## Final Figures, Tables & Result Summary (for report)

- Data quality audit and per-condition mistake-rate table, showing the old threshold labels going from 0% wrong at 1-2 NTU to 50% wrong at 4-5 NTU (Day 8).
- Histogram and boxplot of signal value by class and by NTU condition (Day 10).
- Full model comparison table: accuracy, precision, recall, F1, prediction time across 5 methods (Day 18).
- Feature scaling fix and finding better model settings results (Day 19).
- Real per-condition performance across water conditions table, showing SVM beating the threshold at every turbidity level (Day 20).
- Final model freeze and reload validation (Days 22-23).
- Error analysis showing 9 out of 10 errors happen at the two murkiest conditions (Day 25).

## Final Report Draft: Outline

1. **Introduction & Problem Statement**: from Day 1.
2. **Literature Review**: from Day 2.
3. **Dataset & method**: from Days 4, 6, 7, 8-13.
4. **starting method & Model Development**: from Days 15-18.
5. **finding better model settings & Feature Scaling Fix**: from Day 19.
6. **performance across water conditions Study (Real multiple-condition Data)**: from Day 20.
7. **Final Model & Validation**: from Days 21-23.
8. **Error & Failure Analysis**: from Day 25.
9. **Limitations & Future Scope**: small sample size per condition (~80 rows), data only covers 1-2 NTU through 5-6 NTU, future scope per problem statement (multi-level modulation, adaptive learning, sequence-aware decoding, embedded using it in a real system, larger datasets).
10. **Conclusion.**

## Presentation (PPT) Draft: Slide Outline

1. Title slide (project, name, faculty, programme).
2. Problem statement & motivation.
3. Literature review summary.
4. Dataset overview & the key data quality finding (mistake rate rising with turbidity).
5. EDA: how clearly the two classes differ shrinking as turbidity increases.
6. method / pipeline diagram.
7. Model comparison table & results.
8. The feature scaling fix that rescued SVM and MLP.
9. performance across water conditions study results across all 5 real turbidity conditions.
10. Error analysis findings.
11. Limitations (sample size, NTU range) & future scope.
12. Conclusion & thank you / questions.

*(Report and PPT drafts to be created as separate final files once the remaining written content is compiled; this document provides the structure and source material mapping for both.)*
