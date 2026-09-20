# Day 21 : Picking the Best Model So Far

## Before Tuning vs After Tuning

| Method | Test Accuracy | Test F1 | How Fast |
|---|---|---|---|
| Fixed Threshold | 1.0 | 1.0 | 0.00066s |
| Logistic Regression (tuned) | 1.0 | 1.0 | 0.0023s |

Tuning the settings didn't change anything, both still got everything right on the real data. In the fake noisy-water test (Day 20), both methods failed at about the same rate, so we still can't say ML clearly beats the simple threshold yet.

## What Went Right and What Went Wrong

- **What went right:** On the real data we have, every method got 100% correct. No mistakes at all.
- **What went wrong (in the fake noise test):** Once we added enough random noise, both methods started getting things wrong near the same point, right where the signal value crosses the line between "0" and "1."

## What's Still Weak About This Project

- Everything looks perfect right now because the real data we have is simple, both groups are already far apart with no overlap.
- The one surprising thing: Logistic Regression didn't beat the simple threshold in the fake noise test, they failed almost equally. That's worth talking to the mentor about.
- The biggest weak point overall is still not having real data from murkier water. Everything else depends on getting that.

## Asking Mentor for the Green Light on Week 4

Plan for Week 4:
1. Go with Logistic Regression as the final model, since it's simple, fast, and does just as well as everything else.
2. Do the final testing and packaging using the data we currently have.
3. Be upfront in the final report that we didn't get to test with real murky-water data, so the results are limited.
4. If real data for other turbidity levels shows up before Week 4 ends, redo the noise test with real data instead of fake noise, that would matter more than polishing the rest.
