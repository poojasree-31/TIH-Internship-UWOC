# Day 27 - Final Mentor Review

## Methodology, results, software files and limitations

- **Methodology:** end-to-end pipeline from raw CSV → audit → cleaning → split → baseline/ML models → tuning → robustness simulation → error analysis → frozen final model (Days 1-26).
- **Results:** Logistic Regression selected as final model; perfect accuracy/F1 on real test data; simulated robustness study shows no clear ML advantage over fixed threshold under simple Gaussian noise proxy.
- **Software files:** notebook, processed_data/ (train/val/test CSVs), final_model/ (frozen .pkl), all daily markdown deliverables.
- **Limitations:** dataset covers only one real turbidity condition (1-2 NTU); Day 20's robustness findings are based on simulated noise, not real multi-condition data, and are explicitly flagged as such throughout.

## Repository, report and presentation status

- Repository: organized with daily deliverables, processed data, and final model files (Day 26).
- Report draft: outlined in Day 26, mapping each report section to its source day's work.
- Presentation draft: 12-slide outline prepared in Day 26.

## Final mentor corrections

*(To be filled in after the actual Mentor Review 9 meeting - record any requested changes to results framing, limitations disclosure, or report/PPT content here.)*

## Technical sign-off

*(To be completed once mentor corrections above are resolved and the mentor confirms results are approved for final submission.)*
