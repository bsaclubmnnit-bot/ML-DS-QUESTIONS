# Section 12: Random Forest

---

## Q155. What is a Random Forest?

**Random Forest** is an ensemble learning algorithm that builds many **decorrelated decision trees** and aggregates their predictions:

- **Classification**: majority vote across all trees
- **Regression**: mean of all tree predictions
- Introduced by Leo Breiman (2001)
- Combines **bagging** + **random feature selection** to create diverse, accurate trees

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

# Classification
rf_clf = RandomForestClassifier(n_estimators=100, random_state=42)
rf_clf.fit(X_train, y_train)

# Regression
rf_reg = RandomForestRegressor(n_estimators=100, random_state=42)
rf_reg.fit(X_train, y_train)
```

---

## Q156. How does Random Forest use Bagging?

Random Forest applies **bagging (Bootstrap AGGregating)**:

1. Draw `B` bootstrap samples (with replacement, size `n`) from the training data
2. Train one **full decision tree** on each bootstrap sample
3. At prediction time, aggregate all `B` tree predictions

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,     # B = 100 trees
    bootstrap=True,       # Use bootstrap sampling (True by default)
    random_state=42
)
```

- Each tree sees ~63.2% unique training samples (different subset per tree)
- The remaining ~36.8% are Out-of-Bag (OOB) samples — usable for free validation
- Parallel training: all trees are independent and can be trained simultaneously

---

## Q157. Why are Random Feature Subsets Used?

At each split, Random Forest considers only a **random subset of `m` features** (instead of all features). This is the key difference from plain bagging:

**Why it helps:**
- If one feature is very dominant, all trees would make similar first splits → **high correlation between trees**
- Random feature subsets **break this correlation** → trees become more diverse
- Diverse trees with uncorrelated errors provide greater variance reduction when averaged

**Default values:**
- Classification: `m = √p` (square root of total features)
- Regression: `m = p/3`

```python
rf = RandomForestClassifier(
    max_features='sqrt',   # √p features per split (default for classification)
    # max_features='log2' # log₂(p) features per split
    # max_features=0.5    # 50% of features per split
    random_state=42
)
```

---

## Q158. How does Random Forest Reduce Correlation Between Trees?

Two sources of randomness reduce tree correlation:

1. **Bootstrap sampling**: Each tree trains on a different random data subset
2. **Random feature selection at each split**: Each tree considers different features at each split point

Combined effect — recall the variance formula for an ensemble of `M` trees with correlation `ρ`:

$$\text{Var}(\text{RF}) = \rho \sigma^2 + \frac{1 - \rho}{M} \sigma^2$$

- **Plain bagging**: reduces `(1-ρ)/M` term, but `ρ` remains large if one feature dominates
- **Random Forest**: reduces `ρ` by random feature subsets → further reduces overall variance
- As `M → ∞`, variance approaches `ρσ²` (irreducible, based on remaining correlation)

---

## Q159. What is Out-of-Bag Error?

Since each tree is trained on a bootstrap sample (~63.2% of data), ~36.8% of samples are **Out-of-Bag (OOB)** for each tree. These samples can be used to estimate generalization error:

- For each training sample `xᵢ`, collect predictions from all trees where `xᵢ` was **not** in the bootstrap sample
- Aggregate those predictions → OOB prediction for `xᵢ`
- OOB error = error on OOB predictions across all training samples

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,
    oob_score=True,        # Enable OOB evaluation
    random_state=42
)
rf.fit(X_train, y_train)

print(f"OOB Score (Accuracy): {rf.oob_score_:.4f}")
# Access OOB predictions
oob_predictions = rf.oob_decision_function_   # shape: (n_samples, n_classes)
```

> OOB error closely approximates cross-validation error with no extra computational cost.

---

## Q160. How is Feature Importance Calculated?

Random Forest feature importance uses **Mean Decrease in Impurity (MDI)** — the total weighted impurity reduction attributable to each feature, averaged over all trees:

$$\text{FI}(j) = \frac{1}{B} \sum_{b=1}^{B} \sum_{\text{nodes in tree}_b \text{ using feature } j} \frac{n_t}{n} \left[\text{Impurity}(t) - \frac{n_L}{n_t}\text{Impurity}(L) - \frac{n_R}{n_t}\text{Impurity}(R)\right]$$

Values are normalized to sum to 1.

```python
import pandas as pd
import matplotlib.pyplot as plt

rf.fit(X_train, y_train)
importances = pd.Series(rf.feature_importances_, index=feature_names)
importances.sort_values(ascending=False).plot(kind='bar', figsize=(10, 4))
plt.title("Feature Importances (MDI)")
plt.tight_layout()
plt.show()
```

> **Warning:** MDI can be **biased toward high-cardinality features**. Use Permutation Importance for a less biased estimate.

---

## Q161. What is Permutation Importance?

**Permutation Importance** measures feature importance by computing how much the model's performance **degrades** when a feature's values are randomly shuffled (breaking its relationship with the target):

$$\text{PI}(j) = \text{Score}(X, y) - \text{Score}(X_{\text{permuted}_j}, y)$$

```python
from sklearn.inspection import permutation_importance

result = permutation_importance(
    rf, X_test, y_test,
    n_repeats=10,       # Repeat permutation 10 times for stability
    random_state=42,
    n_jobs=-1
)

perm_importances = pd.Series(
    result.importances_mean,
    index=feature_names
).sort_values(ascending=False)
print(perm_importances)
```

| | MDI (Built-in) | Permutation Importance |
|-|---------------|----------------------|
| **Speed** | Fast | Slower |
| **Bias** | Biased to high-cardinality | Less biased |
| **Data** | Uses training data | Can use test data |
| **Reliability** | Can overfit | More reliable |

---

## Q162. Can Random Forest Overfit?

**Yes, but it is much harder to overfit than a single Decision Tree:**

- Adding more trees (`n_estimators`) does **not** cause overfitting — error plateaus as trees increase
- However, individual trees can still overfit if not constrained (`max_depth`, `min_samples_leaf`)
- Setting `max_features` too high → more correlated trees → less variance reduction

**When Random Forest can overfit:**
- Very noisy datasets with many irrelevant features
- Very small datasets (high variance in bootstrap samples)
- No depth/leaf constraints on individual trees

```python
# Monitor OOB error as n_estimators increases
oob_errors = []
for n in range(1, 200):
    rf = RandomForestClassifier(n_estimators=n, oob_score=True, random_state=42)
    rf.fit(X_train, y_train)
    oob_errors.append(1 - rf.oob_score_)
# OOB error should decrease and plateau, not increase
```

---

## Q163. What Hyperparameters are Important?

| Hyperparameter | Default | Effect |
|---------------|---------|--------|
| `n_estimators` | 100 | Number of trees; more = better (diminishing returns) |
| `max_features` | `'sqrt'` | Features per split; lower = more diversity |
| `max_depth` | None | Max tree depth; lower = less overfitting |
| `min_samples_split` | 2 | Min samples to split; higher = simpler trees |
| `min_samples_leaf` | 1 | Min samples per leaf; higher = smoother predictions |
| `max_leaf_nodes` | None | Max leaves per tree |
| `bootstrap` | True | Whether to use bootstrap sampling |
| `class_weight` | None | Handle class imbalance |
| `n_jobs` | 1 | Parallelism; `-1` = all cores |

```python
from sklearn.model_selection import RandomizedSearchCV

param_dist = {
    'n_estimators': [100, 200, 500],
    'max_depth': [None, 10, 20, 30],
    'max_features': ['sqrt', 'log2', 0.5],
    'min_samples_leaf': [1, 2, 5, 10]
}

rf_search = RandomizedSearchCV(
    RandomForestClassifier(random_state=42),
    param_distributions=param_dist,
    n_iter=20, cv=5, scoring='f1', n_jobs=-1
)
rf_search.fit(X_train, y_train)
print(rf_search.best_params_)
```

---

## Q164. How does `max_features` Affect the Model?

`max_features` controls the number of features considered at **each split** — the primary lever for controlling tree diversity:

| `max_features` Value | Effect |
|---------------------|--------|
| Low (e.g., 1) | Very diverse trees, high bias per tree, low correlation |
| `'sqrt'` (default) | Good balance — standard recommendation |
| High (e.g., all features) | Less diverse trees, similar to plain bagging |
| All features | No feature randomness → highest correlation between trees |

```
Trade-off:
Low max_features  →  High tree diversity  →  Lower variance, higher per-tree bias
High max_features →  Low tree diversity   →  Higher variance, lower per-tree bias
```

---

## Q165. How does `max_depth` Affect the Model?

`max_depth` controls the depth of **individual trees** in the forest:

| `max_depth` | Per-tree Bias | Per-tree Variance | Forest Behavior |
|-------------|-------------|-----------------|----------------|
| Very small (1-3) | High | Low | Underfitting even with many trees |
| Moderate | Balanced | Balanced | Best performance |
| None (unlimited) | Low | High | Trees overfit, but ensemble averages it out |

```python
# Default: max_depth=None (fully grown trees)
# Random Forest is robust to deep trees because averaging reduces variance
rf_deep = RandomForestClassifier(max_depth=None, n_estimators=100)   # typical
rf_shallow = RandomForestClassifier(max_depth=5, n_estimators=100)   # more regularized
```

> Unlike single Decision Trees, Random Forest with `max_depth=None` typically **doesn't drastically overfit** due to averaging — but constraining depth can still help on noisy data.

---

## Q166. How does Random Forest Handle Imbalanced Classes?

Random Forest, like most algorithms, is biased toward the majority class. Several strategies help:

```python
# 1. class_weight parameter
rf = RandomForestClassifier(
    class_weight='balanced',        # weights inversely proportional to class frequency
    # class_weight='balanced_subsample'  # recalculated per bootstrap sample
    random_state=42
)

# 2. Resampling before training
from imblearn.over_sampling import SMOTE
from imblearn.ensemble import BalancedRandomForestClassifier

# BalancedRandomForestClassifier undersamples majority class in each bootstrap
brf = BalancedRandomForestClassifier(n_estimators=100, random_state=42)
brf.fit(X_train, y_train)

# 3. Adjust decision threshold
probas = rf.predict_proba(X_test)[:, 1]
threshold = 0.3   # Lower threshold favors minority class
y_pred = (probas >= threshold).astype(int)
```

---

## Q167. What are Random Forest Advantages?

| Advantage | Detail |
|-----------|--------|
| ✅ **High accuracy** | One of the best out-of-the-box classifiers |
| ✅ **Robust to overfitting** | Averaging reduces variance significantly |
| ✅ **Handles high dimensions** | Works well even with many features |
| ✅ **Feature importance** | Built-in, interpretable importance scores |
| ✅ **OOB evaluation** | Free validation without extra data split |
| ✅ **Handles missing values** | Some implementations support it |
| ✅ **No feature scaling needed** | Tree-based, scale-invariant |
| ✅ **Parallelizable** | Trees trained independently |
| ✅ **Robust to outliers** | Averaging reduces outlier influence |
| ✅ **Works for both tasks** | Classification and Regression |

---

## Q168. What are Random Forest Disadvantages?

| Disadvantage | Detail |
|-------------|--------|
| ❌ **Not interpretable** | Black-box; can't visualize the overall model |
| ❌ **Slow prediction** | Must aggregate `B` tree predictions at inference |
| ❌ **Memory-intensive** | Stores all `B` trees in memory |
| ❌ **Poor extrapolation** | Like all tree methods, can't predict beyond training range |
| ❌ **Not optimal for sparse data** | Linear models may outperform on very sparse inputs |
| ❌ **MDI importance bias** | Built-in importance biased toward high-cardinality features |
| ❌ **Large models** | Hundreds of trees = large storage footprint |
| ❌ **Slower than linear models** | For real-time inference on resource-constrained devices |

**When to prefer alternatives:**
- **Interpretability required** → Single Decision Tree, Logistic Regression
- **Best accuracy** → XGBoost / LightGBM often outperform Random Forest
- **Very high-dimensional sparse data** → Linear SVM, Logistic Regression
- **Real-time inference** → Simpler models or model distillation
