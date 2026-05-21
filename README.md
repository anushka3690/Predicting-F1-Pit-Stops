# Predicting F1 Pit Stops

## Project Overview

This project aims to build a machine learning model to **predict the probability of a pit stop occurring in the next lap** during F1 races. This is a **probability prediction task** where you must output probability scores (0.0 to 1.0) for each test observation.

### Dataset Summary

- **Training Set:** 439,140 race lap observations (IDs: 0-439139)
- **Test Set:** 188,166 observations (IDs: 439140-627304)
- **Target Variable:** `PitNextLap` (binary in training: 0 or 1)
- **Submission Format:** Probability predictions (0.0 - 1.0 range)
- **Evaluation Metric:** **Area Under the ROC Curve (AUC-ROC)** - measures model's ability to distinguish between pit stop and no pit stop across all probability thresholds
- **Class Distribution:** ~80% class 0 (no pit stop), ~20% class 1 (pit stop)
- **Missing Values:** None

### Evaluation Metric: AUC-ROC

Your model's performance is evaluated using **Area Under the Receiver Operating Characteristic Curve (AUC-ROC)**:

- **AUC-ROC Score:** Ranges from 0 to 1, where:
  - 1.0 = Perfect predictions
  - 0.5 = Random guessing
  - 0.0 = Completely wrong predictions
- Measures how well the predicted probabilities separate pit stops (class 1) from non-pit stops (class 0)
- Not affected by threshold choice - evaluates the quality of probability estimates across all thresholds
- **Your Goal:** Maximize AUC-ROC by producing well-calibrated probability predictions

### Critical Points

- Use `.predict_proba(X_test)[:, 1]` to get probabilities, NOT `.predict(X_test)`
- Submit values like 0.234, 0.876, 0.523 - NOT 0 or 1
- Higher probability values indicate higher confidence in pit stop occurring
- Your predictions will be evaluated on how well they discriminate between the two classes

### Features Available

**Categorical Features:**

- `Driver` (887 unique drivers)
- `Compound` (tire type: HARD, MEDIUM, INTERMEDIATE, SOFT, WET)
- `Race` (26 unique F1 races)
- `Year` (2022-2025)
- `PitStop` (pit stop counter for the race)

**Numerical Features:**

- `LapNumber` - Current lap number
- `Stint` - Current tire stint number
- `TyreLife` - Age of current tire (laps)
- `Position` - Current racing position
- `LapTime (s)` - Time for current lap in seconds
- `LapTime_Delta` - Difference from average lap time
- `Cumulative_Degradation` - Accumulated tire wear
- `RaceProgress` - Percentage of race completed
- `Position_Change` - Position change from previous lap

---

## Files in This Project

- `notebook.ipynb` - Main Jupyter notebook with all analysis and modeling code
- `train.csv` - Training dataset
- `test.csv` - Test dataset for final predictions
- `sample_submission.csv` - Template for submission format
- `README.md` - This file with project workflow guidance
