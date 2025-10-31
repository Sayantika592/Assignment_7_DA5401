Name: Sayantika Chakraborty     Roll No.: ME22B190

# DA5401 – Assignment 7  
**Topic:** Model Evaluation using ROC and PRC Analysis on the Landsat Satellite Dataset  

## Overview
This assignment evaluates multiple machine learning models on the **Landsat Satellite dataset**, focusing on comparing their classification performance using **Accuracy**, **Weighted F1-Score**, **ROC-AUC**, and **Precision–Recall (PRC)** metrics.  
The task aims to identify the most suitable model for multi-class land-cover classification.

## Dataset Description
- **Source:** UCI Landsat Satellite Dataset (ID: 146)  
- **Features:** 36 spectral attributes from 3×3 pixel neighborhoods  
- **Classes:** 6 possible land-cover types, but **class 6 (mixture class)** is **absent** in the dataset.  
  Hence, only classes **1, 2, 3, 4, 5, and 7** are used.  
- **Goal:** Predict the central pixel’s land-cover type.

## Models Evaluated
1. **K-Nearest Neighbors (KNN)**  
2. **Support Vector Classifier (SVC)**  
3. **Logistic Regression**  
4. **Naive Bayes**  
5. **Decision Tree**  
6. **Random Forest**  
7. **XGBoost**  
8. **Dummy (Prior) Baseline**  
9. **BadModel_Shuffled_RF** (intentionally poor model, AUC < 0.5)

## Evaluation Metrics
Each model is compared using:
- **Accuracy & Weighted F1-Score** → Threshold-based performance  
- **ROC-AUC (Macro Average)** → Overall class separability  
- **Average Precision (AP)** → Precision–recall behavior across thresholds  

## Key Observations
| Model | Weighted F1 | ROC-AUC | AP | Average Rank |
|:------|:-------------:|:--------:|:----:|:--------------:|
| **XGBoost** | 0.9156 | 0.9901 | 0.9509 | **1.00** |
| Random Forest | 0.9138 | 0.9886 | 0.9432 | 2.00 |
| KNN | 0.9100 | 0.9806 | 0.9225 | 3.33 |
| SVC | 0.8960 | 0.9821 | 0.9095 | 3.67 |
| Logistic Regression | 0.8513 | 0.9747 | 0.8739 | 5.00 |
| Naive Bayes | 0.8001 | 0.9541 | 0.8021 | 6.33 |
| Decision Tree | 0.8366 | 0.8890 | 0.7080 | 6.67 |
| Dummy (Prior) | 0.0917 | 0.5000 | 0.1667 | 8.33 |
| BadModel_Shuffled_RF | 0.1743 | 0.4702 | 0.1557 | 8.67 |

## Analysis Summary

### **Precision–Recall (PRC) Insights**
- **Good models** (e.g., XGBoost, RandomForest) maintain high precision until recall ≈ 0.9,  
  showing balanced positive predictions.  
- **Poor models** (e.g., Dummy, Inverted) show **sharp drops in precision** early as recall rises,  
  indicating weak discriminative capability.

### **Metric Trade-offs**
- **ROC-AUC** shows global class separability but not confidence.  
- **PRC-AP** better captures performance on less frequent classes.  
- **F1-Score** gives threshold-based balance, not overall trend.

## Final Recommendation

### **Best Model: XGBoost**

**Why:**
- Highest **ROC-AUC (0.990)** → excellent class separability.  
- Highest **Average Precision (0.951)** → strong precision–recall trade-off.  
- Highest **Weighted F1 (0.916)** → balanced performance at optimal threshold.  

**Conclusion:**  
XGBoost delivers the most consistent and reliable performance across all metrics,  
making it the **best-suited model for Landsat multi-class classification**.

## Files Included
- `DA5401_Assignment_7.ipynb` → Full implementation and plots  
- `README.md` → Summary and explanation  
- Dataset files: `sat.trn`, `sat.tst`, `sat.doc`, `index`

