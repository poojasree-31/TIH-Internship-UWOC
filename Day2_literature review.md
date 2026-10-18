# Day 2: Literature Review: Underwater Communication and Machine Learning

## Core Domain Concepts

- **UWOC (Underwater Wireless Optical Communication):** uses light (typically blue-green wavelengths, which penetrate water best) instead of radio waves to transmit data underwater.
- **Turbidity/scattering/absorption:** suspended particles in water scatter and absorb light, degrading the signal quality compared with background noise (SNR) and increasing number of bits detected incorrectly (BER) as distance or turbidity increases.
- **Fixed-threshold detection:** the traditional method of recovering bits by comparing received signal amplitude to a static cutoff; known to degrade as channel conditions (turbidity, distance) worsen.
- **ML/DL-based detection:** an active research trend replacing or augmenting fixed thresholds with adaptive, learned decision boundaries that can better handle varying and non-linear channel conditions.

## Literature / Method Comparison Table

| # | Source | Data/Setup | Approach | Metrics | Results | Limitations |
|---|---|---|---|---|---|---|
| 1 | PSK-HO-D / PSK-HE-D / ASK-HE-D detection in UWOC (Journal of Optics, Springer) | Simulated Jerlov water channels, 450-700 nm wavelengths | Compared coherent (PSK) vs direct (ASK) detection techniques under varying turbidity | Bit rate, transmitter power | PSK-HO-D outperformed the other two detection schemes at best wavelengths (450, 550 nm) | Simulation-only; no real ML classifier, purely physical-layer detection comparison |
| 2 | Deep Learning-Aided Signal Detection for SPAD-Based UWOC | SPAD (single-photon avalanche diode) receiver data | LSTM-based model with Sigmoid output for binary classification; dropout 0.3 to reduce overfitting | BER, SNR | Improved detection accuracy over conventional threshold methods in low-SNR conditions | Requires specialized SPAD hardware; deep model adds making a prediction complexity |
| 3 | DESN & CNN-TCN deep learning models for UWOC | Simulated/experimental UWOC channel data | Deep Echo State Network (DESN) and CNN-Temporal Convolutional Network compared for BER reduction | BER | Both DL models reduced BER versus starting method detection | High model complexity; not evaluated for lightweight/real-time using it in a real system |
| 4 | Turbidity-tolerant WDM UWOC (dense blue-green wavelength division multiplexing) | Multi-channel laser diode UWOC system | Turbidity-tolerant WDM combined with deep-learning-based signal detection (cited from Jiang et al.) | Data rate, crosstalk | Achieved >10 Gbit/s with minimal crosstalk under turbid conditions | Focused on high-end hardware systems, not simple low-cost receivers like a photoresistor |
| 5 | ML classification of OAM (orbital angular momentum) beams in turbid water (PubMed) | Laser beams through highly turbid water (~12 attenuation lengths), image-based | Convolutional Neural Network (CNN) to decode received beam images into multi-bit messages | Classification accuracy | Near-perfect classification, provided training data included the same turbidity conditions | Requires training data matched to each turbidity condition: does not work well on new data to unseen turbidity without retraining |
| 6 | Photon-Counting UWOC with Joint Source-Channel Coding | Photon-counting receiver, compressive sensing for video transmission | Coding-based error correction combined with photon-count signal extraction | BER, video quality | BER of 0.0421 at 100 kbps with clear video reconstruction | Focused on video/error-correction coding, not direct bit-classification via ML |
| 7 | Misalignment-Resilient Propagation Model for UWOC | Monte Carlo simulation, multi-lens receiver | Random Forest used to estimate transmitter-receiver offset/angle from power distribution | Mean square error (offset, angle) | Estimated offset within 5-6 mm, angle within ~0.16-0.17 rad | Random Forest used for alignment estimation, not directly for bit classification: but demonstrates RF's applicability to UWOC-adjacent regression/classification tasks |

## Observations

- Most advanced literature (CNN, LSTM, DESN, CNN-TCN) targets **high-complexity, high-turbidity, or long-range** UWOC systems using specialized hardware (SPAD receivers, laser/OAM beams): a different regime from this project's simple photoresistor-based receiver.
- A recurring theme (source #5) is that ML models trained on one turbidity condition **do not automatically work well on new data to a different, untrained condition**: this is directly relevant to this project, since the dataset covers multiple NTU levels and a model trained carelessly on just the easiest condition could give a misleading sense of how well it really works.
- Random Forest and other classical ML methods (source #7) do appear in UWOC-adjacent literature for regression/estimation tasks, supporting their inclusion here for direct bit classification.
- No literature source found directly matches this project's exact setup (low-cost photoresistor receiver + classical ML bit classification across NTU levels): reinforcing that this project's "project-specific analysis" (NTU-level performance across water conditions comparison) is a genuine, less-explored angle.

## selected for the next step Candidate Methods

Per the problem statement's required scope, the following are selected for the next step for implementation: 1. **Fixed-threshold starting method**: required for direct comparison against ML methods.
2. **Logistic Regression**: simple, fast, interpretable linear classifier.
3. **SVM**: can capture non-linear boundaries if class separation isn't perfectly linear at higher turbidity.
4. **Random Forest**: supported by literature (source #7) as effective for UWOC-adjacent classification/regression; handles non-linear patterns.
5. **Optional small MLP**: included for completeness, informed by literature showing deep learning can improve detection in harder (low-SNR/high-turbidity) conditions (sources #2, #3), even though this project's current data is comparatively simple.
