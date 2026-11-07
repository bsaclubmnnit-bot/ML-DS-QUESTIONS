# Section 11: Ensemble Learning, Bagging and Boosting

---

## Q141. What is Ensemble Learning?

**Ensemble learning** combines predictions from **multiple models** (base learners) to produce a final prediction that is better than any individual model alone.

Key intuition: **wisdom of the crowd** — errors made by individual models tend to cancel out when combined.

```python
from sklearn.ensemble import VotingClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.svm import SVC

# Hard voting ensemble
ensemble = VotingClassifier(estimators=[
    ('dt', DecisionTreeClassifier()),
    ('lr', LogisticRegression()),
    ('svm', SVC())
], voting='hard')
ensemble.fit(X_train, y_train)
```

Three main strategies:
- **Bagging** — parallel training on different data subsets (reduces variance)
- **Boosting** — sequential training focusing on errors (reduces bias)
- **Stacking** — meta-model learns from base model predictions

---

## Q142. Why can combining models improve performance?

Combining models works when individual models make **different errors**. If model errors are uncorrelated, averaging cancels them out.

**Mathematically (for regression, averaging M models):**

$$\text{Var}(\bar{y}) = \frac{\sigma^2}{M} \quad \text{(if uncorrelated)}$$

Variance drops by factor `M` with `M` uncorrelated models.

**Two conditions for ensemble improvement:**
1. **Diversity** — models should make different mistakes (uncorrelated errors)
2. **Accuracy** — each model should be better than random guessing

> If all models make the same errors (identical), ensembling gives no benefit. The more **diverse** the errors, the more benefit from combining.

---

## Q143. What is Bagging?

**Bagging (Bootstrap AGGregating)** trains multiple models **in parallel** on different **bootstrap samples** of the training data, then aggregates predictions:

1. Draw `B` bootstrap samples (with replacement) from training data
2. Train a base model on each sample **independently**
3. **Aggregate**: majority vote (classification) or mean (regression)

```python
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier

bag = BaggingClassifier(
    base_estimator=DecisionTreeClassifier(),
    n_estimators=100,
    max_samples=1.0,       # fraction of training set per bootstrap
    bootstrap=True,        # sample with replacement
    random_state=42
)
bag.fit(X_train, y_train)
```

- **Reduces variance** without significantly increasing bias
- Best applied to **high-variance, low-bias** models (e.g., deep decision trees)

---

## Q144. What is Boosting?

**Boosting** trains models **sequentially**, where each model focuses on correcting the errors of the previous one:

1. Train a weak model on the full training data
2. Identify misclassified/high-error samples
3. Increase their weight (or fit residuals)
4. Train the next model on the reweighted data
5. Combine all models using weighted voting/summation

```python
from sklearn.ensemble import AdaBoostClassifier, GradientBoostingClassifier

# AdaBoost
ada = AdaBoostClassifier(n_estimators=100, learning_rate=0.1, random_state=42)
ada.fit(X_train, y_train)

# Gradient Boosting
gb = GradientBoostingClassifier(n_estimators=100, learning_rate=0.1, max_depth=3)
gb.fit(X_train, y_train)
```

- **Reduces bias** — turns weak learners into strong ones
- Sequential nature means it **cannot be parallelized** across trees

---

## Q145. What is the difference between Bagging and Boosting?

| Aspect | Bagging | Boosting |
|--------|---------|---------|
| **Training** | Parallel (independent) | Sequential (dependent) |
| **Data sampling** | Bootstrap (with replacement) | Weighted / residual fitting |
| **Primary effect** | Reduces **variance** | Reduces **bias** |
| **Model type** | Works with any model | Usually weak learners |
| **Interpretability** | Moderate | Lower |
| **Sensitivity to noise** | Robust | Sensitive (can overfit noise) |
| **Speed** | Fast (parallelizable) | Slower (sequential) |
| **Examples** | Random Forest | AdaBoost, XGBoost, LightGBM |

**Rule of thumb:**
- Use **Bagging** when your model overfits (high variance)
- Use **Boosting** when your model underfits (high bias)

---

## Q146. What is Bootstrap Sampling?

**Bootstrap sampling** draws `n` samples **with replacement** from a dataset of size `n`:

- Each bootstrap sample is the same size as the original dataset
- On average, each bootstrap sample contains ~**63.2%** unique samples
- ~**36.8%** of original samples are excluded (Out-of-Bag samples)

```python
import numpy as np

def bootstrap_sample(X, y, random_state=None):
    rng = np.random.RandomState(random_state)
    n = len(X)
    indices = rng.choice(n, size=n, replace=True)  # with replacement
    return X[indices], y[indices]

X_boot, y_boot = bootstrap_sample(X_train, y_train, random_state=42)
```

**Why ~63.2% unique?**
$$P(\text{not selected once}) = \left(1 - \frac{1}{n}\right)^n \xrightarrow{n \to \infty} e^{-1} \approx 0.368$$

---

## Q147. How does Bagging Reduce Variance?

Each bootstrap sample trains a model on slightly different data, producing diverse models. When averaged, their individual errors cancel out:

**For `M` models with variance `σ²` and pairwise correlation `ρ`:**

$$\text{Var}(\bar{f}) = \rho \sigma^2 + \frac{1-\rho}{M} \sigma^2$$

- As `M → ∞`, the second term → 0
- The remaining variance `ρσ²` depends on **correlation** between trees
- **Key:** reducing correlation between models (random subspaces, bootstrap) reduces overall variance

> Random Forest further reduces `ρ` by using random feature subsets at each split.

---

## Q148. How does Boosting Reduce Bias?

Boosting reduces bias by **sequentially fitting residuals** — each model corrects the previous model's errors:

$$F_m(x) = F_{m-1}(x) + \alpha_m \cdot h_m(x)$$

Where `hₘ` is trained on the **residuals** (or weighted errors) of `F_{m-1}`.

- Even if each `hₘ` is a weak learner (high bias, e.g., a shallow tree), the **sum** of many weak learners approximates a complex function
- This is analogous to **gradient descent in function space**
- With enough iterations, boosting can achieve very low training error

---

## Q149. What is a Weak Learner?

A **weak learner** is a model that performs only **slightly better than random guessing**:

- For binary classification: accuracy slightly above 50%
- Example: a **decision stump** (decision tree with depth=1)
- Individually, each weak learner has **high bias**

```python
from sklearn.tree import DecisionTreeClassifier

# Decision stump = weak learner
stump = DecisionTreeClassifier(max_depth=1)
stump.fit(X_train, y_train)
print(stump.score(X_test, y_test))  # e.g., 0.55
```

Boosting theory (Schapire, 1990): any algorithm that can produce weak learners can be **boosted** to achieve arbitrarily high accuracy.

---

## Q150. What is a Strong Learner?

A **strong learner** is a model that achieves **arbitrarily high accuracy** — as close to perfect as desired.

- In practice: a model with high accuracy on the task
- Boosting converts multiple weak learners into a strong learner by aggregating them
- The **final ensemble** is the strong learner, even if each component is weak

---

## Q151. What is Stacking?

**Stacking (Stacked Generalization)** is an ensemble method where predictions from multiple **level-0 base models** are used as inputs to a **level-1 meta-model**:

```
Training Data → [Model 1, Model 2, Model 3] → Predictions → [Meta-Model] → Final Prediction
```

```python
from sklearn.ensemble import StackingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.svm import SVC

estimators = [
    ('dt', DecisionTreeClassifier(max_depth=5)),
    ('svm', SVC(probability=True)),
]

stack = StackingClassifier(
    estimators=estimators,
    final_estimator=LogisticRegression(),  # meta-model
    cv=5                                   # cross-val to generate meta-features
)
stack.fit(X_train, y_train)
```

- Base models must be **diverse** (different algorithms, different feature views)
- Meta-model learns **how to combine** base model outputs
- Typically outperforms any single base model

---

## Q152. What is Blending?

**Blending** is a simplified version of stacking where:
- Base models are trained on a training split
- A **holdout set** (not seen by base models) is used to train the meta-model
- Predictions on the holdout set become meta-features

| | Stacking | Blending |
|-|---------|---------|
| **Meta-features** | Generated via cross-validation | Generated on a holdout set |
| **Data efficiency** | Better (uses all data) | Worse (holdout is "wasted") |
| **Simplicity** | More complex | Simpler to implement |
| **Leakage risk** | Lower (CV prevents it) | Higher (if holdout overlaps) |

---

## Q153. What is Out-of-Bag Evaluation?

In Bagging, each bootstrap sample leaves out ~36.8% of training samples (Out-of-Bag samples). These **OOB samples** were never seen by that particular tree and can be used as a **free validation set**:

- Each training sample is OOB for some fraction of trees
- Average the predictions from only those trees for which the sample was OOB
- Provides an **unbiased estimate of generalization error** without a separate validation set

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,
    oob_score=True,       # Enable OOB evaluation
    random_state=42
)
rf.fit(X_train, y_train)
print(f"OOB Score: {rf.oob_score_:.4f}")
```

---

## Q154. Why can Boosting be Sensitive to Noisy Data?

Boosting **focuses increasingly on misclassified samples** by upweighting them. This becomes problematic with noisy data:

- Noisy samples (mislabeled or extreme outliers) get **repeatedly upweighted** because they're hard to classify correctly
- The algorithm spends more and more capacity fitting irreversible errors
- This leads to **overfitting on noise** — the ensemble fits the noisy labels instead of true patterns

**Mitigations:**
- **Reduce learning rate** (`learning_rate` / `shrinkage`): slower adaptation to errors
- **Limit tree depth**: prevents individual learners from perfectly fitting noise
- **Subsample** training data per iteration (Stochastic Gradient Boosting)
- **Early stopping**: monitor validation loss and stop before overfitting noise

```python
from sklearn.ensemble import GradientBoostingClassifier

gb = GradientBoostingClassifier(
    n_estimators=500,
    learning_rate=0.05,    # Small learning rate
    max_depth=3,           # Shallow trees
    subsample=0.8,         # Stochastic boosting
    random_state=42
)
```
