# Day 4 - Dataset Design & Quality Expectations

## Expected Files, Columns, Labels & Metadata (Before Using Final Dataset)

- **Expected columns:** received analog signal value (feature), transmitted bit label (target, 0/1), turbidity/NTU level (metadata/condition).
- **Expected metadata:** which turbidity condition each file/row corresponds to; ideally, multiple files or a column covering a range of NTU levels (not just one condition).
- **Expected structure:** one row per transmission/measurement, similarly labelled.

## Likely Risks (Checklist)

| Risk Category | Specific Risk | Likelihood (pre-inspection estimate) |
|---|---|---|
| Missing data | Gaps in signal readings or missing NTU labels | Low-Medium |
| Annotation | Mislabeled bits due to manual/hardware logging errors | Low |
| Imbalance | Class imbalance (more 0s than 1s or vice versa) | Medium |
| Imbalance | Turbidity-condition imbalance (far more data at one NTU level than others) | High - found likely, since only 1-2 NTU has been made available so far |
| Leakage | A column that directly or indirectly reveals the target (e.g. a pre-computed prediction column) | Medium - worth checking explicitly |
| Temporal | Signal drift over time within a session, not captured by static features | Low-Medium |
| Duplication | Repeated readings due to low sensor resolution, mistaken for data errors | Medium - depends on hardware ADC resolution |

## Train/Validation/Test Split - What Must Be Preserved

- **Class balance:** balanced split so the ratio of 0s to 1s is similar across train/val/test.
- **No data leakage across splits:** ensure the same exact reading isn't duplicated across both train and test in a way that inflates test performance (a risk given expected duplicate/repeated readings).
- **Condition coverage:** ideally, each split should include data from every available turbidity condition, so validation/test performance reflects real-world variation - not just one easy condition.
- **Reproducibility:** fixed random seed for the split, documented and reused across all experiments.

## Dataset-Risk Checklist (Summary)

- [ ] Check for missing values in every column.
- [ ] Check for duplicate rows and understand their cause before deciding to keep/remove.
- [ ] Check class balance (bit label distribution).
- [ ] Check turbidity/coverage of water conditions - flag if data is concentrated in one condition.
- [ ] Check for any column that might leak the answer (e.g. a pre-existing prediction).
- [ ] Confirm all labels are valid (only 0/1, no corrupted entries).
- [ ] Confirm feature values fall within an expected, physically plausible range.
