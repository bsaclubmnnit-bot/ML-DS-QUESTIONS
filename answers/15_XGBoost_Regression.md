# Section 15: XGBoost Regression

---

## Q195. What objectives can XGBoost use for regression?

XGBoost supports multiple **regression objectives**:

| Objective | Description | Use Case |
|---|---|---|
| `reg:squarederror` | Mean Squared Error (MSE) | Standard regression (default) |
| `reg:squaredlogerror` | Mean Squared Log Error | Targets with exponential scale |
| `reg:absoluteerror` | Mean Absolute Error | Robust to outliers |
| `reg:pseudohubererror` | Huber loss | Balance between MSE and MAE |
| `reg:tweedie` | Tweedie regression | Insurance, count data with zeros |
| `count:poisson` | Poisson regression | Count data |
| `survival:cox` | Cox proportional hazards | Survival analysis |

```python
import xgboost as xgb

# Standard regression
model = xgb.XGBRegressor(objective='reg:squarederror')

# Huber loss (more robust to outliers)
model = xgb.XGBRegressor(objective='reg:pseudohubererror')

# Log-scale targets (e.g., house prices)
model = xgb.XGBRegressor(objective='reg:squaredlogerror')

model.fit(X_train, y_train)
```

> [!TIP]
> Use `reg:absoluteerror` or `reg:pseudohubererror` when your target variable has significant outliers.

---

## Q196. How do you evaluate an XGBoost Regressor?

XGBoost regression models are evaluated using **standard regression metrics**:

| Metric | Formula | Interpretation |
|---|---|---|
| **RMSE** | `√(Σ(ŷᵢ - yᵢ)²/n)` | Same unit as target; sensitive to outliers |
| **MAE** | `Σ|ŷᵢ - yᵢ|/n` | More robust to outliers |
| **R²** | `1 - SS_res/SS_tot` | Proportion of variance explained (higher=better) |
| **MAPE** | `Σ|ŷᵢ - yᵢ|/yᵢ · 100%` | Percentage error; avoid when yᵢ≈0 |
| **MSLE** | `Σ(log(ŷ+1) - log(y+1))²/n` | For log-scale targets |

```python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
import numpy as np

y_pred = model.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test, y_pred))
mae  = mean_absolute_error(y_test, y_pred)
r2   = r2_score(y_test, y_pred)

print(f"RMSE: {rmse:.4f}")
print(f"MAE:  {mae:.4f}")
print(f"R²:   {r2:.4f}")
```

**Built-in eval metrics for early stopping:**
```python
model = xgb.XGBRegressor(eval_metric='rmse')
model.fit(X_train, y_train, eval_set=[(X_val, y_val)])
```

---

## Q197. How does early stopping work?

Early stopping monitors validation performance and **stops training when it stops improving**:

```python
model = xgb.XGBRegressor(
    n_estimators=2000,
    learning_rate=0.05,
    early_stopping_rounds=50,   # stop after 50 rounds with no improvement
    eval_metric='rmse'
)

model.fit(
    X_train, y_train,
    eval_set=[(X_val, y_val)],
    verbose=100  # print every 100 rounds
)

# Access results
print(f"Best iteration: {model.best_iteration}")
print(f"Best RMSE: {model.best_score:.4f}")
```

**Mechanism:**
1. After each tree, compute metric on `eval_set`
2. Track the **best score seen** so far
3. If no improvement for `early_stopping_rounds` consecutive rounds → stop
4. Final model uses weights from the **best iteration**

> [!IMPORTANT]
> The eval_set must be a **held-out validation set** not used in training. Using training data for early stopping defeats the purpose.

---

## Q198. How do you tune an XGBoost Regressor?

**Recommended tuning sequence:**

```python
from sklearn.model_selection import RandomizedSearchCV
import numpy as np

param_grid = {
    'n_estimators': [200, 500, 1000],
    'max_depth': [3, 4, 5, 6],
    'learning_rate': [0.01, 0.05, 0.1],
    'subsample': [0.6, 0.8, 1.0],
    'colsample_bytree': [0.6, 0.8, 1.0],
    'min_child_weight': [1, 3, 5],
    'gamma': [0, 0.1, 0.5],
    'reg_alpha': [0, 0.1, 1.0],
    'reg_lambda': [0.5, 1.0, 5.0]
}

model = xgb.XGBRegressor(objective='reg:squarederror', tree_method='hist')

search = RandomizedSearchCV(
    model, param_grid,
    n_iter=50, cv=5,
    scoring='neg_root_mean_squared_error',
    n_jobs=-1, random_state=42
)
search.fit(X_train, y_train)
print(search.best_params_)
```

**Tuning priority order:**
1. `max_depth` + `min_child_weight` (tree structure)
2. `subsample` + `colsample_bytree` (randomness)
3. `gamma` (pruning)
4. `reg_alpha` + `reg_lambda` (leaf regularization)
5. `learning_rate` + `n_estimators` (finalize with early stopping)

---

## Q199. How does max_depth affect regression?

`max_depth` controls the **complexity of each regression tree**:

| max_depth | Tree Complexity | Behavior |
|---|---|---|
| 2–3 | Simple, linear-ish | High bias, captures only simple patterns |
| 4–6 | Moderate | Good balance; most common range |
| 7–10 | Complex | Risk of overfitting |
| >10 | Very deep | Almost certainly overfitting |

```python
import matplotlib.pyplot as plt
from sklearn.model_selection import cross_val_score

depths = range(2, 10)
cv_scores = []

for d in depths:
    m = xgb.XGBRegressor(max_depth=d, n_estimators=100, learning_rate=0.1)
    scores = cross_val_score(m, X_train, y_train,
                             cv=5, scoring='neg_root_mean_squared_error')
    cv_scores.append(-scores.mean())

plt.plot(list(depths), cv_scores)
plt.xlabel('max_depth')
plt.ylabel('CV RMSE')
plt.title('max_depth vs RMSE')
plt.show()
```

> [!NOTE]
> In regression with many features and complex interactions, `max_depth=6` is a good starting point. Lower to 3–4 if overfitting is observed.

---

## Q200. How does subsampling reduce overfitting?

**Subsampling** injects randomness into the training process, similar to Random Forests:

**Row subsampling (`subsample`):**
```python
model = xgb.XGBRegressor(subsample=0.8)
# 80% of training rows used per tree (without replacement)
```

**Column subsampling (`colsample_bytree`):**
```python
model = xgb.XGBRegressor(colsample_bytree=0.7)
# 70% of features considered per tree
```

**How it reduces overfitting:**
1. Each tree sees a **different random subset** of data/features
2. Prevents individual trees from memorizing specific patterns
3. Reduces **correlation between trees** → better ensemble diversity
4. Similar to the bagging effect in Random Forest

```python
# Stochastic gradient boosting setup
model = xgb.XGBRegressor(
    subsample=0.8,
    colsample_bytree=0.8,
    colsample_bylevel=0.8
)
```

> [!TIP]
> Even `subsample=0.5` can dramatically reduce overfitting on small datasets while maintaining good performance.

---

## Q201. Can XGBoost model non-linear relationships?

**Yes** — XGBoost is inherently non-linear because it uses **decision trees as base learners**:

- Each tree creates **piecewise constant** regions in feature space
- The ensemble of many trees approximates **complex, non-linear functions**
- Automatically captures **feature interactions** at any depth
- No need for manual polynomial features or interaction terms

```python
import numpy as np
import matplotlib.pyplot as plt

# Non-linear data
X = np.linspace(0, 10, 200).reshape(-1, 1)
y = np.sin(X.ravel()) + 0.1 * np.random.randn(200)

model = xgb.XGBRegressor(n_estimators=100, max_depth=4)
model.fit(X, y)

y_pred = model.predict(X)
plt.plot(X, y, 'b.', label='Data')
plt.plot(X, y_pred, 'r-', label='XGBoost')
plt.legend()
plt.show()
```

> [!NOTE]
> Unlike linear regression, XGBoost requires no feature engineering to capture non-linear patterns. However, it cannot **extrapolate beyond the training range** — predictions plateau at the min/max training values.

---

## Q202. How do you compare XGBoost with Random Forest for regression?

| Aspect | XGBoost | Random Forest |
|---|---|---|
| **Algorithm** | Sequential boosting | Parallel bagging |
| **Bias-Variance** | Reduces both | Primarily reduces variance |
| **Performance ceiling** | Generally higher | Good out-of-the-box |
| **Tuning effort** | High (many hyperparameters) | Low |
| **Training time** | Slower (sequential) | Faster (parallel) |
| **Overfitting risk** | Higher (needs regularization) | Lower |
| **Outlier sensitivity** | Moderate (with Huber loss) | More robust |
| **Extrapolation** | Cannot extrapolate | Cannot extrapolate |

```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import r2_score

# Random Forest baseline
rf = RandomForestRegressor(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)
rf_r2 = r2_score(y_test, rf.predict(X_test))

# XGBoost
xgb_model = xgb.XGBRegressor(n_estimators=100, max_depth=5,
                               learning_rate=0.1, random_state=42)
xgb_model.fit(X_train, y_train)
xgb_r2 = r2_score(y_test, xgb_model.predict(X_test))

print(f"Random Forest R²: {rf_r2:.4f}")
print(f"XGBoost R²:       {xgb_r2:.4f}")
```

**When to prefer each:**
- **Random Forest:** Quick baseline, noisy data, less time to tune
- **XGBoost:** When pushing for maximum performance, structured tabular data, time to tune properly
