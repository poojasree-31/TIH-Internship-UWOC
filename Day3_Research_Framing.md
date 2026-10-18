# Day 3: Research Question and Mentor Review

## Refined Research Question

Can supervised machine learning classifiers (Logistic Regression, SVM, Random Forest, optional MLP), trained on received analog signal values, recover transmitted bits in underwater optical communication more robustly than a fixed threshold: particularly as water turbidity (NTU) increases?

## things I will measure

- Accuracy, precision, recall, F1 score, confusion matrix, BER/error rate, and prediction time: for each method, on a test set.
- performance across water conditions comparison: performance of each method across individual NTU levels (pending availability of multiple NTU raw data).

## 3-Slide Progress Pack

**Slide 1: Work Completed:**
- Rewrote the problem statement in technical terms; defined inputs/output and success criteria.
- Drew the full software pipeline.
- Completed a literature review of 7 related UWOC/ML sources, with a comparison table and method shortlist.

**Slide 2: Findings So Far:**
- Literature confirms ML models trained on one turbidity condition often don't work well on new data to untrained conditions, so the dataset will need to be checked carefully to make sure all turbidity conditions are properly represented and tested, not just the easiest one.
- Classical ML methods (Logistic Regression, SVM, Random Forest) are well-supported in UWOC-adjacent literature and are appropriate first choices before considering deep learning.

**Slide 3: Blockers & Next 3-Day Plan:**
- **Blocker:** The dataset has not been formally inspected yet, so the exact columns, row counts per turbidity condition, and data quality are still unconfirmed.
- **Next 3 days:** Define expected dataset schema and a data quality risk checklist (Day 4), plan the full experiment pipeline and folder structure (Day 5), and finalize method V1 (Day 6) ahead of formally inspecting the dataset (Day 7).

## Target Definition, Dataset Structure, Metrics & Scope (to confirm with mentor)

- **Target:** transmitted bit label (0 or 1), per row of signal data.
- **Dataset structure (expected):** received analog signal value, transmitted bit label, turbidity/NTU level per row.
- **Metrics:** accuracy, precision, recall, F1, confusion matrix, BER/error rate, prediction time.
- **Scope:** software-only; no hardware integration or physical data collection required.


