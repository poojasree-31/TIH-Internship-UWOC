# Day 5 - Pipeline & Experiment Planning

## Reproducible Workflow: Raw Data → Final Evaluation

```
1. Load raw dataset (preserve untouched copy)
2. Data quality audit (missing values, duplicates, invalid values, class balance, data leakage)
3. Cleaning (per audit findings; document every decision)
4. Stratified train/validation/test split (fixed random seed)
5. Baseline: fixed-threshold detection
6. ML models: Logistic Regression, SVM, Random Forest, optional MLP
7. Evaluation: accuracy, precision, recall and F1, confusion matrix, BER, inference time
8. Robustness analysis: performance across individual NTU levels
9. Comparison table + shortlisting possible models
10. Hypersetting tuning (shortlisted candidates only, validation set)
11. Final model selection + finalize
12. Error/checking wrong predictions
13. Final report, presentation, and being able to get the same result again documentation
```

## Baseline, Advanced Methods & Project-Specific Experiment

- **Baseline method:** fixed-threshold detection (single cutoff on signal value).
- **Advanced methods:** Logistic Regression, SVM, Random Forest, optional small MLP - trained and tested identically for fair comparison.
- **Project-specific experiment:** robustness across individual NTU levels - comparing how the fixed threshold vs. each ML method's performance changes (or doesn't) as turbidity increases. This is the project's core research contribution, pending multi-NTU raw data.

## Tentative Evaluation Criteria

- Accuracy, Precision, Recall, F1 Score
- Confusion Matrix
- BER / error rate
- Inference time (per prediction / per batch)

## Experiment Log Template

| Exp. ID | Date | Method | Hypersettings | Train/Val/Test Split | Accuracy | Precision | Recall | F1 | BER | Inference Time | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| EXP-001 | | Fixed Threshold | threshold=0.44 | 70/15/15 | | | | | | | |
| EXP-002 | | Logistic Regression | default | 70/15/15 | | | | | | | |
| EXP-003 | | SVM | default | 70/15/15 | | | | | | | |
| EXP-004 | | Random Forest | default | 70/15/15 | | | | | | | |
| EXP-005 | | MLP | hidden_layer=(8,) | 70/15/15 | | | | | | | |

## Repository / Folder Structure

```
TIH-Internship-UWOC/
├── data/
│   ├── raw/              # Untouched original dataset
│   └── processed_data/   # Cleaned, split train/val/test CSVs
├── notebooks/            # EDA, preprocessing, modelling notebooks
├── reports/               # Daily markdown deliverables (Day1 ... Day28)
├── results/               # Metrics, plots, confusion matrices, comparison tables
└── README.md
```

*(Note: current repo uses a flatter structure with daily .md files and a single main notebook at the root - this template reflects the target structure to move toward as the project scales up in Week 3-4, or can remain flat if simpler is preferred and approved by the mentor.)*
