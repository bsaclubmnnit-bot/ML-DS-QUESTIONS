# Section 21: Bias and Variance

---

## Q251. What is bias?

**Bias** is the error introduced by approximating a real-world problem (which may be complex) with a simplified model.

- It measures how far off the model's **average prediction** is from the true value.
- High bias → model makes strong, incorrect assumptions about the data.
- Mathematically: `Bias² = (E[ŷ] - y)²`

**Example:** Using a linear model to fit a quadratic relationship — the model is systematically wrong.

```python
# High bias example: underpowered model
from sklearn.linear_model import LinearRegression
model = LinearRegression()  # too simple for a non-linear problem
```

> **Key insight:** Bias is a property of the model's structure, not a specific training run.

---

## Q252. What is variance?

**Variance** is the model's sensitivity to small fluctuations in the training data.

- It measures how much the model's predictions **change across different training sets**.
- High variance → model learns noise in training data and doesn't generalize.
- Mathematically: `Variance = E[(ŷ - E[ŷ])²]`

**Example:** A deep decision tree trained on different random subsets of data produces very different predictions for the same input.

```python
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier(max_depth=None)  # high variance — no pruning
```

> **Key insight:** Variance reflects instability in learning — different data → very different model.

---

## Q253. What is high bias?

**High bias** occurs when a model is **too simple** to capture the underlying patterns in the data.

**Symptoms:**
- High training error
- High test error (similar to training error)
- Model performs poorly on both seen and unseen data

**Causes:**
- Too few features
- Model is too simple (e.g., linear model for non-linear data)
- Too much regularization

**Indicators:**
| Metric | High Bias |
|--------|-----------|
| Training Error | High |
| Validation Error | High |
| Gap (Val - Train) | Small |

---

## Q254. What is high variance?

**High variance** occurs when a model is **too complex** and memorizes the training data, including noise.

**Symptoms:**
- Very low training error
- High test/validation error
- Large gap between training and validation performance

**Causes:**
- Too many features / overly complex model
- Too little training data
- Insufficient regularization

**Indicators:**
| Metric | High Variance |
|--------|---------------|
| Training Error | Low |
| Validation Error | High |
| Gap (Val - Train) | Large |

---

## Q255. What is underfitting?

**Underfitting** is when a model is **too simple** to learn the underlying structure of the data — it performs poorly on both training and test sets.

- Direct result of **high bias**
- The model fails to capture important patterns

**Signs:**
- Low training accuracy
- Low test accuracy
- Learning curve plateaus at high error early

**Example:**
```python
# Fitting a line to clearly non-linear data
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1],[2],[3],[4],[5]])
y = np.array([1, 4, 9, 16, 25])  # quadratic relationship

model = LinearRegression().fit(X, y)
print(model.score(X, y))  # R² will be low — underfitting
```

**Fix:** Use a more complex model, add features, or reduce regularization.

---

## Q256. What is overfitting?

**Overfitting** is when a model **memorizes the training data**, including its noise and outliers, and fails to generalize to new data.

- Direct result of **high variance**
- The model is too closely fitted to the training examples

**Signs:**
- Very high training accuracy
- Low test/validation accuracy
- Big gap between train and test performance

**Example:**
```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split

X, y = make_classification(n_samples=200, random_state=42)
X_train, X_test, y_train, y_test = train_test_split(X, y)

model = DecisionTreeClassifier(max_depth=None)  # no limit — overfits
model.fit(X_train, y_train)

print("Train:", model.score(X_train, y_train))  # ~1.0
print("Test:", model.score(X_test, y_test))      # much lower
```

**Fix:** Regularization, more data, pruning, dropout, cross-validation.

---

## Q257. How can you reduce high bias?

High bias = model too simple → **increase model complexity**.

**Strategies:**

1. **Use a more complex model** — deeper tree, more layers, higher-degree polynomial
2. **Add more features** — feature engineering, polynomial features
3. **Reduce regularization** — lower λ in Ridge/Lasso
4. **Train longer** — more epochs for neural networks
5. **Use a different algorithm** — switch from linear to tree-based or neural network

```python
# Reduce bias: increase polynomial degree
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.linear_model import LinearRegression

model = make_pipeline(PolynomialFeatures(degree=3), LinearRegression())
model.fit(X_train, y_train)
```

> **Rule of thumb:** If both training and validation error are high → reduce bias.

---

## Q258. How can you reduce high variance?

High variance = model too complex → **constrain or regularize the model**.

**Strategies:**

1. **Get more training data** — most effective solution
2. **Apply regularization** — L1 (Lasso), L2 (Ridge), Dropout
3. **Reduce model complexity** — fewer layers, shallower trees, pruning
4. **Use cross-validation** — choose model with best CV score
5. **Feature selection** — remove irrelevant/noisy features
6. **Ensemble methods** — Bagging (Random Forest) averages out variance
7. **Early stopping** — stop training before overfitting in neural networks
8. **Data augmentation** — artificially expand training data

```python
from sklearn.linear_model import Ridge

# L2 regularization reduces variance
model = Ridge(alpha=1.0)  # higher alpha = more regularization
model.fit(X_train, y_train)
```

> **Rule of thumb:** If training error is low but validation error is high → reduce variance.
