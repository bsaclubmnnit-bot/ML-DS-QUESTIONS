# Section 3: Ridge and Lasso Regression

## Q36. Why is regularization needed?

**Regularization** is needed to prevent **overfitting** — the situation where a model learns the training data too well (including noise) and fails to generalize to new data.

**Root causes of overfitting that regularization addresses:**
- **Too many features:** A model with many features has many parameters and can memorize training data
- **Complex models:** High-degree polynomials, deep trees, etc.
- **Limited training data:** With few samples and many features, the model can find spurious patterns

**What regularization does:**
- Adds a **penalty term** to the loss function that discourages large coefficients
- Constrains the model's flexibility, forcing it to learn simpler, more generalizable patterns
- Trades a small increase in bias for a larger decrease in variance → better test performance

**Without regularization (plain OLS):**
- On perfectly collinear features, `(XᵀX)` is singular → no unique solution
- Coefficients can be arbitrarily large, leading to unstable and overfit models

**Regularized objective:**
```
Minimize: Loss(θ) + λ · Penalty(θ)
```

The `λ` parameter controls the trade-off between fitting the data and keeping coefficients small. As `λ → 0`, we approach OLS; as `λ → ∞`, all coefficients are pushed to zero.

---

## Q37. What is Ridge Regression?

**Ridge Regression** (also called **L2 Regularization** or **Tikhonov Regularization**) adds the **sum of squared coefficients** as a penalty to the OLS loss.

**Objective:**
```
Minimize: Σ(yᵢ - ŷᵢ)² + λ · Σⱼ θⱼ²
```

Or in matrix form:
```
Minimize: ||y - Xθ||² + λ||θ||²
```

**Closed-form solution:**
```
θ_ridge = (XᵀX + λI)⁻¹ Xᵀy
```

Adding `λI` ensures the matrix is always invertible — Ridge directly solves the multicollinearity problem.

**Key properties:**
- **Shrinks** all coefficients toward zero, but **never exactly to zero**
- Handles multicollinearity well (distributes weight among correlated features)
- Keeps all features in the model
- The penalty grows quadratically — large coefficients are penalized much more than small ones

```python
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

model = make_pipeline(StandardScaler(), Ridge(alpha=1.0))
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

---

## Q38. What is Lasso Regression?

**Lasso Regression** (Least Absolute Shrinkage and Selection Operator, **L1 Regularization**) adds the **sum of absolute values of coefficients** as a penalty.

**Objective:**
```
Minimize: Σ(yᵢ - ŷᵢ)² + λ · Σⱼ |θⱼ|
```

**Key properties:**
- **Shrinks** some coefficients **exactly to zero** → performs automatic **feature selection**
- Results in a **sparse model** (only a subset of features have non-zero coefficients)
- Especially useful when you believe many features are irrelevant
- Does **not** have a closed-form solution (because `|θ|` is not differentiable at 0); solved with coordinate descent or subgradient methods

```python
from sklearn.linear_model import Lasso
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

model = make_pipeline(StandardScaler(), Lasso(alpha=0.1))
model.fit(X_train, y_train)

# Feature selection: non-zero coefficients
feature_mask = model.named_steps['lasso'].coef_ != 0
selected_features = X_train.columns[feature_mask]
print("Selected features:", selected_features.tolist())
```

---

## Q39. What is the difference between L1 and L2 regularization?

| Aspect | L1 (Lasso) | L2 (Ridge) |
|--------|-----------|-----------|
| Penalty term | `λ·Σ\|θⱼ\|` | `λ·Σθⱼ²` |
| Effect on coefficients | Drives some to **exactly zero** | Shrinks all toward zero, but **never exactly zero** |
| Feature selection | **Yes** (automatic) | No |
| Sparsity | Produces **sparse** models | Dense models |
| Handles multicollinearity | Picks one of correlated features, zeros others | Distributes weight evenly among correlated features |
| Solution | No closed form (subdifferential) | Closed form: `(XᵀX + λI)⁻¹Xᵀy` |
| Geometric intuition | Diamond-shaped constraint → corners at axes | Circular constraint → no corners |
| Best used when | Many irrelevant features exist | All features are relevant; multicollinearity present |

**Geometric intuition:**
- L1: The L1 ball is a **diamond** in 2D. The optimal solution often hits a corner (where one coordinate = 0) → sparsity.
- L2: The L2 ball is a **circle** in 2D. The optimal solution rarely hits an axis → no sparsity.

```python
import numpy as np

# L1 norm (sum of absolutes)
theta = np.array([2.0, -3.0, 0.5])
l1_penalty = np.sum(np.abs(theta))      # = 5.5

# L2 norm squared (sum of squares)
l2_penalty = np.sum(theta ** 2)         # = 13.25
```

---

## Q40. How does Ridge affect coefficients?

Ridge regression **shrinks all coefficients toward zero** proportionally, but **never sets any coefficient exactly to zero**.

**Mathematical insight:**
The Ridge update effectively multiplies each OLS coefficient by a shrinkage factor:
```
θ_ridge_j ≈ θ_OLS_j · (1 / (1 + λ/n))
```
As `λ` increases, coefficients shrink more.

**Effect on correlated features:**
- If `x₁` and `x₂` are perfectly correlated, Ridge distributes the weight **equally** between them rather than arbitrarily assigning it to one.

```python
import numpy as np
from sklearn.linear_model import Ridge, LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_regression

X, y, true_coef = make_regression(n_samples=100, n_features=5,
                                   n_informative=3, noise=10,
                                   coef=True, random_state=42)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

ols = LinearRegression().fit(X_scaled, y)
ridge = Ridge(alpha=10.0).fit(X_scaled, y)

print("OLS Coefficients:", np.round(ols.coef_, 2))
print("Ridge Coefficients (α=10):", np.round(ridge.coef_, 2))
# Ridge coefficients are smaller in magnitude
```

**Key takeaway:** Ridge never fully eliminates a feature — it reduces the influence of less important features but keeps them in the model.

---

## Q41. How does Lasso perform feature selection?

Lasso drives **some coefficients to exactly zero** through the geometry of its L1 penalty, effectively removing those features from the model.

**Mathematical mechanism:**
The L1 penalty's subdifferential at `θ = 0` is the interval `[-λ, λ]`. If the OLS estimate's gradient at `θ = 0` lies within this interval (i.e., the feature doesn't contribute enough), the coordinate descent update sets that coefficient to exactly zero.

**Coordinate descent update for Lasso:**
```
θⱼ = sign(ρⱼ) · max(|ρⱼ| - λ, 0)
```
This is the **soft-thresholding operator** — if `|ρⱼ| < λ`, the coefficient is set to zero.

```python
import numpy as np
from sklearn.linear_model import Lasso
from sklearn.preprocessing import StandardScaler

# Synthetic data with many irrelevant features
np.random.seed(42)
X = np.random.randn(100, 10)
y = 2*X[:,0] + 3*X[:,1] - X[:,2] + np.random.randn(100)*0.5
# Only features 0, 1, 2 matter; rest are noise

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

lasso = Lasso(alpha=0.1)
lasso.fit(X_scaled, y)

print("Lasso Coefficients:")
for i, coef in enumerate(lasso.coef_):
    print(f"  Feature {i}: {coef:.3f} {'✓ selected' if coef != 0 else '✗ zero'}")
```

**Output:** Features 0, 1, 2 will have non-zero coefficients; irrelevant features will be zero.

> This built-in feature selection makes Lasso especially useful when you have high-dimensional data with many irrelevant features.

---

## Q42. What is the regularization parameter?

The **regularization parameter** (commonly denoted `λ` in mathematics or `alpha` in scikit-learn) controls the **strength of the regularization penalty**.

**Role in Ridge:**
```
Objective = MSE + λ · Σθⱼ²
```

**Role in Lasso:**
```
Objective = MSE + λ · Σ|θⱼ|
```

**Effect of λ:**
- **Small λ (→ 0):** Minimal regularization → behaves like OLS (low bias, high variance)
- **Large λ (→ ∞):** Strong regularization → all coefficients → 0 (high bias, low variance)

**Tuning:** The optimal λ is found via **cross-validation** (e.g., `RidgeCV`, `LassoCV` in sklearn).

```python
import numpy as np
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler

X_scaled = StandardScaler().fit_transform(X)

alphas = [0.001, 0.01, 0.1, 1.0, 10.0, 100.0]
for alpha in alphas:
    ridge = Ridge(alpha=alpha).fit(X_scaled, y)
    coef_norm = np.linalg.norm(ridge.coef_)
    print(f"α={alpha:6.3f} | Coefficient L2 norm: {coef_norm:.4f}")
```

> **Note:** scikit-learn uses `alpha` as the regularization parameter; statsmodels uses `alpha`; the mathematical notation typically uses `λ`.

---

## Q43. What happens when regularization is zero?

When `λ = 0`, the regularization term vanishes and the model reduces to **ordinary OLS (Ordinary Least Squares)**:

```
Objective = Σ(yᵢ - ŷᵢ)²  [no penalty]
```

**Consequences:**
- Coefficients are the standard OLS estimates: `θ = (XᵀX)⁻¹Xᵀy`
- **No shrinkage** is applied
- If features are multicollinear, `(XᵀX)` may be singular or near-singular → unstable coefficients
- Higher risk of **overfitting** on small datasets with many features
- Maximum flexibility — model fits training data as closely as possible

```python
from sklearn.linear_model import Ridge

# λ=0 → equivalent to OLS
ridge_zero = Ridge(alpha=0)
ridge_zero.fit(X_scaled, y)

from sklearn.linear_model import LinearRegression
ols = LinearRegression().fit(X_scaled, y)

import numpy as np
print("Ridge (α=0):", np.round(ridge_zero.coef_, 4))
print("OLS:         ", np.round(ols.coef_, 4))
# Should be identical (or very close)
```

> **In practice:** Never set `alpha=0` for Ridge or Lasso in production; if you want OLS, use `LinearRegression()` directly.

---

## Q44. What happens when regularization is very high?

When `λ → ∞`, the regularization penalty dominates the objective function, forcing **all coefficients toward zero**.

**For Ridge (L2):**
- All `θⱼ → 0` (but never exactly zero for finite λ)
- Model predicts approximately the **mean of y** for all inputs
- Extremely high bias, very low variance
- Equivalent to the **null model** (intercept-only)

**For Lasso (L1):**
- All `θⱼ = 0` exactly (for large enough finite λ)
- Same null model behavior

```python
import numpy as np
from sklearn.linear_model import Ridge, Lasso
from sklearn.preprocessing import StandardScaler

X_scaled = StandardScaler().fit_transform(X)

for alpha in [1, 100, 10000, 1e9]:
    ridge = Ridge(alpha=alpha).fit(X_scaled, y)
    print(f"α={alpha:.0e} | Max |coef|: {np.max(np.abs(ridge.coef_)):.6f}")

# Output shows coefficients → 0 as alpha → ∞
```

**Bias-Variance impact:**
- Very high λ → **underfitting** (model is too constrained)
- The model ignores the training data and just predicts the mean

> **The optimal λ lies between 0 and ∞**, balancing fit quality and model simplicity. This is found via cross-validation.

---

## Q45. When would you prefer Ridge over Lasso?

**Prefer Ridge when:**

1. **Most or all features are relevant** — Lasso would zero out some useful features; Ridge keeps all of them with reduced coefficients.

2. **Many correlated features** — Ridge handles multicollinearity by distributing weight evenly; Lasso arbitrarily picks one from a correlated group.

3. **Stable coefficient estimates needed** — Ridge gives smoother, more stable coefficient paths than Lasso.

4. **Prediction accuracy is the primary goal** — In many settings with dense, meaningful features, Ridge achieves lower test error.

5. **p (features) << n (samples)** — With relatively few features, you likely want all of them and just need shrinkage.

**Prefer Lasso when:**
- Many features are suspected to be irrelevant (high-dimensional sparse problems)
- Interpretability requires a small subset of features
- You need automated feature selection

```python
from sklearn.linear_model import RidgeCV, LassoCV
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

# Try both and compare cross-validation scores
ridge_cv = make_pipeline(StandardScaler(), RidgeCV(alphas=[0.1, 1, 10, 100]))
lasso_cv = make_pipeline(StandardScaler(), LassoCV(alphas=[0.001, 0.01, 0.1, 1]))

ridge_cv.fit(X_train, y_train)
lasso_cv.fit(X_train, y_train)

print(f"Ridge CV score: {ridge_cv.score(X_test, y_test):.4f}")
print(f"Lasso CV score: {lasso_cv.score(X_test, y_test):.4f}")
```

---

## Q46. What is Elastic Net?

**Elastic Net** combines **both L1 and L2 regularization** into a single penalty, getting the benefits of both Ridge and Lasso.

**Objective:**
```
Minimize: Σ(yᵢ - ŷᵢ)² + λ₁·Σ|θⱼ| + λ₂·Σθⱼ²
```

In scikit-learn's parameterization:
```
Minimize: (1/2n)·||y - Xθ||² + α·l1_ratio·||θ||₁ + (α/2)·(1-l1_ratio)·||θ||₂²
```

Where:
- `alpha` controls overall regularization strength
- `l1_ratio` (between 0 and 1) controls the mix:
  - `l1_ratio = 1` → pure Lasso
  - `l1_ratio = 0` → pure Ridge
  - `l1_ratio = 0.5` → 50/50 mix

```python
from sklearn.linear_model import ElasticNet, ElasticNetCV
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

# Manual Elastic Net
en = make_pipeline(
    StandardScaler(),
    ElasticNet(alpha=0.1, l1_ratio=0.5)  # equal L1 and L2
)
en.fit(X_train, y_train)

# With CV to find best alpha and l1_ratio
encv = make_pipeline(
    StandardScaler(),
    ElasticNetCV(l1_ratio=[0.1, 0.5, 0.7, 0.9, 1.0],
                 alphas=[0.001, 0.01, 0.1, 1.0],
                 cv=5)
)
encv.fit(X_train, y_train)
print(f"Best alpha: {encv.named_steps['elasticnetcv'].alpha_}")
print(f"Best l1_ratio: {encv.named_steps['elasticnetcv'].l1_ratio_}")
```

---

## Q47. Why is Elastic Net useful for correlated features?

Elastic Net solves a key weakness of Lasso with correlated features:

**Lasso's problem with correlated features:**
- When features are highly correlated, Lasso arbitrarily picks **one** and sets the others to zero
- The selected feature depends on small data variations → unstable
- This is problematic when correlated features all contribute to the target

**Elastic Net's solution:**
- The L2 (Ridge) component creates a **grouping effect**: correlated features are **selected or rejected together**, with similar coefficients
- The L1 component still provides **sparsity** (sets irrelevant features to zero)

**Concrete example:**
- 5 highly correlated gene expression features all related to a disease outcome
- Lasso: picks 1, ignores 4 (even if all 5 matter)
- Elastic Net: keeps all 5 with moderate coefficients → better interpretation and prediction

```python
import numpy as np
from sklearn.linear_model import Lasso, ElasticNet
from sklearn.preprocessing import StandardScaler

np.random.seed(42)
# Create correlated features
x1 = np.random.randn(100)
X = np.column_stack([x1, x1 + 0.01*np.random.randn(100),
                     x1 + 0.01*np.random.randn(100),
                     np.random.randn(100)])  # Last feature is independent
y = 2*x1 + np.random.randn(100)*0.5

X_s = StandardScaler().fit_transform(X)

print("Lasso:", np.round(Lasso(0.05).fit(X_s, y).coef_, 3))
print("ElasticNet:", np.round(ElasticNet(0.05, l1_ratio=0.5).fit(X_s, y).coef_, 3))
# Lasso: one of first three features; ElasticNet: all three share weight
```

---

## Q48. How does regularization affect bias and variance?

Regularization directly controls the **bias-variance tradeoff**:

**As regularization strength (λ) increases:**
- **Bias increases:** The model is forced away from the true function (more constrained)
- **Variance decreases:** Coefficients are more stable, less sensitive to training data variations

**As regularization strength (λ) decreases:**
- **Bias decreases:** Model can fit the data more freely
- **Variance increases:** Model becomes sensitive to training data noise

```
λ = 0         → OLS: Low Bias, High Variance (overfitting risk)
λ = optimal   → Balanced: Minimum Total Error on test data
λ → ∞        → Null model: High Bias, Low Variance (underfitting)
```

**Bias-Variance decomposition:**
```
Expected Test Error = Bias² + Variance + Irreducible Noise
```

```python
import numpy as np
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

alphas = [0, 0.1, 1, 10, 100, 1000]
for alpha in alphas:
    train_errors, test_errors = [], []
    for seed in range(30):
        X_tr, X_te, y_tr, y_te = train_test_split(X, y, test_size=0.3,
                                                    random_state=seed)
        model = Ridge(alpha=alpha).fit(X_tr, y_tr)
        train_errors.append(mean_squared_error(y_tr, model.predict(X_tr)))
        test_errors.append(mean_squared_error(y_te, model.predict(X_te)))

    print(f"α={alpha:5}: Train MSE={np.mean(train_errors):.3f}, "
          f"Test MSE={np.mean(test_errors):.3f}, "
          f"Variance={np.var(test_errors):.3f}")
```

---

## Q49. Should features be scaled before Ridge and Lasso?

**Yes — scaling is essential** before applying Ridge or Lasso regularization.

**Why scaling is required:**

Ridge and Lasso penalize the **magnitude of coefficients**. Without scaling, features with larger numerical ranges will have smaller coefficients (to fit the data), while features with smaller ranges will have larger coefficients. The regularization penalty is then **unfairly applied** based on feature scale, not actual importance.

**Example:**
- Feature 1: `age` (range 0–100) → coefficient ≈ 0.05 (small)
- Feature 2: `income_cents` (range 0–10,000,000) → coefficient ≈ 0.000001 (tiny)

Without scaling, L2 penalty barely touches the income coefficient even if income is unimportant.

**With standardization (mean=0, std=1):**
- All features are on equal footing
- Regularization penalizes equally across features based on relevance

```python
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge, Lasso
from sklearn.pipeline import make_pipeline

# CORRECT: scaling inside pipeline
model = make_pipeline(
    StandardScaler(),   # Scale BEFORE regularization
    Ridge(alpha=1.0)
)
model.fit(X_train, y_train)

# WRONG: scaling outside, or not scaling at all
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)   # Data leakage risk if not in pipeline
X_test_scaled = scaler.transform(X_test)
```

> **Important:** Always use a **Pipeline** to apply scaling — this prevents data leakage by ensuring the scaler is fit only on training data.

---

## Q50. How do you select the best regularization strength?

The optimal regularization strength (lambda/alpha) is selected using **cross-validation** to find the value that minimizes validation error.

**Method 1: Manual Cross-Validation with GridSearch**
```python
from sklearn.model_selection import GridSearchCV
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(StandardScaler(), Ridge())
param_grid = {'ridge__alpha': [0.001, 0.01, 0.1, 1, 10, 100, 1000]}

grid_search = GridSearchCV(pipeline, param_grid, cv=5,
                           scoring='neg_mean_squared_error')
grid_search.fit(X_train, y_train)
print(f"Best alpha: {grid_search.best_params_}")
print(f"Best CV MSE: {-grid_search.best_score_:.4f}")
```

**Method 2: RidgeCV / LassoCV (Efficient built-in CV)**
```python
from sklearn.linear_model import RidgeCV, LassoCV
import numpy as np

alphas = np.logspace(-4, 4, 100)  # 100 values from 0.0001 to 10000

# RidgeCV uses efficient leave-one-out CV
ridge_cv = RidgeCV(alphas=alphas, cv=5)
ridge_cv.fit(X_train_scaled, y_train)
print(f"Best Ridge alpha: {ridge_cv.alpha_:.4f}")

# LassoCV uses coordinate descent for all alphas
lasso_cv = LassoCV(alphas=alphas, cv=5, max_iter=10000)
lasso_cv.fit(X_train_scaled, y_train)
print(f"Best Lasso alpha: {lasso_cv.alpha_:.4f}")
```

**Method 3: Regularization path (coefficient trace plot)**
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import lasso_path

alphas, coefs, _ = lasso_path(X_train_scaled, y_train)

plt.figure(figsize=(10, 4))
for coef in coefs:
    plt.plot(np.log10(alphas), coef)
plt.xlabel('log10(alpha)'); plt.ylabel('Coefficient value')
plt.title('Lasso Regularization Path')
plt.axvline(x=np.log10(lasso_cv.alpha_), color='r', linestyle='--',
            label='Optimal alpha')
plt.legend(); plt.show()
```

> **Best practice:** Use logarithmically spaced alpha values (`np.logspace`) and choose based on cross-validated MSE, not training MSE.
