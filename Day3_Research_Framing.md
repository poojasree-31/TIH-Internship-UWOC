# Day 3 - Research Framing & Mentor Review

## Refined Research Question

Can supervised machine learning classifiers (Logistic Regression, SVM, Random Forest, optional MLP), trained on received analog signal values, recover transmitted bits in underwater optical communication more robustly than a fixed threshold - particularly as water turbidity (NTU) increases?

## Measurable Outputs

- Accuracy, precision, recall, F1 score, confusion matrix, BER/error rate, and inference time - for each method, on a held-out test set.
- Robustness comparison: performance of each method across individual NTU levels (pending availability of multi-NTU raw data).

## 3-Slide Progress Pack

**Slide 1 - Work Completed:**
- Rewrote the problem statement in technical terms; defined inputs/output and success criteria.
- Drew the end-to-end software pipeline.
- Completed a literature review of 7 related UWOC/ML sources, with a comparison table and method shortlist.

**Slide 2 - Findings So Far:**
- The available dataset (`1-2NTU.csv`) covers only one turbidity condition; literature confirms ML models trained on one condition often don't work well to untrained conditions - directly relevant here.
- Classical ML methods (Logistic Regression, SVM, Random Forest) are well-supported in UWOC-adjacent literature and are appropriate first choices before considering deep learning.

**Slide 3 - Blockers & Next 3-Day Plan:**
- **Blocker:** No raw data yet for turbidity levels beyond 1-2 NTU, limiting the checking how well the model works central to this project.
- **Next 3 days:** Define expected dataset schema and a data-quality risk checklist (Day 4), plan the full experiment pipeline and folder structure (Day 5), and finalize Methodology V1 (Day 6) ahead of receiving/inspecting the dataset (Day 7).

## Target Definition, Dataset Structure, Metrics & Scope (to confirm with mentor)

- **Target:** transmitted bit label (0 or 1), per row of signal data.
- **Dataset structure (expected):** received analog signal value, transmitted bit label, turbidity/NTU level per row.
- **Metrics:** accuracy, precision, recall and F1, confusion matrix, BER/error rate, inference time.
- **Scope:** software-only; no hardware integration or physical data collection required.

## Mentor Notes / Decisions

*(To be filled in after the actual mentor review meeting - record any changes to target definition, dataset expectations, metrics, or scope here, and update assumptions accordingly.)*
