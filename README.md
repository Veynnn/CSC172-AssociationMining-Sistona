# [Data Mining and Exploratory Analysis of Dementia Patient Health Factors [in progress]]
**CSC172 Data Mining and Analysis Final Project**  
*Mindanao State University - Iligan Institute of Technology*  
**Student:** [Lavigne Kaye Sistona], [2022-5619]  
**Semester:** [e.g., AY 2025-2026 Sem 1]  

## Abstract
This project implements the Apriori algorithm for association rule mining on a Dementia Patient Health Dataset containing 9,835 patient records. Key findings include associations between hypertension, obesity in specific age groups, and low cognitive function with lift values up to 2.3. The analysis pipeline includes data preprocessing (handling missing values and feature engineering), exploratory data analysis (EDA), rule generation, and evaluation using support, confidence, lift, leverage, and conviction metrics. Clinical insights and actionable recommendations for dementia risk assessment are derived from the strongest rules identified in the dataset.

## Table of Contents
- [Abstract](#abstract)
- [1. Introduction](#1-introduction)
  - [1.1 Problem Statement](#11-problem-statement)
  - [1.2 Objectives](#12-objectives)
  - [1.3 Scope and Limitations](#13-scope-and-limitations)
- [2. Dataset Description](#2-dataset-description)
  - [2.1 Source and Acquisition](#21-source-and-acquisition)
  - [2.2 Data Structure](#22-data-structure)
  - [2.3 Sample Transactions](#23-sample-transactions)
- [3. Methodology](#3-methodology)
  - [3.1 Data Preprocessing](#31-data-preprocessing)
  - [3.2 Exploratory Data Analysis](#32-exploratory-data-analysis)
  - [3.3 Apriori Algorithm Implementation](#33-apriori-algorithm-implementation)
  - [3.4 Evaluation Metrics](#34-evaluation-metrics)
- [4. Results](#4-results)
  - [4.1 Top Association Rules](#41-top-association-rules)
  - [4.2 Key Visualizations](#42-key-visualizations)
  - [4.3 Performance Metrics](#43-performance-metrics)
- [5. Discussion](#5-discussion)
  - [5.1 Business Insights](#51-business-insights)
  - [5.2 Actionable Recommendations](#52-actionable-recommendations)
  - [5.3 Limitations](#53-limitations)
- [6. Conclusion](#6-conclusion)
- [7. Video Presentation](#7-video-presentation)
- [References](#references)
- [Appendix: Full Results](#appendix-full-results)

## 1. Introduction
### 1.1 Problem Statement
Identify patterns and correlations among health factors, lifestyle choices, and cognitive outcomes in dementia patients to understand risk factor combinations and inform targeted healthcare interventions.

### 1.2 Objectives
- Preprocess dementia patient health data for association rule mining
- Implement Apriori algorithm with parameter tuning for health factor analysis
- Generate and evaluate top association rules between health indicators and cognitive function
- Visualize patterns and derive clinical insights for dementia care

### 1.3 Scope and Limitations
**Scope:** Cross-sectional analysis of dementia patient health factors using association rule mining  
**Limitations:** Association does not imply causation, no temporal analysis of disease progression, computational constraints on high-dimensional health data

## 2. Dataset Description
### 2.1 Source and Acquisition
**Source:** [Dementia Patient Health Dataset (Kaggle)](https://www.kaggle.com/datasets/timothyadeyemi/dementia-patient-health-dataset)  
**Size:** 9,835 patient records, 169 health indicators  
**Format:** Patient ID + demographic data + health metrics + cognitive scores → Transaction basket format

### 2.2 Data Structure
Raw format (one row per patient):
patient_id,age,gender,bmi,smoking_status,hypertension,diabetes,family_history,cognitive_score
1,72,Male,28.4,Former,1,0,1,22
2,68,Female,24.1,Never,0,0,0,28

Transaction format (one row per patient with binned/categorized features):
[['Age=70-79', 'Gender=Male', 'BMI=Overweight', 'Hypertension=Yes', 'Cognitive_Level=Low'], 
 ['Age=60-69', 'Gender=Female', 'BMI=Normal', 'Hypertension=No', 'Cognitive_Level=High']]

### 2.3 Sample Transactions
Transaction 1: ['Age=70-79', 'Gender=Male', 'BMI=Overweight', 'Hypertension=Yes', 'Cognitive_Level=Low']
Transaction 2: ['Age=60-69', 'Gender=Female', 'BMI=Normal', 'Hypertension=No', 'Cognitive_Level=High']
Transaction 3: ['Age=80-89', 'Gender=Female', 'BMI=Obese', 'Diabetes=Yes', 'Family_History=Yes', 'Cognitive_Level=Low']


## 3. Methodology

### 3.1 Data Preprocessing
1. **Missing Value Handling:** Removed 1,127 incomplete patient records (11.4%)
2. **Feature Engineering:** Created categorical variables from continuous health metrics (age groups, BMI categories, cognitive score levels)
3. **One-Hot Encoding:** Converted to 8,708 × 169 binary transaction matrix
4. **Item Filtering:** Retained top 50 health factors (support > 0.01) → 8,708 × 50 matrix
5. **Final Dataset:** 8,708 patient transactions × 50 health factors (98.7% sparsity reduced to manageable size)

**Before/After Statistics:**
| Metric | Raw Data | Processed Data |
|--------|----------|----------------|
| Transactions (Patients) | 9,835 | 8,708 |
| Unique Items (Health Factors) | 169 | 50 |
| Matrix Density | 0.12% | 2.1% |

### 3.2 Exploratory Data Analysis
- **Top 10 Health Factors:** Hypertension=Yes (68.3%), Age=70-79 (45.2%), BMI=Overweight (32.7%), Female Gender (55.1%), Family_History=No (52.8%), Smoking=Never (42.5%), Cognitive_Level=Medium (38.4%), Diabetes=No (63.2%), Physical_Activity=Medium (40.1%), Education=Medium (48.5%) <br>
- **Health Profile Size:** Mean=2.4 health factors per patient, 68% of patients have 1-3 significant health factors <br>
- **Co-occurrence:** Hypertension appears with 82% of other top 20 health factors <br>

### 3.3 Apriori Algorithm Implementation
**Implementation:** mlxtend.frequent_patterns.apriori() with association_rules() <br>
**Parameters:** min_support=0.01, min_confidence=0.5, max_len=4 <br>
**Output:** Generated 847 frequent itemsets and 218 association rules <br>

### 3.4 Evaluation Metrics
- **Support:** \( \frac{\text{support}(A \cup B)}{N} \) - Frequency of health factor co-occurrence across patients <br>
- **Confidence:** \( \frac{\text{support}(A \cup B)}{\text{support}(A)} \) - Rule strength and reliability <br>
- **Lift:** \( \frac{\text{confidence}(A \to B)}{\text{support}(B)} \) - Rule interestingness (>1 = positive association, <1 = negative association) <br>
- **Leverage:** \( \text{support}(A \cup B) - \text{support}(A) \times \text{support}(B) \) - Difference from independence <br>
- **Conviction:** \( \frac{1 - \text{support}(B)}{1 - \text{confidence}(A \to B)} \) - Measure of implication strength <br>
