# Section 6: Ridge and Lasso Practical Implementation

## Q80. How do you implement Ridge Regression?

```python
from sklearn.linear_model import Ridge
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score
import numpy as np

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('ridge', Ridge(alpha=1.0))  # alpha = regularization strength
])

pipe.fit(X_train, y_train)
y_pred = pipe.predict(X_test)
print("R²:", r2_score(y_test, y_pred))
print("Coefficients:", pipe.named_steps['ridge'].coef_)
```

---

## Q81. How do you implement Lasso Regression?

```python
from sklearn.linear_model import Lasso
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('lasso', Lasso(alpha=0.1, max_iter=10000))
])

pipe.fit(X_train, y_train)
y_pred = pipe.predict(X_test)

# Check which features were selected (non-zero coefficients)
coefs = pipe.named_steps['lasso'].coef_
selected = [(f, c) for f, c in zip(feature_names, coefs) if c != 0]
print("Selected features:", selected)
```

---

## Q82. Why should scaling be inside a pipeline?

**Outside pipeline (WRONG — causes leakage):**
```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)  # Leaks test statistics!
scores = cross_val_score(Ridge(), X_scaled, y, cv=5)
```

**Inside pipeline (CORRECT):**
```python
pipe = Pipeline([('scaler', StandardScaler()), ('ridge', Ridge())])
scores = cross_val_score(pipe, X, y, cv=5)  # Scaler fit on train fold only
```

When the scaler is inside the pipeline, it's re-fit on each training fold during cross-validation, preventing the test fold's statistics from influencing preprocessing.

---

## Q83. How do you tune alpha?

```python
from sklearn.model_selection import GridSearchCV
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge
import numpy as np

pipe = Pipeline([('scaler', StandardScaler()), ('ridge', Ridge())])

param_grid = {'ridge__alpha': np.logspace(-3, 3, 50)}

grid_search = GridSearchCV(pipe, param_grid, cv=5, scoring='neg_root_mean_squared_error')
grid_search.fit(X_train, y_train)

print("Best alpha:", grid_search.best_params_['ridge__alpha'])
print("Best CV RMSE:", -grid_search.best_score_)
```

Use a **log-scale** for alpha search since it spans orders of magnitude.

---

## Q84. What is RidgeCV?

`RidgeCV` is an efficient cross-validated Ridge Regression. It uses **generalized cross-validation (GCV)** to select the best alpha without repeating full training multiple times:

```python
from sklearn.linear_model import RidgeCV
import numpy as np

# Try multiple alphas automatically
ridge_cv = RidgeCV(alphas=np.logspace(-3, 3, 50), scoring='neg_mean_squared_error', cv=5)
ridge_cv.fit(X_train_scaled, y_train)

print("Best alpha:", ridge_cv.alpha_)
print("CV Score:", ridge_cv.best_score_)
```

More efficient than `GridSearchCV` for Ridge specifically. Note: scaling should still be done separately or in a pipeline.

---

## Q85. What is LassoCV?

`LassoCV` uses **coordinate descent** with k-fold CV to find the best alpha for Lasso:

```python
from sklearn.linear_model import LassoCV
import numpy as np

lasso_cv = LassoCV(alphas=np.logspace(-4, 1, 50), cv=5, max_iter=10000)
lasso_cv.fit(X_train_scaled, y_train)

print("Best alpha:", lasso_cv.alpha_)
print("Non-zero coefs:", np.sum(lasso_cv.coef_ != 0))
```

It follows the **regularization path** efficiently — evaluates many alphas faster than naive CV.

---

## Q86. How do you interpret features selected by Lasso?

Lasso sets irrelevant feature coefficients to exactly zero, performing **automatic feature selection**:

```python
import pandas as pd

coefs = pd.Series(lasso_model.coef_, index=feature_names)
selected = coefs[coefs != 0].sort_values(key=abs, ascending=False)
print("Selected features and their coefficients:")
print(selected)
```

**Interpretation:**
- **Non-zero coefficient** = feature is selected and contributes to prediction
- **Magnitude** = relative importance (after scaling)
- **Sign** = direction of effect (positive = increases prediction, negative = decreases)

---

## Q87. What happens when alpha is too high?

When alpha (regularization strength) is too high:
- Penalty dominates the loss function
- All coefficients are shrunk heavily toward zero
- Model becomes **overly simple** → **underfitting**
- High bias, low variance
- Training and test performance both suffer

```python
# Extreme alpha → near-zero coefficients
ridge = Ridge(alpha=1e6)
ridge.fit(X_train_scaled, y_train)
print(ridge.coef_)  # All near zero
```

---

## Q88. What happens when alpha is too low?

When alpha is too low (approaching 0):
- Regularization has minimal effect
- Model behaves like **ordinary linear regression**
- **Overfitting** likely with high-dimensional data
- Low bias, high variance
- Good training performance, poor test performance

At `alpha=0`, Ridge = OLS. Lasso with `alpha=0` also becomes OLS.

---

## Q89. How do you compare Linear, Ridge, and Lasso?

```python
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import cross_val_score
import numpy as np

models = {
    'Linear': LinearRegression(),
    'Ridge': Ridge(alpha=1.0),
    'Lasso': Lasso(alpha=0.1, max_iter=10000)
}

results = {}
for name, model in models.items():
    pipe = Pipeline([('scaler', StandardScaler()), ('model', model)])
    scores = cross_val_score(pipe, X, y, cv=5, scoring='neg_root_mean_squared_error')
    results[name] = -scores.mean()
    print(f"{name}: RMSE = {-scores.mean():.4f} ± {scores.std():.4f}")
```

| Model | Use When | Behavior |
|-------|----------|----------|
| Linear | Few features, no multicollinearity | No regularization |
| Ridge | Multicollinearity present | Shrinks all coefs |
| Lasso | Feature selection needed | Zeros out some coefs |
| Elastic Net | Both situations | Combination of Ridge + Lasso |

