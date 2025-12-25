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

