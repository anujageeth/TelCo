# Data Preprocessing and Correlation Matrix

The correlation matrix is typically calculated **after preprocessing** but **before feature selection or model training**. Preprocessing involves steps such as handling missing values, encoding categorical variables, scaling, and feature engineering. Once these steps are complete, calculate the correlation matrix to understand relationships between numerical features.

## Typical Order of Operations

1. **Data Cleaning (Preprocessing):**
   - Handle missing values (e.g., filling or dropping).
   - Convert categorical variables to numerical format (e.g., one-hot or label encoding).
   - Handle outliers (e.g., removing or transforming extreme values).
   - Normalize or scale numerical features (e.g., MinMaxScaler or StandardScaler).

2. **Feature Engineering:**
   - Create new features from existing ones (e.g., interaction or polynomial features).
   - Transform features (e.g., taking log of skewed features).

3. **Correlation Matrix (After Preprocessing):**
   - After cleaning and transforming the data, calculate the correlation matrix for numerical features.
   - Identify relationships and redundancies to help reduce multicollinearity.

4. **Feature Selection:**
   - Use the correlation matrix and domain knowledge to select relevant features.
   - Aim to reduce redundancy and avoid multicollinearity.

5. **Model Training:**
   - After selecting features, train the model.

## Why Calculate Correlation After Preprocessing?

- **Handling Missing Data**: Prevents distortion in the correlation matrix.
- **Categorical Variables**: Correlation applies to numerical features; encode categorical variables first.
- **Scaling**: Normalizes feature relationships for models that require scaling.
- **Outliers**: Eliminating outliers prevents misleading correlation values.

---

# Choosing Between Min-Max Normalization and Standard Scaling

## 1. Min-Max Normalization

- **Best for**: Data with known min/max and when values need to be between [0, 1].
- **Effect on Outliers**: Sensitive to outliers.
- **Use Cases**: Neural networks, deep learning.

## 2. Standard Scaling (Z-Score Normalization)

- **Best for**: Normally distributed data or centering data at 0 with unit variance.
- **Effect on Outliers**: More robust than Min-Max but still can be affected.
- **Use Cases**: Linear models, PCA, SVM.

## Which One Is Best?

- Use **Standard Scaling** if the data has outliers.
- Use **Min-Max Scaling** if the data needs to be in a specific range (e.g., for neural nets).
- **Experiment** with both and evaluate performance.

---

# K-Fold Cross-Validation

- Divide the dataset into *k* folds.
- Train the model *k* times, using different folds for testing.
- Average the results to estimate performance.

**Example**: 5-fold or 10-fold cross-validation.

### Benefits

- Reliable performance estimation.
- Reduces overfitting and underfitting risk.
- Makes efficient use of data (especially small datasets).

---

# Model Evaluation

## 1. Linear Regression

**Metrics:**
- Train MSE: 0.1384
- Test MSE: 0.1452
- Train R²: 0.2959
- Test R²: -748445.059

**Interpretation:**
- **MSE**: Lower is better; test MSE is slightly higher — minor generalization issues.
- **R²**:
  - Train: ~29.6% variance explained.
  - Test: Very negative — model overfits and performs poorly on new data.

**Conclusion:** Linear Regression generalizes poorly. Consider regularization (Ridge/Lasso) or improved preprocessing.

---

## 2. Logistic Regression

**Metrics:**
- Accuracy: 79%
- Precision/Recall/F1:
  - **Class 0 (Non-Churn)**: High (~0.86 F1)
  - **Class 1 (Churn)**: Lower (~0.57 F1)

**Interpretation:**
- Accuracy is decent at 79%.
- Class 1 is less accurately predicted due to class imbalance.
- Macro average F1 ~0.70 — balanced overall performance.

**Conclusion:** Logistic Regression performs well but could improve for the minority class.

---

# Key Comparison Metrics

| Metric             | Linear Regression | Logistic Regression |
|--------------------|-------------------|---------------------|
| Train MSE          | 0.1384            | Not applicable      |
| Test MSE           | 0.1452            | Not applicable      |
| Train R²           | 0.296             | Not applicable      |
| Test R²            | -748445.059       | Not applicable      |
| Accuracy           | Not applicable    | 79%                 |
| Class 0 F1-Score   | Not applicable    | 86%                 |
| Class 1 F1-Score   | Not applicable    | 57%                 |
| Generalization     | Poor              | Good                |

---

# Conclusion

- **Linear Regression**: Poor generalization — not suitable due to overfitting or incorrect assumptions.
- **Logistic Regression**: Better performance on classification tasks like churn prediction.

## Recommendations

For binary classification:
- Use **Logistic Regression**.

To improve Linear Regression:
- Apply **Ridge or Lasso**.
- Address **multicollinearity**.
- Ensure proper **scaling** and **feature engineering**.
