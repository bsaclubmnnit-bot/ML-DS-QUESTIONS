# Section 13: AdaBoost and Gradient Boosting

---

## Q169. What is AdaBoost?

**AdaBoost (Adaptive Boosting)** is an ensemble learning algorithm that combines multiple **weak learners** (typically decision stumps) into a single strong classifier.

**Key ideas:**
- Each weak learner is trained sequentially
- Misclassified samples receive **higher weights** in the next round
- Final prediction is a **weighted majority vote** of all weak learners

```python
from sklearn.ensemble import AdaBoostClassifier
from sklearn.tree import DecisionTreeClassifier

model = AdaBoostClassifier(
    estimator=DecisionTreeClassifier(max_depth=1),
    n_estimators=100,
    learning_rate=1.0
)
model.fit(X_train, y_train)
```

> [!NOTE]
> AdaBoost was one of the first practically successful boosting algorithms, introduced by Freund & Schapire (1995).

---

## Q170. How does AdaBoost train models sequentially?

AdaBoost trains weak learners one after another, each focusing on the **mistakes of the previous one**:

1. Initialize equal sample weights: `w_i = 1/N`
2. Train a weak learner on the weighted dataset
3. Compute the learner's weighted error
4. Calculate the learner's **importance (alpha)**
5. **Update sample weights** — misclassified samples get higher weights
6. Normalize weights so they sum to 1
7. Repeat steps 2–6 for `n_estimators` rounds
8. Final prediction = weighted sum of all weak learner predictions

```
Final(x) = sign( Σ αₜ · hₜ(x) )
```

Where `αₜ` is the weight of learner `t` and `hₜ(x)` is its prediction.

---

## Q171. How are sample weights updated?

After each round, sample weights are updated using the formula:

**For misclassified sample i:**
```
w_i ← w_i · exp(αₜ)
```

**For correctly classified sample i:**
```
w_i ← w_i · exp(-αₜ)
```

Then all weights are **normalized** to sum to 1.

Where:
```
αₜ = 0.5 · ln((1 - εₜ) / εₜ)
```
- `εₜ` = weighted error rate of learner `t`
- Higher `αₜ` → learner was more accurate → misclassified samples get even larger weight bump

```python
import numpy as np

# Example weight update (simplified)
alpha = 0.5 * np.log((1 - error) / error)
weights[misclassified] *= np.exp(alpha)
weights[correct] *= np.exp(-alpha)
weights /= weights.sum()  # normalize
```

---

## Q172. Why are misclassified samples given more weight?

The philosophy is **"focus on your mistakes"**:

- If a sample was misclassified, the next learner should **pay more attention** to it
- By increasing its weight, the next weak learner is effectively **penalized more** for getting it wrong
- This forces successive learners to specialize in **hard-to-classify regions**
- Over many rounds, the ensemble covers the entire feature space more thoroughly

> [!TIP]
> This adaptive reweighting is what makes AdaBoost fundamentally different from Bagging — each learner is not independent but builds on the errors of its predecessors.

---

## Q173. What is a decision stump?

A **decision stump** is a decision tree with **depth = 1** — it makes exactly **one split** on one feature.

```
         [Feature X ≤ threshold]
          /                    \
       Yes                     No
    Class A                 Class B
```

**Properties:**
- Very weak learner (slightly better than random guessing)
- Low variance, high bias individually
- Fast to train
- Default base estimator for AdaBoost

```python
from sklearn.tree import DecisionTreeClassifier

stump = DecisionTreeClassifier(max_depth=1)
stump.fit(X_train, y_train)
```

> [!NOTE]
> A stump can only create one linear decision boundary, which is why many of them are needed to model complex patterns.

---

## Q174. Why is AdaBoost sensitive to outliers?

AdaBoost is **highly sensitive to outliers** because:

1. Outliers are inherently **hard to classify correctly**
2. They get **misclassified repeatedly** → their weights keep growing exponentially
3. Eventually, the algorithm **overfits to outliers**, hurting generalization
4. Mislabeled data (label noise) causes the same problem

**Mitigation strategies:**
- Remove or clip outliers before training
- Use **robust loss functions** (e.g., Gradient Boosting with Huber loss)
- Limit the number of estimators
- Use Random Forest instead, which is less sensitive

> [!CAUTION]
> A single outlier can dominate the AdaBoost training process if its weight grows large enough to crowd out legitimate patterns.

---

## Q175. What is Gradient Boosting?

**Gradient Boosting** is an ensemble technique that builds models sequentially, where each new model is trained to **minimize the residual errors** (pseudo-residuals) of the previous ensemble using **gradient descent in function space**.

**Core idea:**
- Instead of reweighting samples (AdaBoost), fit the next tree to the **negative gradient of the loss function**

```python
from sklearn.ensemble import GradientBoostingClassifier

model = GradientBoostingClassifier(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=3
)
model.fit(X_train, y_train)
```

**General algorithm:**
```
F₀(x) = initial prediction (e.g., mean)
For t = 1 to T:
    rᵢ = -∂L(yᵢ, F_{t-1}(xᵢ)) / ∂F_{t-1}(xᵢ)   # pseudo-residuals
    hₜ = fit tree to (xᵢ, rᵢ)
    Fₜ(x) = F_{t-1}(x) + η · hₜ(x)
```

---

## Q176. How does Gradient Boosting differ from AdaBoost?

| Feature | AdaBoost | Gradient Boosting |
|---|---|---|
| **Focus mechanism** | Reweights samples | Fits residuals (negative gradient) |
| **Loss function** | Fixed exponential loss | Flexible — any differentiable loss |
| **Base learner weight** | Computed analytically (alpha) | Fixed learning rate (η) |
| **Robustness** | Sensitive to outliers | More robust (with appropriate loss) |
| **Generality** | Primarily classification | Both regression and classification |
| **Flexibility** | Limited | High (custom objectives) |

> [!NOTE]
> Gradient Boosting generalizes AdaBoost — AdaBoost is a special case of Gradient Boosting with exponential loss.

---

## Q177. What is shrinkage?

**Shrinkage** (also called the **learning rate**) scales the contribution of each new tree:

```
Fₜ(x) = F_{t-1}(x) + η · hₜ(x)
```

- `η` (eta) is a small positive number, typically between 0.01 and 0.3
- Each tree makes a **smaller step** toward the solution
- Forces the algorithm to **add more trees** for the same accuracy
- Acts as a form of **regularization** by preventing any single tree from dominating

```python
# Lower learning_rate → more trees needed but better generalization
model = GradientBoostingClassifier(learning_rate=0.05, n_estimators=500)
```

> [!TIP]
> Smaller learning rate + more estimators almost always produces better results than a large learning rate with few estimators.

---

## Q178. What is the learning-rate versus estimators tradeoff?

There is a **fundamental tradeoff** between `learning_rate` and `n_estimators`:

| Learning Rate | N Estimators | Effect |
|---|---|---|
| High (0.3–1.0) | Few (50–100) | Fast training, risk of overfitting |
| Low (0.01–0.05) | Many (500–5000) | Slow training, better generalization |
| Very low | Very many | Diminishing returns, expensive |

**Best practice:**
1. Set `learning_rate` low (e.g., 0.05)
2. Use early stopping to find the optimal `n_estimators`

```python
from sklearn.ensemble import GradientBoostingClassifier

# Use a small learning rate + more trees
model = GradientBoostingClassifier(
    learning_rate=0.05,
    n_estimators=1000,
    subsample=0.8  # also helps
)
```

> [!IMPORTANT]
> Always tune `learning_rate` and `n_estimators` together. Use cross-validation or early stopping to find the sweet spot.

---

## Q179. How can boosting models be regularized?

Several techniques exist to regularize gradient boosting:

| Technique | Parameter | Effect |
|---|---|---|
| **Learning rate (shrinkage)** | `learning_rate` | Reduces step size per tree |
| **Subsampling** | `subsample < 1.0` | Stochastic gradient boosting |
| **Max depth** | `max_depth` | Limits tree complexity |
| **Min samples split** | `min_samples_split` | Prevents small leaf splits |
| **Max features** | `max_features` | Random feature selection |
| **Early stopping** | `n_iter_no_change` | Stop when validation score plateaus |

```python
model = GradientBoostingClassifier(
    learning_rate=0.05,
    n_estimators=500,
    max_depth=3,          # shallow trees
    subsample=0.8,        # use 80% of data per tree
    max_features='sqrt',  # random subspace
    min_samples_leaf=10
)
```

---

## Q180. What causes boosting to overfit?

Boosting can overfit due to several factors:

1. **Too many estimators** — model memorizes training data
2. **High learning rate** — each tree has too much influence
3. **Deep trees** — individual trees become too complex
4. **No subsampling** — deterministic training without variance reduction
5. **Noisy labels** — boosting amplifies label noise over iterations
6. **Small dataset** — insufficient data for many trees to generalize

**Diagnosis:**
```python
# Plot train vs validation error over iterations
train_errors = [model.train_score_[i] for i in range(100)]
val_errors = [...]  # from staged_predict

import matplotlib.pyplot as plt
plt.plot(train_errors, label='Train')
plt.plot(val_errors, label='Validation')
plt.xlabel('Iteration')
plt.ylabel('Loss')
plt.legend()
plt.show()
```

**Fix:** Use early stopping, reduce `max_depth`, lower `learning_rate`, increase `subsample`.

> [!WARNING]
> Unlike Random Forest, boosting does NOT automatically stop overfitting with more trees — more estimators always risks overfitting without regularization.
