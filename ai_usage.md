# AI Usage Documentation

This project investigates whether machine learning models can accurately classify genetic variants in the ClinVar dataset as pathogenic or benign. AI tools (ChatGPT) were used to support writing, organization, and workflow planning throughout the project.

---

## 1. Purpose of AI Assistance
AI was used for:
- Drafting and improving written documentation (proposal text, slide summaries, explanation wording).
- Suggesting preprocessing steps (handling missing values, encoding methods, SMOTE, feature selection ideas) in future if needed
- Providing general structure and guidance for Exploratory Data Analysis and model development in future if needed
- Refining formatting for report sections, bullet points, and final deliverables.

AI was *not* used to generate, alter, or label any dataset values.

---

## 2. Scope of AI Contribution
AI provided:
- Suggestions for model selection (Logistic Regression, Random Forest, XGBoost).
- Guidance on applying evaluation metrics (accuracy, precision, recall, F1-score, ROC-AUC) in future if needed
- Template support for documentation files (README, methodology summary, reproducibility notes).

All code logic, preprocessing steps, and model training were performed manually, executed in Google Colab, and validated against real output.

---

## 3. Verification of AI-Generated Outputs
To ensure accuracy and reliability:
- All suggestions were tested and executed to confirm functionality.
- Model performance was validated using confusion matrix metrics.
- Any AI-generated text was manually reviewed, edited, and aligned with the dataset output and scientific reasoning.

No AI-generated result was accepted without manual verification.

---

## 4. Ethical and Privacy Considerations
- The dataset used (ClinVar) is *public, non-identifiable genetic data*, ensuring no privacy or patient-specific risks.
- AI was not used for clinical interpretation—only for technical and documentation assistance.
- All workflows remain transparent and reproducible through included notebooks and scripts.

---

## 5. Reproducibility Statement
- The repository includes all required notebooks, scripts, and documentation files.
- The project maintains reproducible steps including preprocessing, model training, and evaluation.
- This ai_usage.md file provides transparency of where AI assistance was applied.
