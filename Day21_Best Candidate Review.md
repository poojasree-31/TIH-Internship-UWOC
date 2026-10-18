# Day 21: Picking the Best Model So Far

## Before vs After This Week's Work

| Method | Test Accuracy | Test F1 | How Fast |
|---|---|---|---|
| Fixed Threshold | 51.7% | 55.4% | 0.0004s |
| Logistic Regression (tuned) | 75.0% | 63.4% | 0.0009s |
| Random Forest (default) | 75.0% | 69.4% | 0.0061s |
| SVM (scaled features) | 83.3% | 73.7% | 0.0013s |
| MLP (scaled features) | 80.0% | 71.4% | 0.0010s |

This week we found a clear winner. Once the features were scaled properly, SVM beat every other method on both accuracy and F1. It also stayed fast.

## What Went Right and What Went Wrong

- **What went right:** Once I started using the correct dataset with real multi condition data, the results finally made sense. The threshold method, which was the old hardware approach, turned out to be the weakest one. After I fixed the scaling problem, SVM and MLP became the strongest models.
- **What went wrong (and got fixed):** SVM and MLP failed badly at first on Day 16 and Day 17. They kept guessing 0 no matter what the input was. I found out why on Day 19. The two features were on very different number scales, and that confused both models. Scaling fixed it completely.
- **The robustness test on Day 20** showed that SVM beats the threshold at every single water condition. Also, SVM gets worse in a smooth and gradual way as the water gets murkier, which makes sense. The threshold just jumps around with no clear pattern.

## What's Still Weak About This Project

- The dataset is still small. There are only about 80 rows per water condition, and only 9 to 14 rows per condition in the test set. The exact percentages could shift a bit with more data.
- Logistic regression, even after tuning, has lower recall than SVM. It misses more real 1 bits than I would like.
- I only tested 5 NTU conditions, from 1 to 2 up to 5 to 6. I do not know how the model would behave in even murkier water beyond that range.

## Asking Mentor for the Green Light on Week 4

Plan for Week 4:
1. Go with SVM (with scaled features) as the final model, since it had the best accuracy, the best F1, and it got worse in the most sensible way across water conditions.
2. Do the final testing and packaging using this model.
3. Be honest in the final report about the small sample size per condition and the fact that the project only used real lab data from 1 to 2 NTU up to 5 to 6 NTU.
4. Explain the full story in the final report. The old threshold method does not hold up as water gets murkier, and a properly scaled ML model is a clear improvement.
