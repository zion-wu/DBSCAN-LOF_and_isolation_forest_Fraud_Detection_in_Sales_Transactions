# Sales Fraud Detection

This project compares the effectiveness of two anomaly detection methods—DBSCAN/LOF and Isolation Forest—for identifying fraudulent sales transactions in a large dataset of sales reports. The findings aim to provide actionable insights for businesses seeking to reduce fraud and safeguard their commission-based sales structures.

## 📊 Project Overview

Fraudulent sales reporting by representatives can lead to significant financial losses. Traditional rule-based detection systems often fall short, as fraudsters adapt to evade detection. This project evaluates two unsupervised anomaly detection techniques to recommend the most suitable method for detecting anomalies in sales transactions.

### Objectives

- Compare DBSCAN/LOF and Isolation Forest for detecting anomalies.
- Evaluate models on real-world labeled test data.
- Recommend the best-performing method for deployment.

## 🔍 Dataset

The dataset is a systematic sample from a sales transaction case study by Torgo (2017, 2021). It consists of:

- **Training set**: 133,731 unlabeled sales transactions.
- **Test set**: 15,732 labeled transactions (1,270 fraud, 14,462 normal).

Each transaction includes:

- `Prod`: Product ID.
- `Quant`: Quantity sold.
- `Val`: Total sale value.
- `Insp`: Inspection result (`ok`, `fraud`, or `unkn` in training set).

## 🧰 Methods

### Data Preprocessing

- Dropped rows with missing `Quant` or `Val` (<3%).
- Applied log transformation to `Quant` and `Val` to address skewness.
- Analyzed fraud rates by product to create additional features.

### Model Implementation

1. **DBSCAN + LOF**:
   - DBSCAN: `eps=0.16`, `min_samples=9`.
   - LOF: `contamination=0.01`.
   - Final classification: Fraud if detected by both methods or flagged as high-risk product.

2. **Isolation Forest**:
   - `n_estimators=400`, `contamination=0.07`, `max_samples=0.9`.
   - Final classification: Fraud if detected by the model or flagged as high-risk product.

### Evaluation Metrics

Given the imbalanced dataset, models were evaluated using:
- **F1-Score (Macro & Weighted)**.
- **Precision-Recall AUC**.
- **Balanced Accuracy**.

## 📈 Results

| Model           | Macro F1 | Weighted F1 | PR AUC  | Balanced Accuracy |
|----------------|-----------|-------------|---------|------------------|
| DBSCAN + LOF   | 0.7113    | 0.9097      | 0.5084  | 0.7542           |
| Isolation Forest | 0.7555    | 0.9214      | 0.5985  | 0.8229           |

**Key Findings**:
- Isolation Forest outperformed DBSCAN/LOF across all metrics.
- DBSCAN/LOF may capture local density anomalies, useful in specific cases.
- Isolation Forest is recommended for deployment due to higher F1, balanced accuracy, and precision-recall balance.
