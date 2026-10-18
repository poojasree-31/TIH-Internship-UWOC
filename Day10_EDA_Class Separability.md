# Day 10: Looking at the Data Visually

## What We Plotted

We made two charts:

1. A histogram comparing signal values for label 0 vs label 1, across all water conditions combined.
2. A boxplot comparing signal values across each water condition separately.

## What We Found

**Chart 1: Label 0 vs Label 1, all conditions combined**

Label 0 and label 1 never overlapped, this real multi condition data actually overlaps, especially around 0.43 to 0.51. This makes sense. A signal value that means 1 in clear water might land in the same range as a 0 signal in murky water. When you mix every water condition together, the two groups start overlapping.

**Chart 2: Signal value by water condition**

This is the most useful chart we have made so far. As the water gets murkier (from 1 to 2 NTU on the left to 5 to 6 NTU on the right):

- The typical (median) signal value drops, from about 0.49 at 1 to 2 NTU down to about 0.37 to 0.43 at 4 to 5 and 5 to 6 NTU.
- The whole range of values shifts downward and gets narrower.

## Why This Matters

This explains our Day 8 finding. The fixed threshold worked perfectly at 1 to 2 NTU because the signal values there match what the cutoff expects. But as water gets murkier, the signal values shift down and do not match that same fixed cutoff anymore, so the cutoff starts guessing wrong more and more. That is exactly what we saw (0% mistakes at 1 to 2 NTU, jumping to 50% at 4 to 5 NTU).

## What This Means Going Forward

A smarter model might be able to notice that the right cutoff point should change depending on water condition, something a single fixed number can never do. This is the advantage we are hoping our ML models have over the simple threshold. And now we have real data to test it, not fake noise like before.

## Hypotheses for Our Models

1. A plain fixed threshold will likely keep failing more as NTU increases, matching the Day 8 numbers.
2. A model trained using water condition as an input (along with signal value) might do much better than one trained on signal value alone, since the right cutoff clearly depends on NTU.
3. We expect our ML models to clearly beat the simple threshold this time, especially at higher NTU levels.