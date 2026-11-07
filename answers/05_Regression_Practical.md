# Section 5: Regression Practical Implementation

## Q66. How do you handle missing values before regression?

**Strategies:**

| Strategy | When to Use | Code |
|----------|-------------|------|
| Drop rows | Few missing values | `df.dropna()` |
| Mean/Median imputation | Random missing, numerical | `SimpleImputer(strategy='mean')` |
| Mode imputation | Categorical features | `SimpleImputer(strategy='most_frequent')` |
| Forward/Backward fill | Time-series data | `df.fillna(method='ffill')` |
| KNN imputation | Complex patterns | `KNNImputer(n_neighbors=5)` |
| Model-based imputation | Best quality, expensive | `IterativeImputer()` |

```python
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(strategy='median')
X_imputed = imputer.fit_transform(X)
```

Always fit on training data only, transform on both train and test to avoid leakage.

---

## Q67. How do you encode categorical variables?

| Encoding | Use Case | Notes |
|----------|----------|-------|
| **One-Hot Encoding** | Nominal (no order) | Drops one column to avoid multicollinearity |
| **Ordinal Encoding** | Ordinal (e.g., Low/Med/High) | Preserves order |
| **Label Encoding** | Tree-based models only | Don't use for linear models |
| **Target Encoding** | High cardinality | Risk of leakage if not done carefully |

```python
from sklearn.preprocessing import OneHotEncoder
enc = OneHotEncoder(drop='first', sparse_output=False)
X_encoded = enc.fit_transform(X[['category_col']])
```

---

## Q68. When should features be standardized?

**Standardize when:**
- Algorithm is distance-based (KNN, SVM, k-Means)
- Algorithm uses gradient descent (Linear Regression, Logistic Regression, Neural Networks)
- Using Ridge or Lasso (regularization is scale-sensitive)

**No need to standardize for:**
- Tree-based models (Decision Trees, Random Forest, XGBoost)
- Models that don't compute distances

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)  # Use training stats!
```

---

## Q69. How do you split data for regression?

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,      # 80% train, 20% test
    random_state=42     # Reproducibility
)
```

For time-series data, **always split chronologically** (not randomly) to avoid data leakage:
```python
# Time series split
split_idx = int(0.8 * len(df))
train, test = df[:split_idx], df[split_idx:]
```

---

## Q70. How do you implement Linear Regression using scikit-learn?

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
import numpy as np

# Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train
model = LinearRegression()
model.fit(X_train, y_train)

# Predict
y_pred = model.predict(X_test)

# Evaluate
print("R²:", r2_score(y_test, y_pred))
print("RMSE:", np.sqrt(mean_squared_error(y_test, y_pred)))
print("Coefficients:", model.coef_)
print("Intercept:", model.intercept_)
```

---

## Q71. What metrics evaluate regression models?

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **MAE** | $\frac{1}{n}\sum|y_i - \hat{y}_i|$ | Average absolute error |
| **MSE** | $\frac{1}{n}\sum(y_i - \hat{y}_i)^2$ | Penalizes large errors more |
| **RMSE** | $\sqrt{MSE}$ | Same unit as target |
| **R²** | $1 - \frac{SS_{res}}{SS_{tot}}$ | Proportion of variance explained |
| **Adj. R²** | Adjusted for # features | Better for multiple regression |
| **MAPE** | $\frac{1}{n}\sum\frac{|y_i - \hat{y}_i|}{y_i} \times 100$ | Percentage error |

---

## Q72. What is MAE?

**Mean Absolute Error** = average of absolute differences between predictions and actuals:
$$\text{MAE} = \frac{1}{n}\sum_{i=1}^n |y_i - \hat{y}_i|$$

- Robust to outliers (unlike MSE)
- Same unit as the target variable
- Intuitive: "on average, predictions are off by X units"

```python
from sklearn.metrics import mean_absolute_error
mae = mean_absolute_error(y_test, y_pred)
```

---

## Q73. What is MSE?

**Mean Squared Error** = average of squared differences:
$$\text{MSE} = \frac{1}{n}\sum_{i=1}^n (y_i - \hat{y}_i)^2$$

- Heavily penalizes large errors (squaring amplifies outliers)
- Differentiable, making it useful for optimization
- Unit is the square of the target variable

```python
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(y_test, y_pred)
```

---

## Q74. What is RMSE?

**Root Mean Squared Error** = square root of MSE:
$$\text{RMSE} = \sqrt{\frac{1}{n}\sum_{i=1}^n (y_i - \hat{y}_i)^2}$$

- Same unit as the target variable (unlike MSE)
- More sensitive to outliers than MAE
- Most commonly reported metric for regression

```python
import numpy as np
rmse = np.sqrt(mean_squared_error(y_test, y_pred))
# Or in newer sklearn:
rmse = mean_squared_error(y_test, y_pred, squared=False)
```

---

## Q75. When is MAE preferred over RMSE?

| Prefer MAE | Prefer RMSE |
|-----------|------------|
| Outliers are present and should not dominate | Large errors are particularly undesirable |
| Target variable has heavy-tailed distribution | Smooth optimization is needed |
| Interpretability is key | Penalizing large deviations is important |
| Robust evaluation needed | Standard practice in a domain |

**Rule of thumb:** If large errors are especially bad (e.g., medical dosing), use RMSE. If the data has natural outliers that aren't mistakes, use MAE.

---

## Q76. What is MAPE and what are its limitations?

**Mean Absolute Percentage Error:**
$$\text{MAPE} = \frac{100\%}{n} \sum_{i=1}^n \left|\frac{y_i - \hat{y}_i}{y_i}\right|$$

**Advantages:** Scale-independent, easy to explain ("predictions are off by X%")

**Limitations:**
- **Undefined** when $y_i = 0$
- **Asymmetric**: over-forecasting and under-forecasting penalized differently
- **Biased** toward lower predictions for skewed distributions
- **Poor for small values**: 1 unit error on $y=2$ = 50% error

Alternative: **SMAPE** (Symmetric MAPE) handles some of these issues.

---

## Q77. How does cross-validation work for regression?

Cross-validation estimates model performance on unseen data by training and evaluating multiple times on different splits:

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LinearRegression

model = LinearRegression()
scores = cross_val_score(model, X, y, cv=5, scoring='neg_root_mean_squared_error')
print("Mean RMSE:", -scores.mean())
print("Std:", scores.std())
```

**K-Fold CV steps:**
1. Split data into K equal folds
2. Train on K-1 folds, validate on 1
3. Repeat K times (each fold used as validation once)
4. Average the K validation scores

For time series, use `TimeSeriesSplit` to maintain temporal order.

---

## Q78. How do pipelines prevent data leakage?

**Data leakage** occurs when test data information influences preprocessing (e.g., fitting a scaler on the entire dataset before splitting).

A `Pipeline` ensures preprocessing is **fit only on training data** and applied to test data:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('model', LinearRegression())
])

# During cross-validation, scaler is fit ONLY on training fold
scores = cross_val_score(pipe, X, y, cv=5, scoring='r2')
```

Without a pipeline, fitting the scaler on all data before CV would leak test statistics into training.

---

## Q79. How do you interpret residuals?

**Residual** = $y_i - \hat{y}_i$ (actual minus predicted)

**Ideal residual plots:**
- **Residuals vs Fitted**: Random scatter around 0 (no pattern = linearity holds)
- **Q-Q Plot**: Points along diagonal line = normality of errors
- **Scale-Location**: Horizontal band = homoscedasticity
- **Residuals vs Leverage**: Identifies influential outliers

**What patterns indicate:**

| Pattern | Problem |
|---------|---------|
| U-shape or curve | Non-linearity — need polynomial features |
| Fan shape | Heteroscedasticity — consider log transform |
| Systematic shift | Omitted variable bias |
| Outliers with high leverage | Influential points distorting the fit |

```python
import matplotlib.pyplot as plt
residuals = y_test - y_pred
plt.scatter(y_pred, residuals)
plt.axhline(0, color='red', linestyle='--')
plt.xlabel('Predicted'); plt.ylabel('Residuals')
plt.title('Residuals vs Fitted')
plt.show()
```

