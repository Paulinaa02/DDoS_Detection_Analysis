# DDoS Attack Detection and Analysis in EV Charging Systems using Machine Learning

## Project Overview

This project focuses on detecting **Distributed Denial of Service (DDoS)** attacks targeting **Electric Vehicle (EV) charging systems** through the application of machine learning techniques. Developed as part of my engineering thesis, the goal is to identify malicious behavior based on performance data from real-world EV charging stations.

The system implements a **binary classification** approach to classify traffic as either:
- `0`: Normal connection
- `1`: Attack attempt

---

## 📁 Dataset

The dataset used in this project is derived from the **CICEV2023** collection, which includes logs from EV charging stations during both standard operation and simulated DDoS attacks. The dataset required preprocessing for various reasons in order to be properly prepared for machine learning.

To streamline usage, I provide two preprocessed `.txt` files for direct use:
- **`CORRECT_ID.txt`** – Contains combined and labeled data from attacks and normal sessions, using valid EV identifiers but with invalid keys.
- **`WRONG_ID.txt`** – Contains combined and labeled data from scenarios with invalid EV identifiers.

Each file includes rows that represent data samples with features already labeled (`0` or `1`).

You can use these files directly for training and testing without further data cleaning.

### Dataset Features:
Captured every **0.1 milliseconds**:
- `branch`
- `branch-miss`
- `context-switch`
- `CPU-migration`
- `cycle`
- `instruction`
- `page-fault`
- `task-clock`

These system-level features, related to CPU operations, are crucial for identifying malicious anomalies indicative of DDoS attacks.

---

## Models Used

### Algorithms:
- ✅ Fully Connected Neural Network (FNN)
- ✅ Multi-Layer Perceptron (MLP)
- ✅ Gradient Boosting (GB)
- ✅ Random Forest (RF)
- ✅ Logistic Regression (LR)

A **meta-model** based on Logistic Regression was also built on top of the base models to further enhance performance.

### Preprocessing:
- **Scaling**: Features were scaled using `RobustScaler` to mitigate the effect of outliers.
- **Data Split**: The dataset was split into training and testing sets (80% for training, 20% for testing).
- **Stratified K-Fold Cross-Validation** was applied to ensure reliable evaluation.

---

## 📊 Results Summary

### Scenario: `Correct_ID`
- **Top-performing models**: `MLP`, `Gradient Boosting`
- MLP achieved the **highest accuracy** and **F1-score**, owing to its capacity to capture complex patterns.
- Gradient Boosting was the fastest in both training and prediction — making it suitable for real-time deployment.
- FNN showed comparable results but required longer training times.

### Scenario: `Wrong_ID`
- **Top-performing model**: `Gradient Boosting`
- Clear anomaly patterns in this scenario made detection easier.
- GB provided the best balance of **accuracy** and **speed**.
- MLP, while accurate, had slower performance.
- Random Forest and Logistic Regression performed weaker, especially in real-time applications.

---

## Meta-Model (Ensemble Learning)

In the final step, a **Logistic Regression-based ensemble** was built, combining predictions from all base models. This ensemble approach:
- Improved **stability** and **robustness**.
- Enhanced **generalization** across different attack types, leading to better overall performance.

---

## 🗂️ Project Structure

This project consists of the following files:

1. **`DDoS_Detection_Analysis.ipynb`**: The main Colab notebook containing all the code for training, evaluation, and analysis.
2. **`CORRECT_ID.txt`**: Preprocessed dataset for training/testing with valid EV identifiers but invalid keys.
3. **`WRONG_ID.txt`**: Preprocessed dataset for training/testing with invalid EV identifiers.
4. **`README.md`**: This document providing an overview of the project.
