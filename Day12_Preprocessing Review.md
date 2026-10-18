# Day 12 : Finalising the Cleaned Data

## Summary So Far

- **Data quality (Day 8):** No missing values, no duplicates. 242 label-0 rows, 157 label-1 rows overall. The old threshold method goes from 0% mistakes at 1-2 NTU to 50% mistakes at 4-5 NTU, real proof the simple cutoff breaks down as water gets murkier.
- **EDA (Day 10):** When all water conditions are combined, labels 0 and 1 overlap more than before. Signal values shift lower and get squeezed as water gets murkier, which explains why a fixed cutoff stops working.
- **Split (Day 11):** 70/15/15 train/val/test split, with water condition (`NTU_level`) added as a real input feature this time, not just signal value.

## Decisions We Made

1. **Including NTU as a feature** : this makes sense since Day 10 showed water condition really does change where the "right" cutoff should be.
2. **Not using `binary bit R`** : it's just an old guess, not the real answer, so it stays out of training.
3. **No special balancing for the 60/40 class split** : not extreme enough to need fixing yet.
4. **Being upfront about our small dataset** : only about 80 rows per water condition, so results should be treated as a solid first look, not a huge-scale, completely certain result.

## Locked In: Dataset V1

- **Train:** 279 rows
- **Validation:** 60 rows
- **Test:** 60 rows
- **Inputs:** signal value (`Analog Voltage`) and water condition (`NTU_level`)
- **Target:** true transmitted bit (`Binary bit S`)

We will use this version of the dataset for the models we test next.
