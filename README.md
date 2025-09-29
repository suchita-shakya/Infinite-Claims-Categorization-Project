# Automated Claims Categorization: Project Submission

## Executive Summary
This project addresses the critical need for efficient and accurate health insurance claims processing by developing an automated categorization system. By leveraging machine learning and robust data engineering techniques, this system aims to classify millions of daily claims (inpatient, outpatient, pharmacy) significantly faster and more reliably than manual methods.  

The solution is built upon structured claim data, focusing on classification algorithms and an end-to-end data pipeline, delivering high accuracy and providing performance insights through detailed reporting and visualizations.

---

## 1. Introduction and Problem Statement
Health insurance providers are inundated with millions of claims daily from hospitals, clinics, and pharmacies. These claims contain structured data such as:
- Diagnosis codes (ICD-9),
- Procedure codes (ICD-9, HCPCS),
- Provider types,
- Service dates.  

Effective categorization of these claims into **inpatient, outpatient, or pharmacy** is fundamental for:
- Efficient routing,
- Precise adjudication,
- Insightful analytics.  

Manual categorization is slow, error-prone, and inefficient. This project proposes an **automated solution** to overcome these challenges.

---

## 2. Project Objectives
- Build a **machine learning model** to classify claims into inpatient, outpatient, or pharmacy categories with high accuracy.  
- Design and implement a **robust data pipeline** for ingestion, preprocessing, and feature engineering.  
- Ensure seamless integration of processed data into the classification model.  
- Provide **performance metrics and visualizations** to demonstrate model effectiveness.  

---

## 3. Dataset Description
Dataset: Synthetic Medicare claims data, inspired by **CMS Medicare Claims Synthetic Public Use Files (SynPUFs)**.  

Data sources:
- **Inpatient Claims** – hospital stays and inpatient procedures.  
- **Outpatient Claims** – services without overnight stay.  
- **Pharmacy Claims** – prescription drug events.  

These datasets were merged into a unified corpus for comprehensive model training.

---

## 4. Methodology

### 4.1 Data Preprocessing & Feature Engineering
Steps included:
1. **Data Loading** – inpatient, outpatient, and pharmacy datasets loaded with `pandas`.  
2. **Integration** – added a `claim_type` column as the target variable; concatenated into a single DataFrame.  
3. **Date Handling** – converted `CLM_FROM_DT` and `CLM_THRU_DT` into datetime objects.  
4. **Feature Creation**:
   - Claim Duration (`claim_duration_days` = difference between `CLM_THRU_DT` and `CLM_FROM_DT`).  
   - Categorical Encoding for ICD-9, HCPCS codes (`astype('category').cat.codes`).  
   - Numerical encoding for `claim_type`.  
   - Selection of key financial and pharmacy-specific features.  
5. **Data Splitting** – 80/20 split using `train_test_split`.  

### 4.2 Model Development
- Chosen model: **RandomForestClassifier** (robust, interpretable feature importance).  
- Training performed on training set.  
- Predictions generated for unseen test set.  

---

## 5. Results & Performance Evaluation

### 5.1 Classification Report
| Class      | Precision | Recall | F1-Score | Support   |
|------------|-----------|--------|----------|-----------|
| Inpatient  | 1.00      | 1.00   | 1.00     | 13,319    |
| Outpatient | 1.00      | 1.00   | 1.00     | 158,521   |
| Pharmacy   | 1.00      | 1.00   | 1.00     | 1,110,157 |

**Accuracy:** 1.00 (on 1,281,997 samples)

---

### 5.2 Confusion Matrix
|               | Predicted: Inpatient | Predicted: Outpatient | Predicted: Pharmacy |
|---------------|----------------------|-----------------------|---------------------|
| **Actual: Inpatient**  | 13,319 | 0 | 0 |
| **Actual: Outpatient** | 0 | 158,521 | 0 |
| **Actual: Pharmacy**   | 0 | 0 | 1,110,157 |

---

### 5.3 Interpretation
- High **precision, recall, and F1-score** across all categories.  
- Diagonal confusion matrix indicates strong predictive performance.  
- Confirms the model’s suitability for automating claim categorization.  

---

## 6. Conclusion
The project successfully:
- Developed an **automated claims categorization pipeline**.  
- Processed and engineered features from synthetic claims data.  
- Trained a **RandomForestClassifier** achieving near-perfect classification accuracy.  

This system addresses inefficiencies of manual categorization and provides a **scalable, reliable solution** for health insurers.

---

## 7. Future Work
- **Hyperparameter Tuning** – optimize RandomForest parameters for better performance.  
- **Advanced Feature Engineering** – interaction terms, embeddings for categorical codes.  
- **Alternative Models** – Gradient Boosting, Neural Networks.  
- **Real-time Processing** – enable real-time ingestion and classification.
- **Deployment** – explore deployment on **Azure ML** for production readiness.  

---
