# CSC172 Association Rule Mining Project Proposal
**Student:** Lavigne Kaye S. Sistona, 2022-5619
**Date:** December 12, 2025

## 1. Project Title
Data Mining and Exploratory Analysis of Dementia Patient Health Factors

## 2. Problem Statement
Dementia among elderly individuals (60 years and above) continues to rise in the Philippines, with cognitive decline influenced by physical health, lifestyle, and hereditary factors. Understanding hidden patterns within patient health data can help identify variable relationships that may be associated with cognitive deterioration. This project applies data mining and exploratory analysis techniques to examine a dementia patient dataset, uncovering trends, clusters, and correlations that may aid medical professionals in understanding dementia-related risk factors.

## 3. Objectives
- Clean and preprocess a real-world dementia patient dataset  
- Perform exploratory data analysis (EDA) and create meaningful visualizations  
- Identify trends and correlations among health features and cognitive scores  
- Apply clustering, association analysis, and dimensionality reduction to find hidden patterns  

## 4. Dataset Plan
- **Source:** Dementia Patient Health Dataset – Kaggle  
  https://www.kaggle.com/datasets/timothyadeyemi/dementia-patient-health-dataset  
- **Domain:** Elderly health indicators, lifestyle attributes, cognitive scores  
- **Content:** Variables include age, gender, smoking status, comorbidities, family history, physical health metrics, and cognitive test scores  
- **Acquisition:** Direct Kaggle download → saved to `data/dementia_patients.csv`

## 5. Technical Approach
### Preprocessing
- Handle missing values (median / mode imputation)  
- Encode categorical variables using Label Encoding or One-Hot Encoding  
- Detect and treat outliers using IQR and visualization techniques  
- Standardize numerical features for consistency  

### Exploratory Data Analysis (EDA)
- Distribution plots for age, BMI, cognitive scores, and other features  
- Correlation heatmap to determine strong factor relationships  
- Pairwise visualizations to compare cognitive scores vs. health/lifestyle factors  
- Feature importance ranking using Random Forest or Mutual Information  

### Data Mining Methods
- **Clustering:** K-means or Hierarchical clustering to group similar patient profiles  
- **Association analysis:** Identify co-occurring health and lifestyle factors  
- **Dimensionality reduction:** PCA for visualizing feature patterns in 2D/3D  

### Tools & Environment
- Python, pandas, numpy  
- scikit-learn for data mining techniques  
- seaborn & matplotlib for visualization  
- Jupyter Notebook 

## 6. Expected Challenges & Mitigations
- **Missing or inconsistent records**  
  - Use robust preprocessing and imputation strategies  
- **High variability in health and cognitive features**  
  - Apply scaling techniques to improve consistency  
- **Noisy or overlapping features**  
  - Use feature selection and PCA to reduce dimensionality  
- **Imbalanced category distributions**  
  - Use stratified sampling and targeted visualizations to handle imbalance  

