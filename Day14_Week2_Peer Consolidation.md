# Day 14 : Week 2 Summary

## What We Did This Week

- **Day 8:** Checked data quality on the new, correct dataset, no missing values, no duplicates. Found the big result: the old threshold method goes from 0% mistakes at 1-2 NTU to 50% mistakes at 4-5 NTU.
- **Day 9:** Planned a fair 70/15/15 split, decided to keep all the data as is.
- **Day 10:** Plotted the data and found that water condition really does shift where the signal values sit, which explains why a fixed cutoff stops working as water gets murkier.
- **Day 11:** Did the actual split, and this time added water condition as a real input feature, not just signal value.
- **Day 12:** Reviewed everything and locked it in as "Dataset V1."
- **Day 13:** Tried an new feature we calculated (distance from water-condition average), but it actually did worse than just using the raw signal value, so we kept things simple.

## Correction Note

This week's work replaces our earlier Week 2 work, which was done using the wrong dataset (one that only had one water condition). That earlier version made it look like every model got 100% accuracy, which wasn't a real test of our project's main question. This corrected version, using real data from all 5 water conditions, gives us a more realistic picture of the results.

## Main Takeaway Going Into Week 3

We finally have real proof that water murkiness matters: the old threshold method clearly gets worse as NTU increases. Our hope for Week 3 is that a proper ML model, especially one that uses water condition as an input, will do clearly better than the simple threshold, especially at higher NTU levels. Unlike before, this is now something we can test using the data we have.
