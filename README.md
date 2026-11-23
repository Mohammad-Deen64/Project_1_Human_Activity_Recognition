# Human Activity Recognition Using Wearable Sensor Data

## 1. Project Overview

This project investigates Human Activity Recognition (HAR) using wearable sensor data from the MET dataset.

The objective is to classify everyday human activities using accelerometer (ACC) signals and machine learning techniques. The experiments focus on evaluating how well a model can recognize activities when tested on participants whose data was not used during training.

## 2. Dataset

**Dataset:** Wearable Sensor Dataset for Human Activity Recognition: Household Chores, Stairs, and Physiological Metrics

**Source:** [Zenodo – MET Dataset](https://zenodo.org/records/17671225)

**DOI:** https://doi.org/10.5281/zenodo.17671225

**License:** CC BY-NC-SA 4.0

The dataset contains wearable sensor recordings from seven participants:

- F-01
- F-02
- F-03
- M-01
- M-02
- M-03
- M-04

The available sensor measurements include accelerometer (ACC), blood volume pulse (BVP), electrodermal activity (EDA), temperature (TEMP), heart rate (HR), and inter-beat intervals (IBI).

This project uses accelerometer data for the experiments.

**Note:** The original dataset is not included in this GitHub repository. Download it from the original source and place it in the appropriate local dataset directory.

## 3. Technologies Used

- Python
- Jupyter Notebook
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- SciPy

## 4. Data Processing and Feature Extraction

The accelerometer signals were processed using the following approach:

- Accelerometer readings were converted using a scale factor of 64.
- Window size: 5 seconds (160 samples at 32 Hz).
- Window overlap: 50% (2.5 seconds).
- Statistical feature extraction was performed on the three accelerometer axes (X, Y, Z).
- Additional features were calculated from the accelerometer magnitude.

The statistical features included:

- Mean
- Standard deviation
- Minimum
- Maximum
- Median
- Root Mean Square (RMS)

Frequency-domain features were also investigated, including dominant frequency, spectral energy, and spectral entropy.

The resulting baseline feature dataset contained 2,759 windows and 21 numerical features, along with activity and participant information.

## 5. Machine Learning Experiments

The experiments investigated different machine learning approaches:

1. Random Forest using statistical features.
2. Random Forest with additional frequency-domain features.
3. Support Vector Machine (SVM) with an RBF kernel.
4. Extra Trees Classifier.

### Evaluation Strategy

Leave-One-Participant-Out (LOPO) cross-validation was used.

In this evaluation strategy, data from one participant is held out for testing while the remaining participants are used for training. This process is repeated across all seven participants.

This approach evaluates participant-independent performance rather than randomly splitting overlapping windows from the same participants.

## 6. Experimental Results

The baseline Random Forest model using statistical features achieved the following results:

| Metric | Score |
|---|---:|
| Accuracy | 64.19% |
| Balanced Accuracy | 52.39% |
| Macro F1-score | 52.49% |

### Model Comparison

| Model | Accuracy | Balanced Accuracy | Macro F1 |
|---|---:|---:|---:|
| Random Forest (Statistical Features) | 64.19% | 52.39% | 52.49% |
| Random Forest (Expanded Features) | 63.83% | 51.36% | 52.13% |
| SVM (RBF) | 54.48% | 47.81% | 44.55% |
| Extra Trees | 62.52% | 46.03% | 45.44% |

The baseline Random Forest model achieved the strongest overall performance among the evaluated approaches.

Adding frequency-domain features did not improve the overall results.

## 7. Observations

- Walking fast and washing dishes achieved relatively stronger classification performance.
- Rest was frequently confused with drawing.
- Upstairs and downstairs activities were difficult to classify, partly because of their limited number of samples.
- Performance varied considerably across participants.
- Participant-independent evaluation revealed challenges in generalizing across individuals.

Feature importance analysis indicated that accelerometer magnitude variability and axis-level RMS and standard deviation features were among the influential features.

## 8. Project Structure

```text
Project_01_Human_Activity_Recognition/
│
├── dataset/             # Local dataset (not uploaded)
│
├── notebooks/
│   └── 01_Human_Activity_Recognition_Experiments.ipynb
│
├── results/             # Experimental outputs
│
├── .gitignore
├── .gitattributes
└── README.md
```

## 9. Limitations

- The dataset contains recordings from only seven participants.
- Some activities have substantially fewer samples than others.
- Similar movement patterns can lead to activity misclassification.
- Performance differences across participants indicate that further investigation is needed to improve generalization.

The reported results should be interpreted in the context of this dataset and evaluation setup.

## 10. Future Work

Potential directions for further investigation include:

- Exploring additional machine learning and deep learning architectures.
- Investigating class imbalance and activity-specific performance.
- Improving recognition of similar activities.
- Evaluating additional sensor modalities.
- Investigating techniques for better generalization across participants.

## 11. Author

Mohammad Deen 
Graduate in Computer Science
GitHub: [Add your GitHub profile link here]

---

**Dataset Attribution:** Bermudez-Edo, M., Durán-López, A., Bolaños-Martinez, D., Garrido, J. L., & Rodriguez-Fortiz, M. J. (2025). *Wearable Sensor Dataset for Human Activity Recognition: Household Chores, Stairs, and Physiological Metrics*. Zenodo. https://doi.org/10.5281/zenodo.17671225
