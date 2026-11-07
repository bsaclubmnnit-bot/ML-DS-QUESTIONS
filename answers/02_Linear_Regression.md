# Section 2: Linear Regression

## Q16. What is Linear Regression?

**Linear Regression** is a supervised learning algorithm that models the relationship between one or more input features `X` and a continuous output `y` by fitting a **linear equation** to the data.

**Model form:**
```
ŷ = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ
```
Or in vector form: `ŷ = Xθ`

Where:
- `θ₀` = intercept (bias)
- `θ₁...θₙ` = coefficients (weights) for each feature
- `ŷ` = predicted output

**Goal:** Find the parameters `θ` that minimize the sum of squared differences between predicted and actual values.

```python
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1], [2], [3], [4], [5]])
y = np.array([2.1, 3.9, 6.2, 7.8, 10.1])

model = LinearRegression()
model.fit(X, y)

print(f"Intercept: {model.intercept_:.2f}")   # θ₀
print(f"Coefficient: {model.coef_[0]:.2f}")   # θ₁
print(f"Prediction for x=6: {model.predict([[6]])[0]:.2f}")
```

**Use cases:** House price prediction, salary estimation, demand forecasting, any continuous value prediction.

---

## Q17. What assumptions does Linear Regression make?

Linear Regression relies on several key assumptions. Violations can lead to biased or inefficient estimates.

1. **Linearity:** The relationship between features and target is linear.
   - Check: Scatter plots, residual vs. fitted plots

2. **Independence:** Observations are independent of each other.
   - Violated in: Time series data (autocorrelation)

3. **Homoscedasticity:** The variance of residuals is constant across all levels of the predictor (constant error variance).
   - Check: Residuals vs. fitted plot — should show no pattern

4. **Normality of residuals:** Residuals are approximately normally distributed (important for inference, less so for prediction).
   - Check: Q-Q plot, Shapiro-Wilk test

5. **No multicollinearity:** Features are not highly correlated with each other.
   - Check: Correlation matrix, Variance Inflation Factor (VIF)

6. **No endogeneity:** Features are not correlated with the error term.

```python
import statsmodels.api as sm
import matplotlib.pyplot as plt

model = sm.OLS(y, sm.add_constant(X)).fit()
residuals = model.resid
fitted = model.fittedvalues

# Residuals vs Fitted plot
plt.scatter(fitted, residuals)
plt.axhline(0, color='r', linestyle='--')
plt.xlabel('Fitted Values'); plt.ylabel('Residuals')
plt.title('Residuals vs Fitted')
plt.show()

# Q-Q plot for normality
sm.qqplot(residuals, line='s')
plt.show()
```

---

## Q18. What is simple Linear Regression?

**Simple Linear Regression** involves exactly **one independent variable (feature)** predicting one dependent variable (target).

**Equation:**
```
ŷ = θ₀ + θ₁x
```

Where:
- `θ₀` = y-intercept (value of ŷ when x = 0)
- `θ₁` = slope (change in ŷ for a one-unit increase in x)

**Closed-form solution:**
```
θ₁ = Σ(xᵢ - x̄)(yᵢ - ȳ) / Σ(xᵢ - x̄)²
θ₀ = ȳ - θ₁x̄
```

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Single feature
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([3, 5, 4, 7, 9])

model = LinearRegression()
model.fit(X, y)

x_line = np.linspace(1, 5, 100).reshape(-1, 1)
plt.scatter(X, y, color='blue', label='Data')
plt.plot(x_line, model.predict(x_line), color='red', label='Regression line')
plt.xlabel('x'); plt.ylabel('y')
plt.legend()
plt.title(f'y = {model.intercept_:.2f} + {model.coef_[0]:.2f}x')
plt.show()
```

Simple linear regression is the foundation of all regression models and is easy to visualize and interpret.

---

## Q19. What is multiple Linear Regression?

**Multiple Linear Regression** uses **two or more independent variables** (features) to predict a continuous target variable.

**Equation:**
```
ŷ = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ
```

Or in matrix form:
```
ŷ = Xθ
```

Where `X` is the design matrix (with a column of 1s for the intercept).

```python
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.datasets import make_regression

# Multiple features
X, y = make_regression(n_samples=200, n_features=3, noise=10, random_state=42)

model = LinearRegression()
model.fit(X, y)

print("Intercept:", model.intercept_)
print("Coefficients:", model.coef_)
# Coefficient θⱼ = change in ŷ for 1-unit increase in xⱼ, holding others constant
```

**Interpreting coefficients:** Each coefficient `θⱼ` represents the **partial effect** of feature `xⱼ` on `y`, holding all other features constant (ceteris paribus).

**Challenges over simple LR:**
- Multicollinearity between features
- Harder to visualize
- Risk of including irrelevant features

---

## Q20. What is Ordinary Least Squares?

**Ordinary Least Squares (OLS)** is the standard method for estimating the parameters of a linear regression model by **minimizing the sum of squared residuals**.

**Objective:**
```
Minimize: RSS = Σᵢ (yᵢ - ŷᵢ)² = Σᵢ (yᵢ - θᵀxᵢ)²
```

**Closed-form (Normal Equation) solution:**
```
θ* = (XᵀX)⁻¹ Xᵀy
```

Where `X` is the `(n × p)` design matrix.

```python
import numpy as np

# Manual OLS implementation
X = np.column_stack([np.ones(len(X_raw)), X_raw])  # Add intercept column
theta = np.linalg.inv(X.T @ X) @ X.T @ y
print("OLS Parameters:", theta)
```

**Properties of OLS estimators (Gauss-Markov theorem):**
When the linear regression assumptions hold, OLS is **BLUE** — **Best Linear Unbiased Estimator**:
- **Unbiased:** `E[θ̂] = θ`
- **Best:** Minimum variance among all linear unbiased estimators

**Limitation:** The Normal Equation requires computing `(XᵀX)⁻¹`, which is `O(p³)` — computationally expensive for large numbers of features. Gradient descent is preferred in that case.

---

## Q21. Why are squared errors used?

Squared errors are preferred over other error forms for several reasons:

1. **Mathematical convenience:** Squaring makes the loss function **differentiable everywhere** (unlike absolute value which has no derivative at 0), enabling gradient-based optimization.

2. **Closed-form solution:** MSE leads to the Normal Equation `θ = (XᵀX)⁻¹Xᵀy` — an exact analytical solution.

3. **Penalizes large errors more:** Squaring amplifies large mistakes, which is often desirable (a prediction off by 10 is much worse than one off by 1, and squared errors reflect this: 100 vs 1).

4. **Connection to MLE:** Minimizing squared error is equivalent to **Maximum Likelihood Estimation** when residuals follow a Normal (Gaussian) distribution:
   ```
   If ε ~ N(0, σ²), then MLE of θ = OLS solution
   ```

5. **Convex loss surface:** MSE produces a convex optimization landscape with a single global minimum — gradient descent is guaranteed to converge.

**Trade-off:** Squared errors are **sensitive to outliers** (since large errors get squared). In that case, MAE or Huber loss may be preferred.

---

## Q22. What is the Mean Squared Error loss?

**Mean Squared Error (MSE)** is the average of the squared differences between predicted and actual values.

**Formula:**
```
MSE = (1/n) · Σᵢ (yᵢ - ŷᵢ)²
```

**Properties:**
- Always non-negative; MSE = 0 means perfect predictions
- Units are squared units of the target (e.g., if y is in dollars, MSE is in dollars²)
- **Sensitive to outliers** (large errors are squared and dominate)
- Differentiable everywhere → suitable for gradient descent

```python
import numpy as np
from sklearn.metrics import mean_squared_error

y_true = np.array([3, -0.5, 2, 7])
y_pred = np.array([2.5, 0.0, 2, 8])

# Manual calculation
mse_manual = np.mean((y_true - y_pred) ** 2)
print(f"MSE (manual): {mse_manual:.4f}")

# Sklearn
mse_sklearn = mean_squared_error(y_true, y_pred)
print(f"MSE (sklearn): {mse_sklearn:.4f}")
```

**Gradient of MSE w.r.t. θ:**
```
∂MSE/∂θ = (-2/n) · Xᵀ(y - Xθ)
```

Setting to zero gives the Normal Equation for OLS.

---

## Q23. What is gradient descent?

**Gradient Descent** is an iterative optimization algorithm used to **minimize a loss function** by updating model parameters in the direction of the **negative gradient**.

**Intuition:** Imagine standing on a hilly landscape (the loss surface) and taking steps downhill — gradient descent finds the lowest point (minimum).

**Update rule:**
```
θ := θ - α · ∇_θ L(θ)
```

Where:
- `α` = learning rate (step size)
- `∇_θ L(θ)` = gradient of loss w.r.t. parameters

**For MSE loss in Linear Regression:**
```
θ := θ - (α/n) · Xᵀ(Xθ - y)
```

```python
import numpy as np

def gradient_descent(X, y, lr=0.01, epochs=1000):
    n, p = X.shape
    theta = np.zeros(p)

    for _ in range(epochs):
        y_pred = X @ theta
        gradient = (1/n) * X.T @ (y_pred - y)
        theta -= lr * gradient

    return theta

# Add bias column
X_b = np.column_stack([np.ones(len(X)), X])
theta_gd = gradient_descent(X_b, y, lr=0.01, epochs=1000)
```

**Hyperparameters:**
- **Learning rate (α):** Too small → slow convergence; too large → divergence
- **Epochs:** Number of full passes through the data

---

## Q24. What is stochastic gradient descent?

**Stochastic Gradient Descent (SGD)** updates model parameters using the gradient computed from **one randomly selected training sample** at a time.

**Update rule:**
```
θ := θ - α · ∇_θ L(θ; xᵢ, yᵢ)   (for one random sample i)
```

**vs. Batch Gradient Descent:**
| Aspect | Batch GD | SGD |
|--------|----------|-----|
| Gradient computed on | All n samples | 1 sample |
| Update frequency | Once per epoch | n times per epoch |
| Convergence | Smooth, stable | Noisy, oscillating |
| Speed per epoch | Slow | Fast |
| Memory | High | Low |

**Advantages of SGD:**
- Much faster for large datasets
- Noisy updates help escape local minima
- Can do online learning (update with new data as it arrives)

**Disadvantages:**
- Noisy updates → doesn't converge to exact minimum, oscillates around it
- Requires learning rate scheduling (decay over time)

```python
from sklearn.linear_model import SGDRegressor

model = SGDRegressor(loss='squared_error', learning_rate='invscaling',
                     eta0=0.01, max_iter=1000, random_state=42)
model.fit(X_train, y_train)
```

---

## Q25. What is mini-batch gradient descent?

**Mini-batch Gradient Descent** is a compromise between Batch GD and SGD. It computes the gradient on a **small random subset (mini-batch)** of the training data at each step.

**Update rule:**
```
θ := θ - α · (1/B) · Σᵢ∈B ∇_θ L(θ; xᵢ, yᵢ)
```

Where `B` is the mini-batch size (typically 32, 64, 128, 256).

**Comparison:**
| Method | Batch Size | Gradient Noise | Speed | Stability |
|--------|-----------|----------------|-------|-----------|
| Batch GD | n (all data) | None | Slow | High |
| SGD | 1 | High | Fast | Low |
| Mini-batch GD | B (e.g., 32) | Moderate | Fast | Moderate |

**Why mini-batch is preferred in practice:**
- Leverages vectorized operations (GPU-optimized)
- More stable than SGD, faster than full-batch
- **Standard choice for deep learning**

```python
import numpy as np

def mini_batch_gd(X, y, lr=0.01, epochs=100, batch_size=32):
    n, p = X.shape
    theta = np.zeros(p)

    for epoch in range(epochs):
        indices = np.random.permutation(n)
        for i in range(0, n, batch_size):
            batch_idx = indices[i:i+batch_size]
            X_batch, y_batch = X[batch_idx], y[batch_idx]
            grad = (1/len(batch_idx)) * X_batch.T @ (X_batch @ theta - y_batch)
            theta -= lr * grad
    return theta
```

---

## Q26. What is multicollinearity?

**Multicollinearity** occurs when two or more independent variables (features) in a regression model are **highly correlated** with each other.

**Why it's a problem:**
- Makes it difficult to estimate the **individual effect** of each feature on the target (coefficients become unstable and unreliable)
- **Inflates standard errors** of coefficients → makes hypothesis tests unreliable
- The model predictions remain accurate, but **interpretability suffers**
- Small changes in data can cause large changes in coefficient estimates

**Example:** If `x₁ = income` and `x₂ = annual_salary` are nearly identical, the model can't distinguish their individual effects.

**Types:**
- **Perfect multicollinearity:** `x₁ = a·x₂` (makes `XᵀX` non-invertible → OLS fails)
- **Near-perfect multicollinearity:** High correlation (> 0.8–0.9) between features

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.DataFrame({'x1': [1,2,3,4,5], 'x2': [2,4,6,8,10], 'x3': [1,3,2,5,4]})
corr_matrix = df.corr()

sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
# x1 and x2 have correlation = 1.0 → perfect multicollinearity
```

---

## Q27. How can multicollinearity be detected?

Several methods can detect multicollinearity:

**1. Correlation Matrix / Heatmap**
- Look for feature pairs with `|r| > 0.8`
- Simple but only captures pairwise relationships

**2. Variance Inflation Factor (VIF)**
- Most comprehensive method — detects multicollinearity among multiple features

**3. Eigenvalues of XᵀX**
- Very small eigenvalues indicate near-singular matrix (multicollinearity)
- Condition number = `max_eigenvalue / min_eigenvalue`; if > 30, concern

**4. Coefficient instability**
- Large changes in coefficients when removing/adding a variable

```python
import pandas as pd
import numpy as np
from statsmodels.stats.outliers_influence import variance_inflation_factor

# Create design matrix
X = pd.DataFrame({
    'x1': [1, 2, 3, 4, 5],
    'x2': [2, 4, 6, 8, 10],   # perfectly correlated with x1
    'x3': [1, 3, 2, 5, 4]
})

# Compute VIF for each feature
vif_data = pd.DataFrame()
vif_data['Feature'] = X.columns
vif_data['VIF'] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
print(vif_data)
# VIF for x1 and x2 will be very high (→ inf for perfect collinearity)
```

**Remedies:**
- Remove one of the correlated features
- Use Ridge Regression (handles multicollinearity via L2 penalty)
- Apply PCA to decorrelate features
- Collect more data

---

## Q28. What is VIF?

**Variance Inflation Factor (VIF)** quantifies how much the variance of a regression coefficient is **inflated due to multicollinearity** with other features.

**Formula:**
```
VIF(j) = 1 / (1 - R²_j)
```

Where `R²_j` is the R² from regressing feature `xⱼ` on all other features.

**Interpretation:**
| VIF Value | Interpretation |
|-----------|---------------|
| 1 | No multicollinearity |
| 1 – 5 | Moderate, generally acceptable |
| 5 – 10 | High — investigate |
| > 10 | Severe multicollinearity — action needed |

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
import pandas as pd
import numpy as np

X = pd.DataFrame({
    'sqft': [1000, 1500, 1200, 1800, 2000],
    'rooms': [3, 4, 3, 5, 5],
    'age': [10, 5, 8, 2, 1]
})

vif_df = pd.DataFrame({
    'Feature': X.columns,
    'VIF': [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
})
print(vif_df)
```

**Action when VIF is high:**
- Drop the feature with the highest VIF and recalculate
- Combine correlated features (e.g., average them)
- Use regularization (Ridge penalizes large coefficients caused by multicollinearity)

---

## Q29. How do outliers affect Linear Regression?

Outliers can have a significant and **disproportionate influence** on Linear Regression:

1. **Pull the regression line:** OLS minimizes squared errors, so large deviations get squared, giving outliers massive influence over the coefficient estimates.

2. **Distort coefficient estimates:** A single extreme outlier can change the slope dramatically.

3. **Inflate MSE and reduce R²:** Outliers increase prediction error metrics.

4. **Violate normality assumption:** Extreme outliers cause non-normal residuals.

**Types of influential points:**
- **Outlier:** Unusual y-value (high residual)
- **Leverage point:** Unusual x-value (extreme in feature space)
- **Influential point:** High leverage + high residual (changes model significantly if removed)

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression, HuberRegressor

X = np.array([[1],[2],[3],[4],[5],[20]])  # 20 is an outlier
y = np.array([2, 4, 5, 4, 5, 3])         # outlier has low y

# Standard OLS vs robust regression
ols = LinearRegression().fit(X, y)
huber = HuberRegressor().fit(X, y)

print(f"OLS slope: {ols.coef_[0]:.3f}")
print(f"Huber slope: {huber.coef_[0]:.3f}")
```

**Handling outliers:**
- Detect using: z-score, IQR, Cook's Distance
- Remove if data entry error; otherwise use robust regression (Huber, RANSAC)
- Transform features (log, sqrt) to reduce outlier impact

---

## Q30. What is heteroscedasticity?

**Heteroscedasticity** means the **variance of the residuals (errors) is not constant** across all levels of the independent variables — it changes systematically.

**Example:** Predicting income. For low earners, predictions may be fairly accurate (small errors). For high earners, errors may be much larger. The variance increases with income.

**Problems caused by heteroscedasticity:**
- OLS estimates remain **unbiased** but are **no longer efficient** (minimum variance)
- **Standard errors are incorrect** → hypothesis tests and confidence intervals are invalid
- Predictions may have inconsistent reliability

**Detection:**
- **Residual vs. Fitted plot:** Look for a funnel shape (variance expanding/contracting)
- **Breusch-Pagan test** or **White's test** (formal statistical tests)

```python
import statsmodels.api as sm
from statsmodels.stats.diagnostic import het_breuschpagan

model = sm.OLS(y, sm.add_constant(X)).fit()
_, p_value, _, _ = het_breuschpagan(model.resid, model.model.exog)
print(f"Breusch-Pagan p-value: {p_value:.4f}")
# p < 0.05 → evidence of heteroscedasticity
```

**Remedies:**
- Log-transform the target variable: `log(y)`
- Use Weighted Least Squares (WLS)
- Use robust standard errors (`cov_type='HC3'` in statsmodels)

---

## Q31. What is homoscedasticity?

**Homoscedasticity** means the **variance of the residuals (errors) is constant** across all levels of the independent variables.

This is one of the key assumptions of OLS regression. When it holds:
- Residuals are **equally spread** across all fitted values
- Statistical inference (confidence intervals, hypothesis tests) is **valid**
- OLS is the **Best Linear Unbiased Estimator (BLUE)**

**Visual check:** A residuals vs. fitted plot should show a **horizontal band** with **no pattern** — equal spread of residuals across all fitted values.

```python
import matplotlib.pyplot as plt
import statsmodels.api as sm

model = sm.OLS(y, sm.add_constant(X)).fit()

plt.scatter(model.fittedvalues, model.resid, alpha=0.5)
plt.axhline(0, color='red', linestyle='--')
plt.xlabel('Fitted Values')
plt.ylabel('Residuals')
plt.title('Residuals vs Fitted (Homoscedastic if random scatter)')
plt.show()
```

**Homoscedastic residuals:** Scatter plot shows points randomly scattered in a horizontal band.
**Heteroscedastic residuals:** Scatter plot shows a funnel or other systematic pattern.

---

## Q32. What is R-squared?

**R-squared (R², Coefficient of Determination)** measures the **proportion of variance in the target variable explained by the model**.

**Formula:**
```
R² = 1 - (SS_res / SS_tot)

SS_res = Σ(yᵢ - ŷᵢ)²    (residual sum of squares)
SS_tot = Σ(yᵢ - ȳ)²     (total sum of squares)
```

**Interpretation:**
| R² | Interpretation |
|----|---------------|
| 1.0 | Perfect fit — model explains all variance |
| 0.8 | Model explains 80% of variance |
| 0.0 | Model is no better than predicting the mean |
| < 0 | Model is worse than predicting the mean |

```python
from sklearn.metrics import r2_score
import numpy as np

y_true = np.array([3, -0.5, 2, 7, 4.2])
y_pred = np.array([2.5, 0.0, 2, 8, 4.0])

r2 = r2_score(y_true, y_pred)
print(f"R²: {r2:.4f}")
```

**Limitations:**
- R² **always increases** when adding more features, even if they're irrelevant (use Adjusted R² instead)
- A high R² doesn't guarantee a good model (could be overfitting)
- A low R² doesn't mean the model is useless (e.g., in noisy domains like finance, R²=0.1 can be meaningful)

---

## Q33. What is Adjusted R-squared?

**Adjusted R²** is a modified version of R² that **penalizes the addition of features that don't improve the model**, adjusting for the number of predictors.

**Formula:**
```
Adjusted R² = 1 - [(1 - R²)(n - 1) / (n - p - 1)]
```

Where:
- `n` = number of observations
- `p` = number of predictor features

**Why it's better than R²:**
- R² can **only increase** (or stay the same) when features are added, even noise features
- Adjusted R² **increases only if the new feature improves the model more than expected by chance**
- Adjusted R² can **decrease** if an irrelevant feature is added

```python
def adjusted_r2(r2, n, p):
    return 1 - (1 - r2) * (n - 1) / (n - p - 1)

import numpy as np
from sklearn.metrics import r2_score

y_true = np.array([3, 5, 2, 8, 6])
y_pred = np.array([2.8, 5.2, 2.1, 7.9, 6.1])

r2 = r2_score(y_true, y_pred)
n, p = 5, 2

adj_r2 = adjusted_r2(r2, n, p)
print(f"R²: {r2:.4f}")
print(f"Adjusted R²: {adj_r2:.4f}")
```

> **Rule of thumb:** Use Adjusted R² when comparing models with different numbers of features.

---

## Q34. How do residual plots help?

**Residual plots** are diagnostic tools that help assess whether the **linear regression assumptions are met** and identify potential issues.

**Common residual plots:**

**1. Residuals vs. Fitted Values**
- **Good:** Random scatter around y=0 (horizontal band)
- **Bad:** Funnel shape → heteroscedasticity; curve → non-linearity

**2. Normal Q-Q Plot**
- **Good:** Points follow the diagonal line
- **Bad:** S-curve or heavy tails → residuals not normally distributed

**3. Scale-Location Plot**
- Check for homoscedasticity; should be flat with random scatter

**4. Residuals vs. Leverage**
- Identifies influential outliers (Cook's Distance)

```python
import statsmodels.api as sm
import matplotlib.pyplot as plt

model = sm.OLS(y, sm.add_constant(X)).fit()

fig, axes = plt.subplots(1, 2, figsize=(12, 4))

# Residuals vs Fitted
axes[0].scatter(model.fittedvalues, model.resid, alpha=0.5)
axes[0].axhline(0, color='red', linestyle='--')
axes[0].set_xlabel('Fitted'); axes[0].set_ylabel('Residuals')
axes[0].set_title('Residuals vs Fitted')

# Q-Q plot
sm.qqplot(model.resid, line='s', ax=axes[1])
axes[1].set_title('Q-Q Plot')

plt.tight_layout()
plt.show()
```

---

## Q35. How do you handle non-linear relationships?

When the relationship between features and target is non-linear, several strategies can be applied:

**1. Polynomial Features**
```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.linear_model import LinearRegression

# Adds x, x², x³, x₁x₂, etc.
model = make_pipeline(PolynomialFeatures(degree=2), LinearRegression())
model.fit(X_train, y_train)
```

**2. Feature Transformation**
- Log transform: `log(x)` for exponential relationships
- Square root: `√x` for diminishing returns
- Inverse: `1/x` for hyperbolic relationships

```python
import numpy as np
X_log = np.log1p(X)       # log(1+x) for non-negative x
X_sqrt = np.sqrt(X)
```

**3. Interaction Terms**
```python
X['x1_x2'] = X['x1'] * X['x2']
```

**4. Splines / Piecewise Linear Models**
- Fit different linear segments for different ranges of x

**5. Use Non-linear Algorithms**
- Decision Trees, Random Forests, Gradient Boosting (XGBoost, LightGBM)
- Support Vector Regression with RBF kernel
- Neural Networks

**6. Generalized Additive Models (GAMs)**
- Model each feature with a flexible smooth function

> **Best practice:** First explore scatter plots and correlation matrices to understand the shape of each feature-target relationship, then choose the appropriate transformation or model.
