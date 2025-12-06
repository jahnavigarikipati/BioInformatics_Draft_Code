# Machine Learning Prediction of Pathogenic and Benign Genetic Variants

A machine learning model to classify clinical significance of genetic variants using ClinVar data.

## Overview

This project builds a **5-class classifier** to predict the clinical significance of genetic variants:
- **Benign**
- **Likely Benign**
- **Uncertain**
- **Likely Pathogenic**
- **Pathogenic**

The model is  **Random Forest classifier** trained on the top-6 most informative features selected via Mutual Information scoring.

---

## Dataset

**File**: `clinvar_conflicting.csv` 
**Source**: `https://www.kaggle.com/code/schizo3/clinvarmutations` 
- Contains variant data from ClinVar database
- Raw target column: `CLNSIGINCL` (contains various clinical significance labels)
- Target is cleaned and converted to 5 standardized classes

---

## Project Stages

### 1. **Data Loading & Cleaning**
- Load ClinVar dataset
- Remove duplicates
- Handle missing values using mean imputation (numeric columns)
- Remove outliers using IQR (Interquartile Range) method
- Encode categorical features using LabelEncoder

### 2. **Target Variable Creation**
Raw labels are classified into 5 classes:
- "likely_benign" → **Likely_Benign**
- "likely_pathogenic" → **Likely_Pathogenic**
- "benign" (not "likely") → **Benign**
- "pathogenic" (not "likely") → **Pathogenic**
- "uncertain", "risk_factor", "other", NaN → **Uncertain**

### 3. **Feature Selection**
- Compute Mutual Information (MI) scores for all numeric features
- Select top-6 features with highest MI scores
- Features ranked by information gain w.r.t. clinical significance

### 4. **Class Balancing**
- Apply **SMOTE** (Synthetic Minority Over-sampling Technique) to balance classes
- Creates synthetic samples for underrepresented classes
- Reduces class imbalance in training data

### 5. **Model Training**
- **Algorithm**: Random Forest (300 trees)
- **Split**: 80% train, 20% test (stratified)
- **Class weights**: Balanced (automatically adjust for remaining class imbalance)
- **Random state**: 42 (reproducibility)

### 6. **Evaluation**
**Metrics:**
- Accuracy
- Classification Report (per-class precision, recall, F1-score)
- Confusion Matrix
- Multi-class ROC-AUC curves (per-class and macro-averaged)

### 7. **Exploratory Data Analysis (EDA)**
- **Correlation Heatmap**: Feature correlations with target
- **Bar Plot**: Mean feature values by class
- **Scatter Plot**: Feature distribution across classes
- **Line Graph**: Mean feature trend across class encodings
- **ROC Curves**: One curve per class showing model discrimination ability

---

## Key Features

### Top-6 Selected Features
The model uses the top-6 Mutual Information features:
```
[Feature1, Feature2, Feature3, Feature4, Feature5, Feature6]
```
(Feature names printed during execution)

### Model Characteristics
- **Input**: 6 numeric features (preprocessed)
- **Output**: 5-class prediction (one of the clinical significance classes)
- **Probability Output**: Yes (predict_proba available for confidence scores)

---

## Usage

### Prerequisites
```bash
pip install pandas numpy scikit-learn seaborn matplotlib imbalanced-learn
```

### Run the Pipeline
1. Place `clinvar_conflicting.csv` in the same directory
2. Open `Bioinformatics_Code (1).ipynb` in Jupyter Notebook
3. Run all cells sequentially

### Output
- **Trained model**: Saved in memory
- **Predictions**: Print class label and probabilities
- **Plots**: 
  - Correlation heatmap
  - Confusion matrix
  - Bar/Scatter/Line charts
  - Multi-class ROC curves

---

## Single Prediction Example

To predict clinical significance for a new variant:

```python
# Prepare input (6 top features, in correct order)
single_input = {
    "feature1": value1,
    "feature2": value2,
    # ... other 4 features
}

# Convert to DataFrame (same column order as training)
input_df = pd.DataFrame([single_input], columns=top6)

# Predict
pred_label = le_target.inverse_transform(model.predict(input_df))[0]
pred_proba = model.predict_proba(input_df)[0]

print(f"Predicted: {pred_label}")
print(f"Probabilities: {dict(zip(le_target.classes_, pred_proba))}")
```

---

## Performance Metrics

**Evaluation on test set:**
- **Accuracy**: [Output from notebook]
- **Balanced Accuracy**: Accounts for class imbalance
- **Per-class metrics**: See classification report in notebook

**ROC-AUC scores** for each class show model's ability to discriminate between:
- Each class vs. all others (One-vs-Rest)
- Higher AUC = better discrimination

---

## Important Notes

1. **SMOTE Applied**: Training data is synthetic-balanced; test data is original distribution
2. **Stratified Split**: Test set maintains original class distribution
3. **Feature Scaling**: Not applied (Random Forest is tree-based, scale-invariant)
4. **Random State**: Set to 42 for reproducible results
5. **Class Imbalance**: Handled via SMOTE + class_weight="balanced"



## Future Work
- Add an LLM or AI Agent to explain the reason of prediction

---
## License
For research and educational purposes only. Always refer to ClinVar's terms of use for data usage.
