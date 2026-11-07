# Section 10: Decision Tree Regression

---

## Q131. How does a Regression Tree differ from a Classification Tree?

| Aspect | Classification Tree | Regression Tree |
|--------|-------------------|----------------|
| **Target variable** | Discrete class labels | Continuous numerical values |
| **Leaf prediction** | Majority class | Mean of training samples |
| **Split criterion** | Gini impurity / Entropy | MSE / MAE / Variance reduction |
| **Evaluation** | Accuracy, F1 | MAE, MSE, R² |
| **Output** | Class label | Numerical value |

Both share the same **tree-growing algorithm** — the difference is only in how leaves are evaluated and what they predict.

```python
from sklearn.tree import DecisionTreeRegressor

reg = DecisionTreeRegressor(max_depth=5, random_state=42)
reg.fit(X_train, y_train)
y_pred = reg.predict(X_test)
```

---

## Q132. What split criterion is used?

Regression Trees use **variance reduction** (equivalent to minimizing MSE) as the split criterion:

$$\text{MSE}(t) = \frac{1}{n_t} \sum_{i \in t} (y_i - \bar{y}_t)^2$$

$$\text{Variance Reduction} = \text{MSE}(\text{parent}) - \frac{n_L}{n} \text{MSE}(L) - \frac{n_R}{n} \text{MSE}(R)$$

The split that **maximizes variance reduction** (minimizes weighted child MSE) is chosen.

```python
# Available criteria in scikit-learn
reg_mse = DecisionTreeRegressor(criterion='squared_error')   # default (MSE)
reg_mae = DecisionTreeRegressor(criterion='absolute_error')  # MAE-based
reg_fri = DecisionTreeRegressor(criterion='friedman_mse')    # Improved MSE heuristic
```

---

## Q133. How does a Regression Tree make predictions?

For a given input `x`, the tree routes it down the branches using learned rules until it reaches a **leaf node**. The prediction is the **mean of the training samples** in that leaf:

$$\hat{y} = \bar{y}_{\text{leaf}} = \frac{1}{|\mathcal{L}|} \sum_{i \in \mathcal{L}} y_i$$

**Example:**
```
Feature Age ≤ 30?
├── YES → Leaf: mean salary = $45,000 → predict $45,000
└── NO  → Feature Experience > 5?
          ├── YES → Leaf: mean = $95,000 → predict $95,000
          └── NO  → Leaf: mean = $72,000 → predict $72,000
```

---

## Q134. Why do Regression Trees produce piecewise constant predictions?

Regression Trees make **axis-aligned, rectangular splits** — each leaf covers a rectangular region of the feature space, and all inputs in that region receive the **same constant prediction** (the leaf mean).

- The prediction surface is a **step function** — flat within each partition
- This is fundamentally different from linear regression which produces a smooth plane

```python
import numpy as np
import matplotlib.pyplot as plt

# Visualizing piecewise constant nature
X = np.linspace(0, 10, 100).reshape(-1, 1)
reg = DecisionTreeRegressor(max_depth=3).fit(X, np.sin(X).ravel())
y_pred = reg.predict(X)
# y_pred will be a staircase approximation of sin(X)
```

> This is why deeper trees are needed to approximate smooth functions — each additional split refines the approximation.

---

## Q135. Can Regression Trees Extrapolate?

**No — Regression Trees cannot extrapolate beyond the range of training data.**

- Predictions are bounded by the range of training labels (`min(y_train)` to `max(y_train)`)
- For inputs outside the training range, the tree returns the mean of the closest boundary leaf
- This is a **fundamental limitation** compared to linear regression

```python
import numpy as np

X_train = np.arange(1, 11).reshape(-1, 1)
y_train = X_train.ravel() * 2   # y = 2x, range [2, 20]

reg = DecisionTreeRegressor().fit(X_train, y_train)

# Extrapolation attempt: x=20 → still predicts ~20, NOT 40
print(reg.predict([[20]]))   # Returns max leaf mean, not 40
```

**Contrast:** Linear regression would correctly predict y=40 for x=20.

---

## Q136. What causes Regression Trees to Overfit?

Without constraints, a Regression Tree will grow until each leaf contains a **single training sample** (MSE = 0 on training set), completely memorizing the data:

- **No depth limit** → tree keeps splitting until pure leaves
- **Small min_samples_leaf** → leaves based on very few points
- **Noisy targets** → tree learns noise as signal
- **High-dimensional features** → more splits possible

**Detecting overfitting:**
```python
reg = DecisionTreeRegressor()
reg.fit(X_train, y_train)
print(f"Train R²: {reg.score(X_train, y_train):.4f}")  # ~1.0
print(f"Test  R²: {reg.score(X_test, y_test):.4f}")    # Much lower
```

---

## Q137. How do you prune a Regression Tree?

### Pre-pruning (Constraining Growth)
```python
reg = DecisionTreeRegressor(
    max_depth=5,              # Limit depth
    min_samples_split=10,     # Min samples to split a node
    min_samples_leaf=5,       # Min samples in a leaf
    max_leaf_nodes=20,        # Limit total number of leaves
    random_state=42
)
```

### Post-pruning (Cost-Complexity Pruning)
```python
# Find effective alphas
path = DecisionTreeRegressor().cost_complexity_pruning_path(X_train, y_train)
ccp_alphas = path.ccp_alphas[:-1]   # Exclude trivial alpha

# Cross-validate each alpha
from sklearn.model_selection import cross_val_score

cv_scores = []
for alpha in ccp_alphas:
    reg = DecisionTreeRegressor(ccp_alpha=alpha, random_state=42)
    score = cross_val_score(reg, X_train, y_train, cv=5, scoring='r2').mean()
    cv_scores.append(score)

best_alpha = ccp_alphas[np.argmax(cv_scores)]
```

---

## Q138. What metrics evaluate Regression Trees?

| Metric | Formula | Notes |
|--------|---------|-------|
| **MAE** | `(1/n) Σ\|yᵢ - ŷᵢ\|` | Robust to outliers, interpretable |
| **MSE** | `(1/n) Σ(yᵢ - ŷᵢ)²` | Penalizes large errors more |
| **RMSE** | `√MSE` | Same units as target |
| **R²** | `1 - SS_res/SS_tot` | Proportion of variance explained |
| **MAPE** | `(1/n) Σ\|yᵢ - ŷᵢ\|/yᵢ` | Percentage error (avoid if yᵢ ≈ 0) |

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

mae  = mean_absolute_error(y_test, y_pred)
mse  = mean_squared_error(y_test, y_pred)
rmse = mean_squared_error(y_test, y_pred, squared=False)
r2   = r2_score(y_test, y_pred)
```

---

## Q139. How do Outliers Affect Regression Trees?

Outliers affect Regression Trees in two ways:

1. **Outlier targets in leaves:** Outlier `yᵢ` values inflate the leaf mean → biased predictions for the whole leaf region
2. **Outlier features drive splits:** Extreme `xᵢ` values can cause the tree to create splits that separate outliers from the rest, wasting splitting capacity on noise

**Mitigation:**
- Use **MAE criterion** instead of MSE (more robust to outliers)
- Cap/clip extreme target values before training
- Use `min_samples_leaf` to ensure leaves aren't dominated by single outliers

```python
reg = DecisionTreeRegressor(
    criterion='absolute_error',  # Robust to outliers
    min_samples_leaf=5,
    random_state=42
)
```

---

## Q140. How does tree depth affect performance?

Tree depth is the primary control of the **bias-variance tradeoff**:

| Depth | Bias | Variance | Effect |
|-------|------|----------|--------|
| Very shallow (1-2) | High | Low | Underfitting — misses important patterns |
| Moderate | Balanced | Balanced | Best generalization (found via CV) |
| Very deep (unlimited) | Low | High | Overfitting — memorizes training data |

```python
import matplotlib.pyplot as plt
from sklearn.model_selection import cross_val_score

depths = range(1, 20)
train_scores, cv_scores = [], []

for d in depths:
    reg = DecisionTreeRegressor(max_depth=d, random_state=42)
    reg.fit(X_train, y_train)
    train_scores.append(reg.score(X_train, y_train))
    cv_scores.append(cross_val_score(reg, X_train, y_train, cv=5).mean())

# Plot: train score increases, cv score peaks then drops
```

> The optimal depth is where cross-validation score peaks — this represents the best trade-off between fitting the data and generalizing to unseen samples.
