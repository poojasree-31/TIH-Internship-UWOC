# Day 7 - Dataset Receipt & Initial Inspection

## Raw Data Preservation

The dataset was received as a GitHub project ZIP (`UWOC_useing_photoresistor-main`), with hardware code, GUI scripts, and several data files. The original ZIP and its extracted contents are kept as it is in the working folder; all analysis works from copies, not the original files.

## Files, Rows & Structure

| File | Rows | Columns |
|---|---|---|
| `anaotherGUI/1-2NTU.csv` | 8,513 | `labels`, `feature`, `bit` |
| `Graph/ALL/output.csv` | 400 | `S No`, `Binary Bit R`, `Binary Sent`, `Analog Val`, `Analog`, `1-2NTU` |
| `3ntu_photo.xlsx` | ~8,666 | Multiple unnamed/messy columns, needs further cleanup if used |

The primary file selected for this project is `anaotherGUI/1-2NTU.csv`, being the largest and cleanest.

## Labels, Targets & Metadata

- `labels` - true transmitted bit (0 or 1) - this is the target.
- `feature` - received analog signal value - this is the main input.
- `bit` - an existing threshold-based prediction from the original project (not a true label; flagged for further data leakage review).
- **Metadata gap found:** the file is named for the 1-2 NTU condition, but there is no explicit NTU column within the CSV itself - turbidity level is only known from the filename/folder context, not encoded as data.

## First-Look Checks (No Irreversible Cleaning)

- **Missing/invalid data:** no missing values found; `labels` and `bit` both only contain valid values (0, 1).
- **Duplicates:** a very high number of duplicate rows observed (8,486 of 8,512) - noted for deeper investigation on Day 8, not yet acted on.
- **Class/target coverage:** both classes (0 and 1) are present, with an about 62.5%/37.5% split.
- **Obvious inconsistencies:** none found in this file; however, the broader project folder structure shows that raw data for other turbidity ranges (2-3, 3-4, 4-5, 5-6 NTU) is **not** available - only result plot images exist for those conditions. This is the most important inconsistency versus the project's stated dataset expectations (Day 4).

## First-Look Statistics & Visualization

- `feature` column: min 0.337, max 0.625, mean ≈ 0.416, std ≈ 0.088 - values cluster into two visibly distinct groups rather than spreading smoothly.
- A first histogram of `feature` split by `labels` showed two clusters with a visible gap between them - flagged as worth deeper exploration in Week 2's EDA (Day 10), without drawing firm conclusions yet at this initial-inspection stage.

## Preliminary Dataset Report - Summary

The dataset is clean (no missing/invalid values) but has two notable characteristics carried forward into Week 2 for deeper investigation: (1) a very high duplicate-row count, likely tied to hardware sensor resolution rather than a data error, and (2) coverage limited to a single turbidity condition, which limits the project's ability to test cross-condition robustness until further data is provided.
