# Section 14: XGBoost Classification

---

## Q181. What is XGBoost?

**XGBoost (Extreme Gradient Boosting)** is an optimized, scalable implementation of gradient boosting developed by Tianqi Chen. It is one of the most widely used ML algorithms in competitions and production.

**Key features:**
- Regularized gradient boosting (L1 + L2)
- Second-order gradient optimization (uses Hessians)
- Built-in handling of missing values
- Tree pruning using `gamma`
- Parallel and distributed computing support
- Column and row subsampling

```python
import xgboost as xgb

model = xgb.XGBClassifier(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=6,
    use_label_encoder=False,
    eval_metric='logloss'
)
model.fit(X_train, y_train)
```

> [!NOTE]
> XGBoost won or contributed to winning solutions in many Kaggle competitions and is widely used in industry for tabular data.

---

## Q182. How does XGBoost differ from traditional Gradient Boosting?

| Feature | Traditional GBM | XGBoost |
|---|---|---|
| **Optimization** | First-order gradients | Second-order (gradient + Hessian) |
| **Regularization** | None (sklearn) | L1 (alpha) + L2 (lambda) |
| **Missing values** | Manual imputation | Built-in handling |
| **Tree pruning** | Pre-pruning (max_depth) | Post-pruning with gamma |
| **Speed** | Slow | Much faster (parallel, cache-aware) |
| **Subsampling** | Row only | Row + column + level |
| **Cross-validation** | Separate step | Built-in `cv()` |

```python
# XGBoost with DMatrix for maximum performance
dtrain = xgb.DMatrix(X_train, label=y_train)
dval = xgb.DMatrix(X_val, label=y_val)

params = {'max_depth': 6, 'eta': 0.1, 'objective': 'binary:logistic'}
model = xgb.train(params, dtrain, num_boost_round=100,
                  evals=[(dval, 'val')], early_stopping_rounds=10)
```

---

## Q183. What is the role of gradients and Hessians?

XGBoost uses a **second-order Taylor expansion** of the loss function to find optimal tree structures:

```
L ≈ Σ [gᵢ · f(xᵢ) + 0.5 · hᵢ · f(xᵢ)²] + Ω(f)
```

- **Gradient (gᵢ)** = first derivative of loss w.r.t. prediction = direction of steepest descent
- **Hessian (hᵢ)** = second derivative of loss = curvature of the loss surface

**Why Hessians matter:**
- They provide a **better quadratic approximation** of the loss
- Allow computation of **optimal leaf values** analytically:
  ```
  w*ⱼ = -Gⱼ / (Hⱼ + λ)
  ```
  Where `Gⱼ = Σgᵢ` and `Hⱼ = Σhᵢ` for samples in leaf j

- Lead to **better split scoring** and faster convergence

> [!NOTE]
> Using second-order information means XGBoost needs fewer trees to achieve the same accuracy compared to first-order GBM.

---

## Q184. What regularization does XGBoost use?

XGBoost adds a **regularization term** directly to the objective:

```
Ω(f) = γ · T + 0.5 · λ · Σ wⱼ²  + α · Σ |wⱼ|
```

Where:
- **T** = number of leaves in the tree
- **γ (gamma)** = minimum loss reduction required for a split (complexity penalty on number of leaves)
- **λ (lambda)** = L2 regularization on leaf weights
- **α (alpha)** = L1 regularization on leaf weights
- **wⱼ** = weight (output value) of leaf j

This penalizes both:
- **Model complexity** (too many leaves via gamma)
- **Large leaf weights** (via lambda/alpha)

```python
model = xgb.XGBClassifier(
    gamma=0.1,      # min gain to make a split
    reg_lambda=1.0, # L2
    reg_alpha=0.0   # L1
)
```

---

## Q185. What are gamma, lambda, and alpha?

| Parameter | Type | Effect | Default |
|---|---|---|---|
| **gamma** | Min split gain | A split is only made if it reduces loss by at least gamma. Higher = fewer splits = simpler trees | 0 |
| **lambda** (reg_lambda) | L2 regularization | Penalizes large leaf weights. Smooths predictions. | 1 |
| **alpha** (reg_alpha) | L1 regularization | Encourages sparse leaf weights (some become 0). Useful for high-dimensional data. | 0 |

```python
# gamma: controls tree depth indirectly
model = xgb.XGBClassifier(gamma=0.5)  # require >0.5 gain to split

# lambda: smooth predictions
model = xgb.XGBClassifier(reg_lambda=5.0)  # stronger L2

# alpha: useful for sparse features
model = xgb.XGBClassifier(reg_alpha=0.1)  # light L1
```

> [!TIP]
> Start with tuning `max_depth`, `learning_rate`, and `n_estimators`. Then use `gamma` and `lambda` for fine-grained regularization.

---

## Q186. What is max_depth?

`max_depth` controls the **maximum depth of each tree** in the ensemble.

- **Deeper trees** → more complex interactions captured → higher variance, lower bias
- **Shallower trees** → simpler model → lower variance, higher bias

| max_depth | Effect |
|---|---|
| 1 | Decision stump (like AdaBoost) |
| 3–6 | Typical range for XGBoost |
| >10 | Usually overfitting |

```python
# Typical tuning range
for depth in [3, 4, 5, 6, 7]:
    model = xgb.XGBClassifier(max_depth=depth)
    # evaluate with cross-validation
```

> [!IMPORTANT]
> XGBoost default is `max_depth=6`. For most tabular problems, values of 3–6 work best. Deeper trees need stronger regularization.

---

## Q187. What is min_child_weight?

`min_child_weight` is the **minimum sum of instance weights (Hessians)** required in a child node to make a split.

- If a proposed split creates a child node with total Hessian < `min_child_weight`, the split is rejected
- Acts as a **regularization mechanism** against splits on very few or very uncertain samples
- Equivalent to `min_samples_leaf` but in terms of Hessian sum, not sample count

```python
model = xgb.XGBClassifier(
    min_child_weight=5  # require at least 5 Hessian units per leaf
)
```

**Effect:**
- **Higher** → more conservative (fewer splits, simpler trees)
- **Lower** → more splits allowed (risk of overfitting)

> [!NOTE]
> For imbalanced datasets, `min_child_weight=1` may work better since the minority class has low Hessian sums.

---

## Q188. What are subsample and colsample_bytree?

These are **stochastic regularization** parameters that introduce randomness into training:

**`subsample`** — fraction of training rows sampled per tree:
```python
model = xgb.XGBClassifier(subsample=0.8)  # use 80% of rows per tree
```
- Prevents overfitting (like Random Forest's row sampling)
- Reduces correlation between trees

**`colsample_bytree`** — fraction of features sampled per tree:
```python
model = xgb.XGBClassifier(colsample_bytree=0.8)  # use 80% of features
```

**Other column sampling levels:**
| Parameter | Sampling Level |
|---|---|
| `colsample_bytree` | Once per tree |
| `colsample_bylevel` | Once per tree depth level |
| `colsample_bynode` | Once per split |

> [!TIP]
> Values of 0.6–0.9 typically work well. Combined with `subsample`, they significantly reduce overfitting.

---

## Q189. What is early stopping?

**Early stopping** halts training when the validation metric stops improving for a set number of rounds, preventing overfitting:

```python
model = xgb.XGBClassifier(
    n_estimators=1000,
    early_stopping_rounds=50,  # stop if no improvement for 50 rounds
    eval_metric='auc'
)

model.fit(
    X_train, y_train,
    eval_set=[(X_val, y_val)],
    verbose=True
)

print(f"Best iteration: {model.best_iteration}")
print(f"Best score: {model.best_score}")
```

**How it works:**
1. After each boosting round, evaluate on a validation set
2. If the metric does not improve for `early_stopping_rounds` consecutive rounds, stop
3. The model from the **best round** is returned

> [!IMPORTANT]
> Always use a held-out validation set (not the training set) for early stopping. Prevents both underfitting and overfitting.

---

## Q190. How does XGBoost handle missing values?

XGBoost has a **built-in sparsity-aware split finding algorithm**:

1. For each feature with missing values, XGBoost tries assigning missing samples to the **left** or **right** child
2. Whichever direction produces a **better gain** is chosen as the **default direction**
3. At inference time, missing values automatically follow the learned default direction

```python
import numpy as np

# Missing values handled natively — no imputation needed
X_train[5, 2] = np.nan  # XGBoost handles this automatically
model = xgb.XGBClassifier()
model.fit(X_train, y_train)
```

> [!TIP]
> This is a major advantage over scikit-learn's GradientBoostingClassifier, which requires explicit imputation before training.

---

## Q191. How does scale_pos_weight handle class imbalance?

`scale_pos_weight` balances positive and negative class weights for **imbalanced binary classification**:

```
scale_pos_weight = count(negative) / count(positive)
```

```python
import numpy as np

neg = np.sum(y_train == 0)
pos = np.sum(y_train == 1)
ratio = neg / pos

model = xgb.XGBClassifier(scale_pos_weight=ratio)
model.fit(X_train, y_train)
```

**Effect:** Multiplies the gradient and Hessian of positive class samples by `scale_pos_weight`, making them matter more in the optimization.

| Scenario | Recommended `scale_pos_weight` |
|---|---|
| Balanced (50/50) | 1 |
| 10:1 imbalance | 10 |
| 100:1 imbalance | 100 |

> [!NOTE]
> For multi-class imbalance, use `sample_weight` in `fit()` instead, or resample your data.

---

## Q192. What is XGBoost feature importance?

XGBoost provides **three types of feature importance**:

| Type | Description |
|---|---|
| **weight** | Number of times a feature is used to split across all trees |
| **gain** | Average gain in objective function when feature is used to split |
| **cover** | Average number of samples affected by splits on this feature |

```python
import matplotlib.pyplot as plt
from xgboost import plot_importance

# Default is 'weight'
plot_importance(model, importance_type='gain')
plt.show()

# As a dictionary
importance = model.get_booster().get_score(importance_type='gain')
print(sorted(importance.items(), key=lambda x: x[1], reverse=True))
```

> [!TIP]
> `gain` is generally the most informative metric, as it reflects how much each feature contributes to reducing the loss.

---

## Q193. Why is XGBoost computationally efficient?

XGBoost is optimized at multiple levels:

1. **Parallel split finding** — candidate splits are evaluated in parallel using pre-sorted data
2. **Approximate split finding** — uses quantile sketches instead of checking all thresholds
3. **Cache-aware access** — data is stored in column-major format (CSC) for efficient access
4. **Block structure** — data blocks are pre-sorted and cached to reduce I/O
5. **Sparsity handling** — zero/missing values are skipped efficiently
6. **Out-of-core computing** — can handle data larger than RAM using block compression
7. **GPU support** — `tree_method='gpu_hist'` for GPU-accelerated training

```python
# GPU-accelerated training
model = xgb.XGBClassifier(
    tree_method='hist',       # fast histogram algorithm
    device='cuda'             # use GPU
)

# Histogram-based (faster, approximate)
model = xgb.XGBClassifier(tree_method='hist')
```

> [!NOTE]
> `tree_method='hist'` (histogram-based) is the recommended method for large datasets — it's orders of magnitude faster than the exact method.

---

## Q194. What is the difference between XGBoost and Random Forest?

| Feature | XGBoost | Random Forest |
|---|---|---|
| **Learning type** | Boosting (sequential) | Bagging (parallel) |
| **Tree building** | Trees correct previous errors | Trees are independent |
| **Bias-variance** | Reduces both bias and variance | Primarily reduces variance |
| **Training speed** | Slower (sequential) | Faster (parallel) |
| **Overfitting risk** | Higher (needs regularization) | Lower (naturally regularized) |
| **Hyperparameter sensitivity** | High | Low |
| **Missing values** | Built-in handling | Requires imputation (sklearn) |
| **Typical performance** | Often better on tabular data | More robust out-of-the-box |
| **Interpretability** | Moderate | Moderate |

```python
from sklearn.ensemble import RandomForestClassifier
import xgboost as xgb

rf = RandomForestClassifier(n_estimators=100)
xgb_model = xgb.XGBClassifier(n_estimators=100)

# Random Forest: good baseline, less tuning
# XGBoost: often better ceiling, needs more tuning
```

> [!TIP]
> Start with Random Forest as a baseline. If you need better performance and are willing to tune, move to XGBoost.
