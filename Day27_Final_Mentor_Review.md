# Day 27: Mentor Review

## method, Results, Software files & Limitations Presented

- **method:** full pipeline from raw CSV, covering all 5 real turbidity conditions, through audit, cleaning, split, starting method/ML models, feature scaling fix, finding better model settings, real per-condition performance across water conditions testing, error analysis, and a frozen final model (Days 1-26).
- **Results:** SVM with scaled features selected as the final model. It reached 83.3% accuracy and 73.7% F1 on the real test set, clearly beating the original fixed-threshold method (51.7% accuracy). It also beat the threshold at every individual turbidity condition tested, and got worse gradually and sensibly as the water got murkier, instead of failing unpredictably like the threshold did.
- **Software files:** notebook, processed_data/ (train/val/test CSVs), final_model/ (frozen SVM model and scaler), all daily markdown deliverables.
- **Limitations:** the dataset has a relatively small number of rows per turbidity condition (about 80 each), and only covers turbidity from 1-2 NTU up to 5-6 NTU. Performance beyond that range is unknown.

## Repository, Report Draft & Presentation Draft Status

- Repository: organized with daily deliverables, processed data, and final model files (Day 26).
- Report draft: outlined in Day 26, mapping each report section to its source day's work.
- Presentation draft: 12-slide outline prepared in Day 26.



