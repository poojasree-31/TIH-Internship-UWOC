# Day 7: Getting the Dataset and First Look

## 

## Files, Rows and Structure

| File | Rows | Columns |
| --- | --- | --- |
| Combined internship dataset | 399 | `S No`, `binary bit R`, `Binary bit S`, `Analog value`, `Analog Voltage`, `NTU` |

This single file covers five real turbidity conditions, roughly 80 rows per condition:

| NTU Condition | Row Count |
| --- | --- |
| 1 to 2 NTU | 79 |
| 2 to 3 NTU | 80 |
| 3 to 4 NTU | 80 |
| 4 to 5 NTU | 80 |
| 5 to 6 NTU | 80 |

## Labels, Targets and Metadata

- `Binary bit S`: the true transmitted bit (0 or 1). This is the target.
- `Analog Voltage`: the received analog signal value (normalized 0 to 1). This is the main input.
- `Analog value`: the raw sensor reading (0 to 255). It is the unnormalized version of `Analog Voltage`.
- `binary bit R`: an existing threshold based prediction of the bit from the original project. It is not a true label. Flagged for leakage review on Day 8, similar to the `bit` column in the previous dataset.
- `NTU`: records the turbidity condition for every row. In the earlier dataset we had to guess this from the filename.

## First Look Checks (No Irreversible Cleaning)

- **Missing/invalid data:** to be confirmed with `.isnull().sum()` once loaded (flagged for Day 8).
- **Duplicates:** to be checked on Day 8. This dataset is much smaller than the earlier one (399 vs 8512 rows), so duplicates may behave differently.
- **Class/target coverage:** both classes (0 and 1) are present. From looking at the data, the imbalance seems worse at higher NTU levels (more 0s). I will confirm this with numbers.
- **Obvious inconsistencies:** at low NTU (1 to 2 NTU), `binary bit R` matches `Binary bit S` in every visible row. At higher NTU levels (2 to 3 NTU onward), mismatches start appearing. This clearly shows the threshold method getting worse, which is exactly what this project is about.

## First Look Statistics and Visualization

To be completed once the full dataset is loaded and checked in code. Summary statistics of `Analog Voltage`, grouped by `NTU` and by `Binary bit S`, are planned for Day 8 onward.

## Preliminary Dataset Report: Summary

 dataset is small (399 rows), but it covers all five turbidity conditions we need for our main question. The clearest early sign is that `binary bit R` (the existing threshold prediction) disagrees more and more with the true label `Binary bit S` as NTU goes up. This shows the threshold method getting worse, which the earlier single condition dataset could never show.