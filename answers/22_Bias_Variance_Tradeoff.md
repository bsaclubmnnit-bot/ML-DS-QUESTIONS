# Section 22: Bias-Variance Tradeoff

---

## Q259. What is the bias-variance tradeoff?

The **bias-variance tradeoff** is the fundamental tension in machine learning between a model being too simple (high bias) and too complex (high variance).

The total expected prediction error can be decomposed as:

```
Total Error = Bias² + Variance + Irreducible Noise
```

- **Bias²**: error from wrong assumptions (systematic error)
- **Variance**: error from sensitivity to training data fluctuations
- **Irreducible Noise**: inherent randomness in the data (cannot be reduced)

**The tradeoff:**
- Decreasing bias (more complex model) → tends to increase variance
- Decreasing variance (simpler model) → tends to increase bias

```
Error
  |  \         /
  |   \  Total /
  |    \/___  /
  |    /    \/
  |Var/   Bias²
  |__/_________ Model Complexity →
```

> **Goal:** Find the sweet spot that minimizes total error.

---

## Q260. Why does the tradeoff occur?

The tradeoff occurs because of the **competing demands** of fitting training data vs. generalizing to new data.

**Fundamental reason:**
- A complex model has many degrees of freedom → it can fit training data very well (low bias) BUT different training sets yield very different models (high variance).
- A simple model has few degrees of freedom → stable across datasets (low variance) BUT cannot fit complex patterns (high bias).

**Analogy:**
- **High bias model:** Uses the same answer for every question — consistent but often wrong.
- **High variance model:** Changes answer based on who's asking — flexible but unreliable.

**Mathematical intuition:**
```
E[(y - ŷ)²] = [E[ŷ] - y]² + E[(ŷ - E[ŷ])²] + σ²
              = Bias²        + Variance          + Noise
```

As you increase model complexity, the bias term decreases monotonically, but the variance term increases — their sum has a minimum at the optimal complexity level.

---

## Q261. How does regularization affect it?

**Regularization** adds a penalty to the loss function to constrain model complexity, directly managing the bias-variance tradeoff.

**Effect:**
| Regularization | Bias | Variance |
|----------------|------|----------|
| None | Lower | Higher |
| Moderate (optimal λ) | Balanced | Balanced |
| Too much | Higher | Lower |

**L2 (Ridge) Regularization:**
```python
from sklearn.linear_model import Ridge
import numpy as np

# Low alpha → low bias, high variance
model_low = Ridge(alpha=0.001)

# High alpha → high bias, low variance
model_high = Ridge(alpha=100.0)

# Optimal alpha found via cross-validation
from sklearn.linear_model import RidgeCV
model_cv = RidgeCV(alphas=[0.001, 0.01, 0.1, 1.0, 10.0, 100.0], cv=5)
```

**L1 (Lasso) Regularization:**
```python
from sklearn.linear_model import Lasso
model = Lasso(alpha=0.1)  # also performs feature selection → reduces variance
```

**Key insight:** Regularization introduces controlled bias to significantly reduce variance, often yielding better generalization.

---

## Q262. How does bagging affect variance?

**Bagging** (Bootstrap Aggregating) directly **reduces variance** with minimal impact on bias.

**How it works:**
1. Sample multiple bootstrap datasets from training data
2. Train a separate model on each
3. Aggregate predictions (average for regression, majority vote for classification)

**Why it reduces variance:**
- Individual models have high variance
- Averaging independent estimators reduces variance by a factor of `1/n` (if uncorrelated)
- `Var(mean of n models) ≈ Var(single model) / n`

```python
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier

# High-variance base learner
base = DecisionTreeClassifier(max_depth=None)

# Bagging reduces variance
model = BaggingClassifier(estimator=base, n_estimators=100, random_state=42)
model.fit(X_train, y_train)
```

**Random Forest = Bagging + feature randomness** — further decorrelates trees → more variance reduction.

> **Key point:** Bagging doesn't help much with high-bias models; base learners should have low bias.

---

## Q263. How does boosting affect bias?

**Boosting** primarily **reduces bias** by sequentially fitting models to correct the errors of previous ones.

**How it works:**
1. Train a weak learner (typically shallow tree)
2. Identify misclassified / high-error samples
3. Train next learner focused on those errors
4. Combine all learners with weighted voting

**Why it reduces bias:**
- Weak learners individually have high bias
- Sequential correction forces the ensemble to learn complex patterns
- The final model achieves very low training error → low bias

```python
from sklearn.ensemble import GradientBoostingClassifier, AdaBoostClassifier

# AdaBoost — reweights misclassified samples
ada = AdaBoostClassifier(n_estimators=100, learning_rate=0.1)

# Gradient Boosting — fits residuals
gb = GradientBoostingClassifier(n_estimators=100, max_depth=3, learning_rate=0.1)
gb.fit(X_train, y_train)
```

**Tradeoff:** Boosting can **increase variance** if overfitted (too many estimators, too deep trees). Regularization via learning rate and subsampling helps.

| Method | Primary Effect | Secondary Effect |
|--------|---------------|-----------------|
| Bagging | ↓ Variance | Minimal bias change |
| Boosting | ↓ Bias | Possible ↑ variance |

---

## Q264. How do learning curves diagnose bias and variance?

**Learning curves** plot training and validation error as a function of training set size — they reveal whether a model suffers from bias, variance, or both.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import learning_curve

def plot_learning_curve(model, X, y):
    train_sizes, train_scores, val_scores = learning_curve(
        model, X, y, cv=5,
        train_sizes=np.linspace(0.1, 1.0, 10),
        scoring='accuracy'
    )
    
    train_mean = np.mean(train_scores, axis=1)
    val_mean   = np.mean(val_scores, axis=1)
    
    plt.plot(train_sizes, train_mean, label='Training Score')
    plt.plot(train_sizes, val_mean,   label='Validation Score')
    plt.xlabel('Training Set Size')
    plt.ylabel('Score')
    plt.legend()
    plt.show()
```

**Diagnosis patterns:**

| Pattern | Interpretation |
|---------|----------------|
| Both curves converge at **low score** | **High Bias** — model too simple |
| Training score high, validation score low, **large gap** | **High Variance** — model overfitting |
| Both curves converge at **high score** | Good fit — balanced bias-variance |
| Validation curve still rising with more data | May benefit from more training data |

```
High Bias (Underfitting):          High Variance (Overfitting):
  Score                              Score
  |---train------                    |---train------
  |   val  ------                    |              
  |                                  |   val  ------
  |_____________ Data Size           |_____________ Data Size
  (gap small, both low)              (gap large, train high val low)
```

> **Practical use:** If high bias → try more complex model. If high variance → get more data or regularize.
