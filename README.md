# EEG-States-Classification
 To tackle the task of classifying cognitive states using EEG data and deep learning models
<br><br>

Overview - 

This repository contains a comprehensive analysis and classification of EEG data. The notebook EEG_classify.ipynb focuses on exploring various preprocessing, feature extraction, and machine learning techniques to classify EEG signals into different states (Rest state or Task State)

![EEG Classification](https://github.com/universalus/EEG-States-Classification/blob/main/eeg_test_img.webp)
<br><br>

Table of Contents
1. Introduction
2. Data Description
3. Preprocessing
4. Feature Extraction
5. Modeling and Classification
6. Results
7. Conclusion
8. Dependencies
<br><br>

### Introduction -

Electroencephalography (EEG) is a non-invasive method to record electrical activity of the brain. The primary goal of this project is to classify EEG signals into rest and task states using various machine learning models. This notebook provides a step-by-step approach to preprocess the data, extract meaningful features, and apply classification algorithms to achieve high accuracy.

Dataset Link : https://physionet.org/content/eegmat/1.0.0/
<br><br>

### Data Description -

Input Shape: (72, x, 21, 500) ; where x is inconsistent

This shape corresponds to (samples/subjects, segments/trials, channels/electrodes, time points/samples per segment)
<br><br>

Options to deal with inconsistent data and problems :

i.   Padding : Introduces artificial data, inefficient

ii.  Truncating : Loss of data

iii. Segmentation : Disrupts temporal continuity

Solution: We Flatten the data to make it consistent and use PCA (Principal Component Analysis) or UMAP (Uniform Manifold Approximation and Projection) for Data Reduction 

Problems with this Solution : Loss of Structural Information and potential overfitting of models trained
<br><br>

Better Solution : Use Reshape, since channels and samples per segment are consistent in the data.

We can reshape it to (samples/subjects * segments/trials, channels/electrodes, time points/samples per segment)

Advantages: Makes the data consistent, maintains Structural Information, increases size of samples in data in significant amount which reduces overfitting, and several EEG classification models support Temporal data
<br><br>

### Preprocessing & Feature Extraction -

-> Standardization is preferred due to the varying nature of EEG signals and the need to maintain the relative relationships between different channels and time points.


-> Feature Extraction : Key Features are computed as the power within the band which is computed as the mean of the PSD values corresponding to these frequencies. The chosen frequency bands are critical in EEG analysis because different frequency ranges are associated with various cognitive and physiological processes.

Significance of selected bands -

1. Delta (0.5 - 4 Hz): Associated with deep sleep and unconsciousness, prominent during slow-wave sleep.
2. Theta (4 - 8 Hz): Linked to light sleep, relaxation, and meditation; plays a role in memory formation and navigation.
3. Alpha/Mu (8 - 12 Hz): Related to relaxed wakefulness and meditative states; mu waves are specific to motor areas and mirror neuron activity.
4. Low Alpha (8 - 10 Hz): Indicative of a relaxed, yet alert mental state; often observed during quiet, restful states.
5. High Alpha (10 - 12 Hz): Seen during relaxed, focused states; can be increased with mindfulness and attention.
6. Beta (12 - 30 Hz): Associated with active thinking, focus, and problem-solving; present during cognitive and motor activities.
7. Low Beta (12 - 15 Hz): Related to relaxed focus and calm attention; often seen in tasks requiring sustained mental effort.
8. Mid Beta (15 - 20 Hz): Linked to active problem-solving and engagement; associated with alertness and excitement.
9. High Beta (20 - 30 Hz): Connected to heightened alertness, stress, and anxiety; seen during intense mental activity.
10. Gamma (30 - 100 Hz): Involved in high-level cognitive functions, sensory perception, and consciousness; linked to memory binding and integration.
11. Low Gamma (30 - 50 Hz): Plays a role in sensory processing and higher cognitive functions; often seen during focused attention.
12. High Gamma (50 - 100 Hz): Associated with complex problem-solving, peak performance, and heightened awareness.
13. Epsilon (0.1 - 0.5 Hz): Present in very deep meditative states and near-death experiences; not commonly observed in typical EEG studies.
14. Sigma (12 - 16 Hz): Characteristic of sleep spindles during Stage 2 sleep; involved in sleep maintenance and memory consolidation.
15. High-Frequency Oscillations (100 - 500 Hz): Linked to various cognitive and motor functions; often observed during rapid information processing.
16. Ripples (80 - 200 Hz): Associated with memory consolidation and information transfer in the hippocampus; seen during sharp wave-ripple events in sleep.
17. Fast Ripples (200 - 500 Hz): Related to pathological activity in epilepsy and high-frequency cognitive processes; may indicate regions prone to seizures.

![EEG Classification](https://github.com/universalus/EEG-States-Classification/blob/main/eeg_waves_img.webp)
<br><br>


### Modeling and Classification -


EEGNet: A compact convolutional neural network tailored for EEG signal classification.

Tsception: A temporal convolutional neural network designed for time-series data.

ATCNet: Attention-based Temporal Convolutional Network focusing on important time-series features.

LSTM RNN: A Long Short-Term Memory Recurrent Neural Network to capture temporal dependencies in the EEG signals.
<br><br>


### Results -

The models achieved the following evaluation metrics on the test set:

| Model      | Accuracy | Precision | Recall  | F1-score |
|------------|----------|-----------|---------|----------|
| EEGNet     | 81.91%   | 83.28%    | 82.08%  | 79.08%   |
| TSCeption  | 90.50%   | 90.31%    | 90.50%  | 90.34%   |
| ATCNet     | 80.36%   | 83.64%    | 94.93%  | 88.81%   |
| LSTM RNN   | 82.09%   | 81.04%    | 82.09%  | 80.94%   |

<br>


### Conclusion -

Accuracy: TSCeption has the highest accuracy at 90.49%, indicating it correctly predicts the highest proportion of instances overall.

Precision vs. Recall:

  Precision is highest in TSCeption, meaning it is best at minimizing false positives.
  
  Recall is highest in ATCNet, meaning it is best at minimizing false negatives.
  
F1-Score: TSCeption again leads with the highest F1-score, which means it maintains a good balance between precision and recall.<br><br>


Overall TSCeption is the best performing model across most metrics.


### Dependencies -

The project requires the following Python packages:

1. numpy
2. scipy
3. pandas
4. matplotlib
5. scikit-learn
6. tensorflow
7. mne

