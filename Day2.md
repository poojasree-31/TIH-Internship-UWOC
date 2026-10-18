# Day 2: Initial Implementation and Analysis

## Dataset Used

The corrected, combined dataset (`internship Dataset`), uploaded directly to Colab. It contains 399 rows and 6 columns:
- `S No`: row index
- `binary bit R`: an old, hardware threshold-based bit guess (not used as a model input, since it is really a prior prediction, not a true input)
- `Binary bit S`: the true transmitted bit (0 or 1), used as the target label
- `Analog value`: raw received signal value (0-255 range)
- `Analog Voltage`: normalized signal value (0-1 range), used as the main input feature
- `NTU`: which turbidity condition the row was measured under (5 conditions: 1-2NTU, 2-3NTU, 3-4NTU, 4-5NTU, 5-6NTU)

## First Look at the Data

A quick initial load confirmed:
- 399 rows total, roughly 80 rows per turbidity condition (79 to 80 each).
- `Binary bit S` label split: 242 rows labelled 0, 157 labelled 1 (about 61% / 39%), so the classes are a bit imbalanced.
- This dataset actually spans all 5 real turbidity levels the project is meant to study.

## Early Observation

Looking at the data briefly before doing any formal modeling, it was clear that `binary bit R` (the old hardware threshold guess) matches `Binary bit S` (the true label) almost perfectly at the lowest turbidity (1-2 NTU), but starts disagreeing more at higher NTU levels. This early observation turned out to be the main point of the whole project, and it was investigated properly later (Day 7 initial inspection, Day 8 data quality audit).

## Challenges / Limitations Identified

- With only around 80 rows per turbidity condition, the dataset is small. This will need careful, with a similar balance of 0s and 1s splitting later so each split has a fair mix of both classes and all conditions.
- `binary bit R` must be excluded from model training, since it already reflects a prior prediction attempt and including it would leak information about the answer.

