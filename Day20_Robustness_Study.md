# Day 20 Robustness Study (Testing at Different Noise Levels)

## Why We Did This

Right now we only have real data for one water condition (1-2 NTU). Since we don't have data for murkier water, we made our own fake "murky water" by adding random noise to the signal values. More noise = pretending the water is murkier. This is not real data, just a way to test the idea while we wait for the actual higher NTU data.

## What We Tested

We added different amounts of random noise to the signal and checked how well the threshold method and the Logistic Regression model could still guess the correct bit.

| Noise Amount | Threshold Accuracy | Threshold F1 | Logistic Regression Accuracy | Logistic Regression F1 |
|---|---|---|---|---|
| 0.00 (no noise) | 1.000 | 1.000 | 1.000 | 1.000 |
| 0.01 | 1.000 | 1.000 | 1.000 | 1.000 |
| 0.02 | 1.000 | 1.000 | 1.000 | 1.000 |
| 0.03 | 0.999 | 0.999 | 0.998 | 0.998 |
| 0.05 | 0.968 | 0.957 | 0.969 | 0.959 |
| 0.08 | 0.878 | 0.843 | 0.879 | 0.841 |

## What We Found

- With little or no noise, both methods get everything right, just like before.
- Once we add more noise, both methods start making mistakes, and they get worse at about the same speed.
- The big finding: Logistic Regression did NOT do better than the simple threshold here. They both fail at almost the same rate. The difference between them is tiny, less than 0.002 accuracy at any noise level.

## What This Means

Since we just added plain random noise, both methods handle it the same way because they're both basically drawing one straight cutoff line to separate the two groups. To actually see ML do better than a simple threshold, we'd probably need real messy water data, where the noise isn't just random but behaves in a more complicated, uneven way. Plain random noise isn't a perfect stand-in for real turbidity.

## What's Next

This test is a decent placeholder to show we built the process correctly, but it doesn't prove that ML is better than a simple threshold. We should ask for real data from more turbidity levels so we can test this properly instead of just guessing with fake noise.
