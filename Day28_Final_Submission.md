# Day 28: Practice Presentation and Final Submission

## Mock Presentation Notes

*(To be completed after actually running through the presentation with peers: note timing, clarity issues, and any questions you struggled to answer, so they can be addressed before the real final presentation.)*

## running the same steps again Verification Checklist

- [ ] Repository link is public/accessible (update with your new repo's link after recreating it).
- [ ] Notebook runs top-to-bottom without errors on a fresh Colab session (re-verify before final submission).
- [ ] Dataset reference/instructions are clear (upload `internship Dataset`, the combined 5-NTU-condition file, when prompted).
- [ ] `final_model/svm_final.pkl` and `final_model/scaler_final.pkl` both load correctly and produce expected predictions together.
- [ ] `processed_data/X_train.csv`, `X_val.csv`, `X_test.csv` (and matching y files) are present and match the split used in the notebook.
- [ ] All 28 daily markdown files are present in the repository, reflecting the corrected (restarted) version of the project.
- [ ] README includes setup and run instructions, and clearly states that the scaler must be applied before using the model (Day 26).

## Final Submission Package

| Deliverable | Status | Location |
|---|---|---|
| Problem Understanding Note & Literature Review | Complete | Day1, Day2 |
| Dataset Understanding / Quality Report | Complete | Day4, Day7, Day8 |
| Preprocessing / EDA Notebook | Complete | Day9-12, notebook |
| Feature / Representation Preparation | Complete | Day13 |
| starting method Model / Method Notebook | Complete | Day15 |
| Advanced Model / Method Experiments | Complete | Day16, Day17 |
| Model / Method Comparison and Experiment Log | Complete | Day18 |
| finding better model settings & Feature Scaling Fix | Complete | Day19 |
| Project-Specific performance across water conditions / Error Analysis | Complete, using real multiple-condition data | Day20, Day25 |
| Final Model / Software Pipeline and Output files | Complete | Day22, Day23, final_model/ |
| Clean Source-Code Repository with README | Complete | Day26 |
| Final Individual Project Report | Drafted (outline complete; full write-up pending) | Day26 outline |
| Final Individual Presentation and Future Scope | Drafted (slide outline complete; slides pending) | Day26 outline |

## Project Summary (For the Final Write-Up)

This project set out to test whether a machine learning model could classify transmitted bits in an underwater optical communication system better than a simple fixed-threshold method, especially as water turbidity increases. Using real data across 5 turbidity conditions (1-2 NTU through 5-6 NTU), the final results confirm this: - The fixed threshold method got only 51.7% accuracy overall, and its accuracy jumped around unpredictably across conditions (as low as 28.6% at times).
- The final SVM model (with properly scaled features) reached 83.3% accuracy and clearly outperformed the threshold at every single turbidity condition.
- The SVM model's performance also got worse in a sensible, gradual way as turbidity increased (100% at the clearest conditions down to 61.5% at the murkiest), unlike the threshold's erratic behavior.
- Most of the SVM model's remaining errors (9 out of 10) happen at the two murkiest conditions, and are mostly missed "1" bits rather than false alarms.

This project was restarted partway through after discovering the first attempt used an incorrect, one-condition dataset. The corrected results here are based on real data from all 5 turbidity conditions and give an honest, useful answer to the project's original question.

## Future Scope (Carried from Problem Statement)

- Multi-level modulation.
- Adaptive online learning.
- Sequence-aware decoding and embedded receiver using it in a real system.
- Extension using a larger dataset, especially more rows per turbidity condition, and testing turbidity levels beyond 5-6 NTU.
