# Day 14 : Week 2 Summary

## What We Did This Week

- **Day 8:** Checked data quality on the new, correct dataset, no missing values, no duplicates. Found the big result: the old threshold method goes from 0% mistakes at 1-2 NTU to 50% mistakes at 4-5 NTU.
- **Day 9:** Planned a fair 70/15/15 split, decided to keep all the data as is.
- **Day 10:** Plotted the data and found that water condition really does shift where the signal values sit, which explains why a fixed cutoff stops working as water gets murkier.
- **Day 11:** Did the actual split, and this time added water condition as a real input feature, not just signal value.
- **Day 12:** Reviewed everything and locked it in as "Dataset V1."
- **Day 13:** Tried an new feature we calculated (distance from water-condition average), but it actually did worse than just using the raw signal value, so we kept things simple.



## Main Takeaway Going Into Week 3

We finally have real proof that water murkiness matters:  Our hope for Week 3 is that a proper ML model, especially one that uses water condition as an input, will do clearly better than the simple threshold, especially at higher NTU levels. 
