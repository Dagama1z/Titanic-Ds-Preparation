# Titanic Dataset Analysis & Classification Report

## Executive Summary

This report presents a comprehensive analysis of the Titanic dataset containing 1,309 passenger records. The objective is to build a predictive model to classify passenger survival outcomes. After data preprocessing, exploratory analysis, and model development using Logistic Regression, the model achieved **85.75% accuracy** on the test set.

---

## 1. Data Acquisition

### Dataset Overview
- **Total Records**: 1,309 passengers
- **Total Features**: 12 columns
- **Source**: TITANIC_DATASET_1309.xlsx

### Features
| Feature | Description |
|---------|-------------|
| PassengerId | Unique identifier |
| Survived | Target variable (0=Did not survive, 1=Survived) |
| Pclass | Passenger class (1, 2, or 3) |
| Name | Passenger name |
| Sex | Gender (male/female) |
| Age | Age in years |
| SibSp | Number of siblings/spouses aboard |
| Parch | Number of parents/children aboard |
| Ticket | Ticket number |
| Fare | Ticket fare paid |
| Cabin | Cabin number |
| Embarked | Port of embarkation (S=Southampton, C=Cherbourg, Q=Queenstown) |

---

## 2. Data Preprocessing

### Missing Values
| Feature | Count | Percentage |
|---------|-------|-----------|
| Age | 263 | 20.09% |
| Fare | 1 | 0.08% |
| Cabin | 1,014 | 77.46% |
| Embarked | 2 | 0.15% |

### Preprocessing Actions
1. **Duplicate Rows**: 0 duplicates found - no action needed
2. **Missing Value Imputation**:
   - **Numeric features** (Age, Fare): Filled with median values
   - **Categorical features** (Cabin, Embarked): Filled with mode (most frequent value)
3. **Final Dataset Shape**: 1,309 rows × 12 columns (No data lost)

### Imputation Summary
- ✓ Age - filled with median (28.0)
- ✓ Fare - filled with median (14.45)
- ✓ Cabin - filled with mode
- ✓ Embarked - filled with mode

---

## 3. Exploratory Data Analysis (EDA)

### 3.1 Numerical Variables - Descriptive Statistics

| Variable | Count | Mean | Std | Min | 25% | Median | 75% | Max |
|----------|-------|------|-----|-----|-----|--------|-----|-----|
| Age | 1,309 | 29.5 | 12.9 | 0.17 | 22 | 28 | 35 | 80 |
| Fare | 1,309 | 33.3 | 51.7 | 0.00 | 7.90 | 14.45 | 31.28 | 512.33 |
| Pclass | 1,309 | 2.29 | 0.84 | 1 | 2 | 3 | 3 | 3 |
| SibSp | 1,309 | 0.50 | 1.04 | 0 | 0 | 0 | 1 | 8 |
| Parch | 1,309 | 0.39 | 0.87 | 0 | 0 | 0 | 0 | 9 |

### 3.2 Categorical Variables - Frequency Distributions

**Passenger Class Distribution**
| Class | Count | Percentage |
|-------|-------|-----------|
| 3rd Class | 709 | 54.16% |
| 1st Class | 323 | 24.68% |
| 2nd Class | 277 | 21.16% |

**Gender Distribution**
| Gender | Count | Percentage |
|--------|-------|-----------|
| Male | 843 | 64.4% |
| Female | 466 | 35.6% |

**Port of Embarkation**
| Port | Count | Percentage |
|------|-------|-----------|
| S (Southampton) | 916 | 69.98% |
| C (Cherbourg) | 270 | 20.63% |
| Q (Queenstown) | 123 | 9.40% |

### 3.3 Visualizations

1. **Passenger Ages Distribution**: Most passengers clustered between 20-40 years old
2. **Passenger Class Distribution**: Third class passengers dominated (54%)
3. **Age by Passenger Class**: Younger passengers in lower classes; older passengers in higher classes
4. **Age vs Fare Relationship**: Positive correlation observed
5. **Correlation Heatmap**: Shows relationships between numerical variables
6. **Pairplot**: Displays distributions and relationships for all numerical variables

---

## 4. Statistical Analysis

### 4.1 Correlation Analysis

**Correlation Matrix** (Numeric Variables)

| Variable | PassengerId | Survived | Pclass | Age | SibSp | Parch | Fare |
|----------|-------------|----------|--------|-----|-------|-------|------|
| PassengerId | 1.00 | -0.02 | -0.04 | 0.03 | -0.06 | 0.01 | 0.03 |
| Survived | -0.02 | 1.00 | **-0.26** | -0.04 | 0.00 | **0.11** | **0.23** |
| Pclass | -0.04 | -0.26 | 1.00 | -0.38 | 0.06 | 0.02 | **-0.56** |
| Age | 0.03 | -0.04 | -0.38 | 1.00 | -0.19 | -0.13 | 0.18 |
| SibSp | -0.06 | 0.00 | 0.06 | -0.19 | 1.00 | **0.37** | 0.16 |
| Parch | 0.01 | 0.11 | 0.02 | -0.13 | 0.37 | 1.00 | 0.22 |
| Fare | 0.03 | 0.23 | -0.56 | 0.18 | 0.16 | 0.22 | 1.00 |

**Key Correlations**
- **Strongest Positive**: Parch & SibSp = 0.374 (family relationships)
- **Strongest Negative**: Fare & Pclass = -0.559 (higher class = higher fare)

### 4.2 Key Statistical Findings

1. **Age Distribution**: 
   - Median = 28 years
   - Mean = 29.5 years
   - Range: 0.17 to 80 years

2. **Survival Overview**:
   - Survival Rate = 37.7%
   - 494 survivors out of 1,309 passengers

3. **Passenger Composition**:
   - Predominantly 3rd class passengers (54%)
   - Majority male (64.4%)
   - Most embarked from Southampton (70%)

---

## 5. Feature Selection & Data Split

### 5.1 Selected Predictor Variables

**7 Features Selected for Model**:
1. Pclass (Passenger Class)
2. Sex (Gender)
3. Age (Age in years)
4. SibSp (Siblings/Spouses)
5. Parch (Parents/Children)
6. Fare (Ticket fare)
7. Embarked (Port of embarkation)

**Target Variable**: Survived (0 or 1)

### 5.2 Train/Test Split

- **Train Set**: 916 samples (70%)
  - Non-survivors: 570 (62.2%)
  - Survivors: 346 (37.8%)

- **Test Set**: 393 samples (30%)
  - Non-survivors: 245 (62.3%)
  - Survivors: 148 (37.7%)

- **Stratification**: Used to maintain survival ratio in both sets
- **Random State**: 42 (for reproducibility)

---

## 6. Logistic Regression Model

### 6.1 Model Architecture

**Preprocessing Pipeline**:
1. **Numeric Features** (Age, SibSp, Parch, Fare):
   - Missing value imputation: Median
   - Scaling: StandardScaler

2. **Categorical Features** (Sex, Embarked):
   - Missing value imputation: Mode
   - Encoding: One-Hot Encoding

**Model**: Logistic Regression
- Solver: lbfgs
- Max Iterations: 1,000

### 6.2 Model Performance

#### Overall Accuracy
**85.75%** - Correctly classifies ~86 out of 100 passengers

#### Confusion Matrix

|  | Predicted: Did Not Survive | Predicted: Survived |
|--|-------|---------|
| **Actual: Did Not Survive** | 227 (TN) | 18 (FP) |
| **Actual: Survived** | 38 (FN) | 110 (TP) |

#### Performance Metrics

| Metric | Value | Interpretation |
|--------|-------|----------------|
| **Sensitivity (Recall)** | 74.32% | Model identifies 74% of actual survivors |
| **Specificity** | 92.65% | Model identifies 93% of actual non-survivors |
| **Precision** | 85.94% | Of predicted survivors, 86% actually survived |
| **F1-Score** | 0.7976 | Balanced measure of precision & recall |

#### Classification Report

|  | Precision | Recall | F1-Score | Support |
|--|-----------|--------|----------|---------|
| **Non-Survivor (0)** | 0.857 | 0.927 | 0.890 | 245 |
| **Survivor (1)** | 0.859 | 0.743 | 0.798 | 148 |
| **Weighted Avg** | 0.858 | 0.858 | 0.857 | 393 |

---

## 7. Model Insights & Interpretation

### 7.1 Model Strengths
- **High Specificity (92.65%)**: Excellent at identifying non-survivors
- **Good Precision (85.94%)**: Few false alarms when predicting survivors
- **Balanced Performance**: Weighted F1-score of 0.857 indicates overall reliability

### 7.2 Model Limitations
- **Moderate Sensitivity (74.32%)**: Misses ~26% of actual survivors (38 false negatives)
- **Small Dataset**: Limited to 1,309 samples for model training
- **Feature Dependencies**: Some strong correlations between features (multicollinearity)

### 7.3 Error Analysis

**False Positives (18)**: Non-survivors predicted as survivors
- Likely passengers with characteristics resembling survivors
- May have paid higher fares or been female passengers

**False Negatives (38)**: Survivors predicted as non-survivors
- Could be passengers in 3rd class who survived despite odds
- May have incomplete data or unusual profiles

---

## 8. Key Findings & Recommendations

### 8.1 Findings

1. **Class Effect**: Strong negative correlation with survival (r = -0.26)
   - 1st class passengers had higher survival rates
   - 3rd class passengers had lower survival rates

2. **Fare Matters**: Positive correlation with survival (r = 0.23)
   - Higher fares associated with increased survival probability

3. **Gender Impact**: Female passengers had higher survival rates
   - "Women and children first" evacuation policy evident

4. **Family Groups**: Moderate impact on survival
   - Small groups (1-2 family members) had better survival rates
   - Very large groups had lower survival rates

### 8.2 Recommendations

1. **Model Improvement**:
   - Consider tree-based models (Random Forest, Gradient Boosting) to capture non-linear patterns
   - Implement cross-validation for robust performance estimates
   - Try feature engineering (e.g., interaction terms, family size categories)

2. **Hyperparameter Tuning**:
   - Adjust regularization (L1/L2) to improve generalization
   - Test different solvers and max_iter values
   - Consider class weight adjustment for better sensitivity

3. **Data Enhancement**:
   - Impute cabin information for better feature representation
   - Create additional features from names (titles, surnames)
   - Consider temporal or sequential patterns if available

4. **Deployment Considerations**:
   - Monitor model performance on new passenger data
   - Set decision thresholds based on business requirements
   - Combine predictions with other analytical methods

---

## 9. Conclusion

The Logistic Regression model successfully predicts Titanic passenger survival with **85.75% accuracy**. The model demonstrates strong ability to identify non-survivors (92.65% specificity) but has moderate ability to identify survivors (74.32% sensitivity). 

Key predictors of survival include:
- **Passenger Class** (most important)
- **Fare** (ticket price)
- **Gender** (female bias)
- **Family composition**

While the model shows good performance, opportunities exist to improve sensitivity through ensemble methods or hyperparameter optimization. This analysis provides valuable insights into factors influencing survival outcomes on the Titanic.

---

## Appendix: Technical Details

**Python Libraries Used**:
- pandas: Data manipulation
- scikit-learn: Machine learning & preprocessing
- matplotlib: Visualization
- seaborn: Statistical visualization
- numpy: Numerical operations

**Model Parameters**:
- Solver: lbfgs
- Max Iterations: 1,000
- Random State: 42
- Test Size: 0.30
- Stratification: Yes

**File**: TITANIC_DATASET_1309.xlsx
**Analysis Date**: 2026-07-07
**Report Generated**: Titanic Project Analysis
