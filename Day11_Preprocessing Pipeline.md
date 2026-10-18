# Day 11 : Splitting the Data
We have real data from 5 different water conditions. So along with the signal value, we also turned the water condition (`NTU`) into a number from 1 to 5 (1 = clearest, 5 = murkiest), so our models can actually use water condition as an input, not just the signal value.

## Cleaning Applied

- No missing values to handle.
- No duplicate rows to handle.
- `binary bit R` column excluded (it's just an old guess, not the real answer).
- `NTU` turned into a number (`NTU_level`, 1 to 5) so models can use it as an input.

## How We Split the Data

We split the data into training, validation, and testing, keeping the same mix of 0s and 1s in each part (split that keeps a similar mix of 0s and 1s):

- **Train:** 279 rows (70%)
- **Validation:** 60 rows (15%)
- **Test:** 60 rows (15%)

The balance between the two labels matched closely across train and test (about 60.5% label 0 in train, 61.7% in test), so the split is fair.

## Inputs Used

- `Analog Voltage` : the received signal value.
- `NTU_level` : the water condition, turned into a number from 1 (clearest) to 5 (murkiest).

## What We Saved

The split data is ready to use for every model from here on, so every method gets tested on the same training, validation and test groups, so we can compare them fairly.
