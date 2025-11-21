# BioInformatics_Draft_Code
BioInformatics_Draft_Code


# Machine Learning Prediction of Pathogenic and Benign Genetic Variants

This repository contains a machine learning preprocessing and exploratory analysis pipeline for the **ClinVar conflicting variant dataset**.  
The workflow includes data cleaning, feature engineering, feature selection, and visualization — preparing the dataset for downstream machine learning classification tasks.

## Dataset

- **File used:** `clinvar_conflicting.csv`
- Contains genetic variants with clinical interpretation labels and metadata.

## Prediction Target

The goal is to classify variants into **five clinical significance categories:**

0 - Benign
1 - Likely_Benign
2 - Pathogenic
3 - Likely_Pathogenic
4 - Uncertain

These labels are derived from the raw column **`CLNSIGINCL`** 

## Workflow

Load dataset  
Print summary statistics  
Create target class (`CLNSIG_5class`)  
Drop duplicate rows  
Detect numeric vs categorical features  
Handle missing values (mean imputation)  
Handle outliers using **IQR clipping**  
Label encoding of categorical features  
Extract numerical target label (`CLNSIG_5class_encoded`)  
Feature selection using **Mutual Information (MI)**  
Visualization of relationships among selected features  

## Data Preprocessing Steps

| Step | Method Used |
|------|------------|
| Missing values | `SimpleImputer(strategy="mean")` |
| Outliers | IQR method → clipped to lower/upper bounds |
| Encoding | `LabelEncoder()` for categorical & target |
| Numeric conversion | Auto-detect coercible string features → convert to numeric |

---

## Exploratory Data Analysis

For the **top MI-ranked feature**, the script generates:

- Bar Chart (mean feature value per class)  
- Scatter/Strip Plot (distribution across classes)  
- Line Plot (trend of mean values across encoded target)

A correlation heatmap is also produced using the selected top 6 features.

---

## Feature Selection

Feature importance is determined using correlation heatmap. Top 6 features are chosen


