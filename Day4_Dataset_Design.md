# Day 4: Dataset Plan and Quality Checks

## Expected Files, Columns, Labels & Metadata 

- **Expected columns:** received analog signal value, transmitted bit label (target), turbidity/NTU level (metadata/condition).
- **Expected metadata:** which turbidity condition each row corresponds to, ideally covering multiple NTU levels so performance across water conditions can actually be tested.
- **Expected structure:** one row per transmission/measurement, consistently labelled.

## Likely Risks (Checklist)

| Risk Category | Specific Risk | Likelihood (pre-inspection estimate) |
|---|---|---|
| Missing data | Gaps in signal readings or missing NTU labels | Low-Medium |
| Annotation | Mislabeled bits due to manual/hardware logging errors | Low |
| Imbalance | uneven number of 0 and 1 labels (more 0s than 1s or vice versa) | Medium |
| Imbalance | Turbidity-condition imbalance (uneven rows per NTU level) | Medium |
| answer information accidentally getting into the inputs | A column that directly or indirectly reveals the target (e.g. a pre-computed prediction column) | Medium: worth checking explicitly |
| Sample size | Small overall dataset size, limiting split reliability | Medium-High: flagged as a risk to monitor once the real row count is known |
| Duplication | Repeated readings due to low sensor resolution, mistaken for data errors | Medium: depends on hardware ADC resolution |

## Train/Validation/Test Split: What Must Be Preserved

- **Class balance:** split that keeps the class balance similar so the ratio of 0s to 1s is consistent across train/val/test.
- **NTU condition coverage:** each split should include data from every available turbidity condition, so validation/test performance reflects real variation across water conditions, not just one easy condition.
- **No answer information accidentally getting into the inputs across splits:** ensure no reading is duplicated across both train and test in a way that inflates test performance.
- **running the same steps again:** fixed random seed for the split, documented and reused across all experiments.

## Dataset-Risk Checklist (Summary)

- [ ] Check for missing values in every column.
- [ ] Check for duplicate rows and understand their cause before deciding to keep/remove.
- [ ] Check class balance (bit label distribution), overall and per NTU level.
- [ ] Check row count per NTU condition: flag if any condition is too sparse for reliable evaluation.
- [ ] Check for any column that might leak the answer (e.g. a pre-existing prediction column).
- [ ] Confirm all labels are valid (only 0/1, no corrupted entries).
- [ ] Confirm feature values fall within an expected, reasonable for the sensor range.
