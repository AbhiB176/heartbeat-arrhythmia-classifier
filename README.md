# Heartbeat Arrhythmia Classifier (ECG)

Course project for **ITSC-3146: Introduction to Data Mining**.  
This project builds a heartbeat-level classifier using ECG signals from the **MIT-BIH Arrhythmia Dataset**, focusing on preprocessing, segmentation, and class imbalance challenges.

---

## Overview

- Dataset: MIT-BIH Arrhythmia Database
- Task: Binary heartbeat classification (Normal vs Arrhythmic)
- Signal type: ECG (MLII lead)
- Model: Random Forest Classifier
- Key challenges: noisy signals, segmentation, severe class imbalance

---

## Dataset & Signal Characteristics

- 47 subjects, ~30 minutes of ECG per subject
- Sample rate: 360 Hz
- Two ECG leads per recording (MLII used here)
- Heartbeat annotations provided per sample

Due to compute and time constraints, this project focuses on **one subject (~30 minutes, ~650k samples)**.

---

## Feature Extraction & Preprocessing

ECG data is noisy and not organized by heartbeat, so preprocessing was a core part of this project.

**Key steps:**
- ECG cleaning and noise removal
- R-peak detection (automated + manual fallback)
- Heartbeat segmentation centered on R-peaks
- Z-score normalization per heartbeat
- Resampling each beat to a fixed length (200 samples)
- Annotation alignment and filtering of unknown labels

Feature extraction and signal processing were implemented using **NeuroKit2**.

---

## Data Exploration

Before modeling, several visual checks were performed:
- Raw vs cleaned ECG signals
- R-peak alignment with true heartbeat peaks
- Normalized heartbeat segments by class

Observations:
- Strong class imbalance (≈2200 normal vs ≈30 arrhythmic beats)
- Significant variability between heartbeats
- Visualization confirmed the importance of segmentation and normalization

---

## Modeling

A **Random Forest Classifier** was used due to its robustness to noise and ability to model non-linear patterns.

**Setup:**
- Binary classification (Normal vs Arrhythmic)
- Stratified 70/30 train-test split
- `class_weight="balanced"` to address imbalance
- Beats labeled as “Unknown” were excluded

---

## Results & Interpretation

- Normal beats were classified almost perfectly
- Arrhythmic beats were often missed due to class imbalance
- Overall accuracy was high but misleading
- Minority-class F1 score was low (~0.36)

**Key takeaway:**  
Accuracy alone is insufficient for imbalanced medical datasets; preprocessing and evaluation metrics matter more than raw performance.

---

## Limitations & Future Work

- Extremely limited arrhythmic samples
- Single-subject focus
- No resampling or synthetic data augmentation

Future improvements could include:
- SMOTE or other imbalance-handling techniques
- Multi-subject training
- More expressive models (CNNs on raw signals)
- Better heartbeat alignment and normalization

---

## Impact & Considerations

- **Clinical:** Automated filtering of normal beats could reduce clinician workload
- **Ethical:** Missed arrhythmic detections highlight the need for human oversight
- **Technical:** Demonstrates real-world challenges of noisy, imbalanced medical data

---

## Tools & References

- MIT-BIH Arrhythmia Database
- NeuroKit2
- scikit-learn

> *ChatGPT was used to assist with report structuring and code refactoring.*
