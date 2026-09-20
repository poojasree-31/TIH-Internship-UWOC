# Day 23 - Software Performance / Final Validation

## Final validation results

| Metric | Value |
|---|---|
| Test Accuracy | 1.0 |
| Test F1 | 1.0 |
| Total inference time (1,277 samples) | 0.00598s |
| Per-sample inference time | ~4.68 microseconds |
| Model file size | 1.11 KB |

## Comparison with the simple baseline

| Method | Accuracy | Per-Prediction Speed | Model Size |
|---|---|---|---|
| Fixed Threshold | 1.0 | Fastest (no model, direct comparison) | None (just a constant) |
| Logistic Regression (final) | 1.0 | ~4.68 μs/sample | 1.11 KB |

The fixed threshold remains marginally faster since it requires no model loading at all, but the Logistic Regression model is extremely lightweight (1.11 KB) and fast enough (microsecond-level per prediction) that this difference is negligible in any practical software context.

## Accuracy, complexity and runtime

- On the current dataset, there is **no accuracy trade-off** - Logistic Regression matches the fixed threshold and all other tested models perfectly.
- The trade-off that does exist is **model complexity vs. usefulness for future extension**: unlike a fixed threshold, Logistic Regression can be extended to incorporate additional features (e.g. turbidity/NTU level) once multi-condition data becomes available, without needing a full pipeline redesign.
- Given the tiny model size (1.11 KB) and negligible inference time, there is no meaningful software performance cost to choosing the ML model over the simpler threshold - reinforcing it as the practical final choice.

## Note for future hardware

Although hardware deployment is outside this project's mandatory scope, these figures (sub-microsecond model size, low inference time) indicate the frozen model would likely be lightweight enough for future embedded deployment, should that become a future-scope extension.
