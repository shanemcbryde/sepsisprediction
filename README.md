# Sepsis Prediction

## Background & Task

Sepsis is the leading cause of mortality in the United States and the most expensive condition associated with in-hospital stay, accounting for 6.2% (nearly $24 billion) of total hospital costs. In particular, Septic shock, the most advanced complication of sepsis due to severe abnormalities of circulation and/or cellular metabolism, reaches a mortality rate as high as 50% and the annual incidence keeps rising. It is estimated that as many as 80% of sepsis deaths could be prevented with early diagnosis and intervention; indeed prior studies have demonstrated that early diagnosis and treatment of septic shock can significantly decrease patients’ mortality and shorten their length of stay. In this capstone, your task is to build a machine learning model for accurate early diagnosis of septic shock.

## Methods

You will explore two categories of Machine Learning methods: one is Recent Temporal Patterns (RTPs) mining which will be used in conjunction with a Support Vector Machine (SVM) model and a Logistic Regression (LR) model (i.e., RTP-SVM and RTP-LR); the other is a powerful deep learning model named Long Short Term Memory (LSTM).

## MIMIC-III Datasets

Our dataset is a subset of MIMIC-III dataset. 1 The original MIMIC-III dataset contains admissions of adult patients (i.e., age > 16) who are admitted to intensive care units (ICU) at a tertiary referral hospital between 2001 and 2012, corresponding to 53,423 visits containing ∼11 million events.

### Selecting Features

Five features related to the sepsis progression were selected as suggested by clinicians:
1. Systolic Blood Pressure (SystolicBP)
2. Heart Rate (HeartRate)
3. Respiratory Rate (RespiratoryRate)
4. Temperature
5. White Blood Cell(WBC)

### Prediction Task and Final Dataset

Our goal for this Capstone project is: based on observation of a patient’s visit until 24 hours before an endpoint, we will predict whether or not a patient will develop septic shock 24 hours later. For septic shock visits, the endpoint is the onset time of septic shock while for non-shock visits, the endpoint is the end of sequences.

To conduct this task, we right aligned all the shock sequences by septic shock onset and all non-shock by the end of their sequences and include all the EHRs until 24 hours before the end of sequences (see Fig. 1).

As shown in Figure 1, the 24 hours leading up to the endpoint is denoted as prediction window and before that, is denoted as observation window. So the visits that contain no events in the observation window are excluded from the septic shock prediction task. As a result, the final datasets, MIMIC III shock.csv and MIMIC III nonshock.csv, have 796 visits (398 shock-positive visits and 398 negative visits) containing 37,246 events. Notably, MIMIC-III is ICU-specific and sepsis onset can present itself early, thus the number of remaining visits in MIMIC-III is relatively small after applying a 24-hour cut before the onset.

![Figure 1](https://user-images.githubusercontent.com/125444385/221104493-ef54afc0-c19c-4918-ae1f-67b7f16f8e60.png)

## Experiment Setup

You will employ RTP and long short-term memory (LSTM) as the prediction model since extensive previous works have demonstrated their robust and superior performance in EHRs modeling.

### RTP Mining

For RTP Mining, please explore the following parameters:

1. Maximum gap: explore between 4 and 10 hours, in increments of 1;
2. Support for the positive cases (shock): explore between 0.1 and 0.3, in increments of 0.05
3. Support for negative cases(non-shock): explore between 0.1 and 0.3, in increments of 0.05.

After retrieving the binary matrix for the train and test data, use the train data to fit a Support Vector Machine model and a Logistic Regression model (two independent models).

### Long Short Term Memory (LSTM)

For LSTM, please do the following:

1. Apply both padding and masking to the sequences. For masking, please use -10 as the fill value.
2. Create the model (using keras.layers) by first defining a Sequential model, then add a Masking layer, followed by a LSTM layer and lastly a Dense layer with 1 output neuron using sigmoid activation function. The LSTM layer should have 200 neurons within it. Use an Adam optimizer with a learning rate of 1e − 2. Compile the (Sequential) model with a Binary Cross-entropy loss function, pass in the Adam optimizer.
3. Fit the Sequential model (should contain 3 layers: Masking → LSTM [200 units] → Dense [1 unit, the output neuron]) with 10 epochs and report the performance when the batch size is 64, 128, and 256 respectively. In other words, there should be a different LSTM model for each possible batch size (i.e., LSTM-64, LSTM-128, LSTM-256).

## Evaluation Metrics

All models evaluated by a 5-fold cross-validation.

### Results

In your Jupyter notebook, please report:
* The best final RTP-LR model’s settings and/or hyper-parameters.
* The best final RTP-SVM model’s settings and/or hyper-parameters.
* The best final LSTM model’s settings and/or hyper-parameters.
* Present and compare the RTP-LR, RTP-SVM, LSTM’s results using the evaluation metrics: Accuracy, Recall, Precision, F1-score, and AUC under ROC.

### Final Report

In your Jupyter notebook, please critically evaluate the results of the experiments and describe the lessons learned: What specific things did you learn from doing this project? Did you learn anything about the problem itself, the approaches you tried, or the experiments you conducted? If there are any good ideas you came up with in the end but did not have time to pursue, this would be a good place to mention them.
