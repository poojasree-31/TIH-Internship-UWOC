# Day 13 : Testing an Extra Feature

## What We Tried

Since water condition clearly matters this time (see Day 10), we tried an new feature we calculated: instead of using the raw signal value, we calculated how far each signal value is from the average signal value for its own water condition. The idea was that this might help the model "see" what's unusual for that particular water condition.

## What We Compared

| Feature Set | Test Accuracy |
|---|---|
| Raw signal value + water condition | 76.7% |
| Engineered "distance from condition average" + water condition | 70.0% |

## What We Found

The raw signal value actually did better than our new feature we calculated. This makes sense when we think about it: the raw signal value already carries real information (how clear or murky the water is affects the number directly), but by converting it into "distance from average," we may have thrown away some of that useful information.

## Decision

We are keeping the raw signal value (`Analog Voltage`) plus water condition (`NTU_level`) as our two inputs, since this combination performed better. The new feature did not improve the result, so we decided not to use it.

## Redundancy Check

With only two inputs, there's little risk of redundancy. Both carry different information: the signal value tells us what was measured, and the water condition tells us the context that measurement was taken in.
