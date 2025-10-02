# 🧬 Sepsis Prediction via Temporal Pattern Mining & Deep Learning

This project tackles one of the most urgent challenges in healthcare: early detection of septic shock. Using ICU patient data from MIMIC-III, it compares temporal pattern mining with deep learning to identify high-risk patients up to 24 hours before onset. The goal is to maximize recall and minimize false negatives—where delayed intervention could mean the difference between life and death.

## 📊 Overview

The project evaluates two modeling paradigms:

- **Recent Temporal Pattern (RTP) Mining**  
  Frequent temporal patterns are extracted from patient vitals and used to train Support Vector Machine (SVM) and Logistic Regression (LR) classifiers.

- **Long Short-Term Memory (LSTM)**  
  A sequential neural network is trained on padded time-series data to learn latent temporal dependencies in patient vitals.

## 🎯 Objectives

- Predict septic shock onset 24 hours in advance using ICU vitals  
- Compare RTP-SVM, RTP-LR, and LSTM across five key metrics  
- Identify optimal model settings for clinical deployment  
- Propose strategies for extending the observation window without sacrificing predictive power

## 🧠 Model Architectures

**RTP Mining**
- Parameters: max gap (4–10 hrs), support thresholds (0.1–0.3)  
- Classifiers: SVM (poly kernel), LR  
- Output: Binary classification (Shock vs. Non-Shock)

**LSTM Neural Network**
- Layers: Masking → LSTM (200 units) → Dense (1 unit, sigmoid)  
- Padding: -10.0 fill value  
- Optimizer: Adam (learning rate = 0.01)  
- Epochs: 10  
- Batch sizes tested: 64, 128, 256

## 📁 Dataset

**Source**: MIMIC-III ICU admissions  
**Visits**: 796 (398 shock-positive, 398 non-shock)  
**Features Used**:
- Systolic Blood Pressure  
- Heart Rate  
- Respiratory Rate  
- Temperature  
- White Blood Cell Count  

**Observation Window**: All events ≥24 hours before diagnosis

## 📈 Evaluation Metrics

- Accuracy  
- Precision  
- Recall  
- F1 Score  
- AUC-ROC  

All models were evaluated using 5-fold cross-validation.

## 🔍 Key Findings

| Metric       | Best Method | Score |
|--------------|-------------|-------|
| Accuracy     | RTP-SVM     | 0.842 |
| Precision    | RTP-LR      | 0.831 |
| Recall       | RTP-SVM     | 0.977 |
| F1 Score     | RTP-SVM     | 0.860 |
| AUC-ROC      | RTP-LR      | 0.917 |

- **RTP-SVM** excels in recall and F1-score, making it the most clinically viable model for early intervention.  
- **RTP-LR** offers strong precision and AUC-ROC, minimizing false positives.  
- **LSTM** underperforms relative to RTP methods, likely due to limited sequence depth and feature granularity.

## 💡 Strategic Proposal

Inspired by Chi et al.’s work on RTP mining, this project achieved an F1-score of 0.860 with a 24-hour prediction window—nearly matching their 0.868 score with just 4 hours of lead time. This suggests a promising opportunity:  
**Extend the observation window in 4-hour increments until the minimum acceptable F1-score is reached**, enabling even earlier detection and intervention.

## ⚠️ Limitations

- MIMIC-III is ICU-specific and may not generalize to broader hospital populations  
- Only five vitals were used; additional features could improve performance  
- LSTM architecture was not tuned beyond batch size and layer depth  
- RTP mining relies on discretized event sequences, which may lose nuance

## 🛠️ Tools Used

[![TensorFlow](https://img.shields.io/static/v1?label=TensorFlow&message=Deep_Learning&labelColor=FF6F00&color=gray)](https://www.tensorflow.org/)
[![Keras](https://img.shields.io/static/v1?label=Keras&message=Deep_Learning&labelColor=FF0000&color=gray)](https://keras.io/)
[![Python](https://img.shields.io/static/v1?label=Python&message=Programming_Language&labelColor=3776AB&color=gray)](https://python.org)
[![Scikit-learn](https://img.shields.io/static/v1?label=Scikit--Learn&message=Metrics&labelColor=F7931E&color=gray)](https://scikit-learn.org)
[![Pandas](https://img.shields.io/static/v1?label=Pandas&message=Data_Handling&labelColor=150458&color=gray)](https://pandas.pydata.org)
[![NumPy](https://img.shields.io/static/v1?label=NumPy&message=Numerical_Computing&labelColor=013243&color=gray)](https://numpy.org)
[![Jupyter](https://img.shields.io/static/v1?label=Jupyter&message=Notebook&labelColor=F37626&color=gray)](https://jupyter.org)

## 📚 Reference Materials

- **MIMIC-III Clinical Database**  
  [https://physionet.org/content/mimiciii/1.4/](https://physionet.org/content/mimiciii/1.4/)  
  *A publicly available ICU dataset used for modeling patient trajectories and predicting septic shock.*

- **Recent Temporal Pattern Mining for Multivariate Time-series Classification**  
  [https://github.com/farzanehkh/RTP-mining-ICHI18](https://github.com/farzanehkh/RTP-mining-ICHI18)  
  *GitHub repository containing the RTP mining toolkit used for extracting temporal patterns from clinical sequences.*
