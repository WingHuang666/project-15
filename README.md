# project-15

# Diabetes Risk Prediction and Patient Segmentation Project

## Project Overview

This project analyzes a diabetes risk prediction dataset containing 50,000 patient records and 41 variables. The dataset includes demographic characteristics, lifestyle behaviors, family and medical history, clinical measurements, diabetes risk scores, and diabetes risk categories.

The objective of the project is to examine diabetes risk from multiple analytical perspectives rather than relying on a single predictive model. The analysis combines multiclass classification, regression, binary screening models, comparative modeling, and unsupervised clustering.

Five research questions are investigated:

1. Can patient characteristics predict Low, Moderate, and High diabetes risk categories?
2. Can patient characteristics predict a continuous Diabetes Risk Score?
3. Can high-risk patients be identified without using major laboratory biomarkers?
4. How much predictive value is added when clinical variables are included?
5. Can patients be segmented into meaningful profiles, and how does diabetes risk vary across these profiles?

---

## Dataset

The dataset contains:

* **50,000 observations**
* **41 variables**

The variables cover several major categories:

* Demographics
* Body measurements
* Lifestyle behaviors
* Family history
* Existing health conditions
* Laboratory and clinical measurements
* Diabetes risk outcomes
* Health recommendations

Examples of important predictors include:

* Age
* BMI
* Waist Circumference
* Fasting Blood Sugar
* HbA1c
* Blood Pressure
* Cholesterol
* Physical Activity
* Exercise
* Diet Quality
* Smoking Status
* Stress Level
* Family History of Diabetes
* Hypertension
* Heart Disease

---

## Data Leakage Assessment

Potential data leakage was evaluated before predictive modeling.

`Diabetes_Risk_Score` was excluded when predicting `Diabetes_Risk` because the score ranges correspond almost perfectly to the target categories:

* Low: 13–34
* Moderate: 35–64
* High: 65–100

`Doctor_Consultation_Needed` and `AI_Health_Recommendation` were also excluded from risk-category prediction because they appear to be downstream variables generated after or as part of the risk assessment.

This prevents the models from obtaining artificially high predictive performance by using variables that directly encode the target.

---

# Research Question 1: Multiclass Diabetes Risk Prediction

## Research Question

**Can patient characteristics predict whether an individual belongs to the Low, Moderate, or High diabetes risk category?**

## Task

Multiclass Classification

## Models Compared

* Logistic Regression
* Random Forest
* Extra Trees

---

# Research Question 2: Diabetes Risk Score Prediction

## Research Question

**Can patient characteristics predict the continuous Diabetes Risk Score?**

## Task

Regression

## Models Compared

* Extra Trees Regressor
* Random Forest Regressor

R² was used as the primary model-selection metric.


---

# Research Question 3: High-Risk Non-Laboratory Screening

## Research Question

**Can high-risk individuals be identified using demographic, lifestyle, body-measurement, family-history, and medical-history information without relying on major laboratory biomarkers?**

## Task

Binary Classification

The target was defined as:

* 1 = High Risk
* 0 = Non-High Risk

Major laboratory biomarkers such as Fasting Blood Sugar and HbA1c were excluded.

## Models Compared

* Logistic Regression
* Random Forest
* Extra Trees

Because the purpose of this analysis is **screening**, Recall was selected as the primary evaluation metric. High recall reduces the number of truly high-risk individuals who are missed.


---

# Research Question 4: Added Value of Clinical Variables

## Research Question

**How much does high-risk screening improve when clinical variables are added to lifestyle and non-laboratory patient information?**

## Task

Comparative Binary Classification

Two feature sets were compared:

1. Lifestyle / Non-Laboratory Only
2. Lifestyle + Clinical Variables

For consistency with the screening objective, models for both feature sets were selected based on **Recall**.


---

# Research Question 5: Patient Segmentation

## Research Question

**Can patients be segmented into meaningful profiles based on their characteristics, and do these profiles exhibit different levels of diabetes risk?**

## Task

Unsupervised Clustering

## Method

K-Means clustering was applied using demographic, anthropometric, lifestyle, family-history, and clinical characteristics.

Importantly, the following outcome variables were **not used to create the clusters**:

* Diabetes Risk
* Diabetes Risk Score
* Doctor Consultation Needed
* AI Health Recommendation

Diabetes risk was examined only after clustering to determine whether the resulting patient profiles were associated with different risk levels.

Solutions from k = 2 to k = 6 were evaluated using the Silhouette Score. The scores were generally low, indicating substantial overlap among patients rather than sharply separated natural populations.

A three-cluster solution was retained for descriptive analysis because it provided more granular and interpretable patient profiles.


---

# Methodological Considerations

Several limitations should be considered when interpreting the results.

The dataset is highly imbalanced, particularly for the Low diabetes-risk category. Therefore, accuracy alone may provide a misleading picture of model quality.

Feature importance represents predictive contribution rather than causal influence. A highly important predictor should not automatically be interpreted as causing diabetes risk.

The relationship between clinical biomarkers and the construction of the Diabetes Risk Score should also be considered. If the target score was originally calculated using variables such as Fasting Blood Sugar or HbA1c, predictive performance may partly reflect the underlying score-generation process.

Finally, clustering produced low Silhouette Scores. The identified clusters should therefore be interpreted as descriptive profiles and not as evidence of clearly distinct biological or clinical patient subtypes.

---

# Technologies and Libraries

The project was implemented in Python using:

* pandas
* NumPy
* Matplotlib
* scikit-learn

Major scikit-learn components included:

* Pipeline
* ColumnTransformer
* SimpleImputer
* StandardScaler
* OneHotEncoder
* LogisticRegression
* RandomForestClassifier
* ExtraTreesClassifier
* RandomForestRegressor
* ExtraTreesRegressor
* KMeans
* Classification and regression evaluation metrics

---
