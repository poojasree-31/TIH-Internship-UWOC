# Day 8 : Checking Data Quality

**Dataset:** Combined internship dataset, 399 rows, covering 5 water conditions (1-2NTU, 2-3NTU, 3-4NTU, 4-5NTU, 5-6NTU)

## What We Checked

- **Missing values:** none at all, every column is fully filled in.
- **Duplicate rows:** none, every row is unique.
- **How many 0s and 1s overall:** 242 rows are label 0, 157 rows are label 1. Not perfectly balanced, but not extreme either.
- **How many 0s and 1s per water condition:** each condition has somewhere between 29 and 47 of each label, roughly even across all 5 conditions. So the data isn't skewed toward any one water condition.

## Main Finding: How Often the Old Method Gets It Wrong

The dataset has a column (`binary bit R`) that already shows a guess from a simple threshold method, and we compared it to the real answer (`Binary bit S`) at each water condition:

| Water Condition | Mistakes | Total Rows | Mistake Rate |
|---|---|---|---|
| 1-2 NTU (clearest water) | 0 | 79 | 0% |
| 2-3 NTU | 5 | 80 | 6.25% |
| 3-4 NTU | 5 | 80 | 6.25% |
| 4-5 NTU | 40 | 80 | 50% |
| 5-6 NTU (murkiest water) | 34 | 80 | 42.5% |

This result is important for our project. In clear water, the simple threshold gets everything right. But once the water passes a certain murkiness, somewhere between 3-4 NTU and 4-5 NTU, the simple threshold starts failing badly, getting half the answers wrong at 4-5 NTU. This is the first real proof, using real data, that a simple cutoff method breaks down as water gets murkier. This is the main problem we are trying to solve in our project.

## Other Things We Noticed

- We also have a column called `binary bit R`. We only use `Binary bit S` as the true label.
- The dataset is quite small , only about 80 rows per water condition. This means our results are still useful, but not huge-scale, so we should mention this in our report.

## Cleaning Rules We're Going With

1. No duplicates to remove, data is already clean here.
2. No missing values to fix.
3. Don't use the `binary bit R` column as a model input, it's just a earlier guess, not the real answer.
4. Keep all 5 water conditions in our dataset since this is now the whole point of the project.
5. Be aware the dataset is small, so treat results carefully and mention this limit in the final report.
