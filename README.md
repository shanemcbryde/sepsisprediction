# Sepsis Prediction

## Background & Task:

Sepsis is the leading cause of mortality in the United States and the most expensive condition
associated with in-hospital stay, accounting for 6.2% (nearly $24 billion) of total hospital costs.
In particular, Septic shock, the most advanced complication of sepsis due to severe abnormalities
of circulation and/or cellular metabolism, reaches a mortality rate as high as 50% and the annual
incidence keeps rising. It is estimated that as many as 80% of sepsis deaths could be prevented
with early diagnosis and intervention; indeed prior studies have demonstrated that early diagnosis
and treatment of septic shock can significantly decrease patients’ mortality and shorten their length
of stay. In this capstone, your task is to build a machine learning model for accurate early diagnosis
of septic shock.

## Methods:

You will explore two categories of Machine Learning methods: one is Recent Temporal Patterns
(RTPs) mining which will be used in conjunction with a Support Vector Machine (SVM) model
and a Logistic Regression (LR) model (i.e., RTP-SVM and RTP-LR); the other is a powerful deep
learning model named Long Short Term Memory (LSTM).

## MIMIC-III Datasets:

Our dataset is a subset of MIMIC-III dataset. 1 The original MIMIC-III dataset contains admissions of adult patients (i.e., age > 16) who are admitted to intensive care units (ICU) at a tertiary referral hospital between 2001 and 2012, corresponding to 53,423 visits containing ∼11 million
events.

### Selecting Features

Five features related to the sepsis progression were selected as suggested by clinicians:
1. Systolic Blood Pressure (SystolicBP)
2. Heart Rate (HeartRate)
3. Respiratory Rate (RespiratoryRate)
4. Temperature
5. White Blood Cell(WBC)

