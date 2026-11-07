# Section 9: Decision Tree Classification

---

## Q116. What is a Decision Tree?

A **Decision Tree** is a supervised learning algorithm that makes predictions by learning a hierarchical set of **if-else decision rules** from the training data.

- It partitions the feature space into rectangular regions
- Each internal node tests a feature; each branch represents an outcome; each leaf gives a prediction
- Produces a human-interpretable, flowchart-like model

```python
from sklearn.tree import DecisionTreeClassifier, export_text

clf = DecisionTreeClassifier(max_depth=3, random_state=42)
clf.fit(X_train, y_train)

# Visualize the tree rules
print(export_text(clf, feature_names=feature_names))
```

---

## Q117. What are Root, Internal, and Leaf Nodes?

```
          [Root Node]          ← First split (best overall feature)
         /            \
  [Internal]       [Internal]  ← Intermediate splits
   /      \          /    \
[Leaf]  [Leaf]   [Leaf]  [Leaf] ← Final predictions
```

| Node Type | Description |
|-----------|-------------|
| **Root Node** | Top-most node; represents the best split across the entire dataset |
| **Internal Node** | Intermediate node; splits data further based on a feature threshold |
| **Leaf Node** | Terminal node; contains the final class prediction (majority class) |

- Depth of a node = number of edges from root to that node
- A leaf's prediction = majority class of training samples that reach it

---

## Q118. How does a Decision Tree choose a split?

At each node, the tree evaluates **all features** and **all thresholds** and selects the split that best **reduces impurity** (makes child nodes purer):

1. For each feature `f` and threshold `t`:
   - Split data into left (`x_f ≤ t`) and right (`x_f > t`) subsets
   - Compute impurity reduction (Information Gain or Gini Gain)
2. Choose the `(f, t)` pair that maximizes the impurity reduction
3. Recurse on each child node

```python
clf = DecisionTreeClassifier(
    criterion='gini',      # or 'entropy'
    splitter='best',       # or 'random'
    max_depth=5
)
```

The process is **greedy** — it makes the locally optimal split at each step, not a globally optimal tree.

---

## Q119. What is Gini Impurity?

**Gini impurity** measures the probability of misclassifying a randomly chosen sample if it were labeled according to the class distribution at that node:

$$\text{Gini}(t) = 1 - \sum_{k=1}^{C} p_k^2$$

Where `pₖ` = proportion of class `k` at node `t`, `C` = number of classes.

- **Range:** 0 (pure node) to `1 - 1/C` (maximally impure)
- **Binary classification:** max Gini = 0.5 (equal class distribution)

```python
import numpy as np

def gini(y):
    classes, counts = np.unique(y, return_counts=True)
    probs = counts / len(y)
    return 1 - np.sum(probs**2)

# Pure node: [A, A, A] → Gini = 0
# Impure:    [A, B]   → Gini = 0.5
```

---

## Q120. What is Entropy?

**Entropy** (from information theory) measures the average information (surprise) in a distribution — i.e., the level of disorder at a node:

$$H(t) = -\sum_{k=1}^{C} p_k \log_2(p_k)$$

Where `pₖ` = proportion of class `k`, with convention `0 · log₂(0) = 0`.

- **Range:** 0 (pure) to `log₂(C)` (maximally impure)
- **Binary:** max entropy = 1 bit (equal split)

```python
def entropy(y):
    classes, counts = np.unique(y, return_counts=True)
    probs = counts / len(y)
    return -np.sum(probs * np.log2(probs + 1e-9))
```

---

## Q121. What is Information Gain?

**Information Gain (IG)** measures how much a split reduces entropy (or impurity) compared to the parent node:

$$IG = H(\text{parent}) - \sum_{j \in \{L, R\}} \frac{n_j}{n} H(\text{child}_j)$$

Where `nⱼ` = number of samples in child `j`, `n` = total samples at parent.

- The tree always chooses the split with **maximum Information Gain**
- IG with Gini instead of entropy is called **Gini Gain**

```python
def information_gain(parent, left, right):
    n = len(parent)
    weighted_child_entropy = (len(left)/n) * entropy(left) + (len(right)/n) * entropy(right)
    return entropy(parent) - weighted_child_entropy
```

---

## Q122. What is the difference between Gini and Entropy?

| Property | Gini Impurity | Entropy |
|----------|--------------|---------|
| **Formula** | `1 - Σpₖ²` | `-Σpₖ log₂(pₖ)` |
| **Computation** | Faster (no log) | Slightly slower |
| **Range (binary)** | [0, 0.5] | [0, 1] |
| **Bias** | Slightly favors larger partitions | More balanced splits |
| **Practical difference** | Very similar results | Very similar results |

**In practice:** The choice between Gini and Entropy rarely makes a significant difference in model performance. Gini is the **default** in scikit-learn due to its lower computational cost.

---

## Q123. What causes Decision Trees to Overfit?

Decision Trees can grow until every leaf contains a **single training sample**, memorizing the training data:

- **No depth limit**: Tree grows indefinitely, capturing noise
- **Small leaf size**: Leaves with very few samples overfit to outliers
- **Greedy splitting**: Locally optimal splits may not generalize
- **No regularization**: Unlike linear models, no inherent parameter penalty

**Signs of overfitting:** Near-perfect training accuracy but poor test accuracy.

```python
# Overfit tree
clf_overfit = DecisionTreeClassifier()  # No constraints
clf_overfit.fit(X_train, y_train)
# train accuracy ≈ 100%, test accuracy << 100%
```

---

## Q124. What is Maximum Depth?

`max_depth` limits how many levels deep the tree can grow from the root:

- **Effect:** Fewer splits → simpler decision boundaries → less overfitting
- Setting `max_depth=None` (default) allows the tree to grow until leaves are pure
- **Tuning:** Use cross-validation to find the optimal depth

```python
from sklearn.model_selection import cross_val_score

for depth in range(1, 20):
    clf = DecisionTreeClassifier(max_depth=depth, random_state=42)
    score = cross_val_score(clf, X, y, cv=5).mean()
    print(f"Depth {depth}: {score:.4f}")
```

---

## Q125. What is Minimum Samples Split?

`min_samples_split` is the **minimum number of samples** required at a node to allow it to be split further:

- Default: `2` (split if node has ≥ 2 samples)
- **Higher value** → fewer splits → simpler tree → reduces overfitting
- Acts as regularization by preventing splits on small node populations

```python
clf = DecisionTreeClassifier(
    min_samples_split=10,  # Require at least 10 samples to split
    random_state=42
)
```

---

## Q126. What is Minimum Samples Leaf?

`min_samples_leaf` is the **minimum number of samples** that must remain in a leaf node after a split:

- If a proposed split would create a leaf with fewer than `min_samples_leaf` samples, the split is rejected
- **Higher value** → more regularization → smoother decision boundaries
- Ensures leaf predictions are based on sufficient evidence

```python
clf = DecisionTreeClassifier(
    min_samples_leaf=5,   # Each leaf must have ≥ 5 samples
    random_state=42
)
```

| Hyperparameter | Controls |
|---------------|---------|
| `min_samples_split` | Minimum samples **at a node** to consider splitting |
| `min_samples_leaf` | Minimum samples **in a resulting leaf** after splitting |

---

## Q127. What are Pre-pruning and Post-pruning?

### Pre-pruning (Early Stopping)
Stop tree growth **before** it fully develops using constraints:
- `max_depth`, `min_samples_split`, `min_samples_leaf`, `max_leaf_nodes`
- **Faster** but may stop too early

### Post-pruning (Cost-Complexity Pruning)
Grow the full tree **first**, then **remove** branches that provide little benefit:
- **Cost-complexity pruning (CCP)** in scikit-learn: controlled by `ccp_alpha`
- Higher `ccp_alpha` → more pruning → simpler tree

```python
# Find optimal ccp_alpha via cross-validation
path = DecisionTreeClassifier().cost_complexity_pruning_path(X_train, y_train)
ccp_alphas = path.ccp_alphas

# Try each alpha
for alpha in ccp_alphas:
    clf = DecisionTreeClassifier(ccp_alpha=alpha, random_state=42)
    clf.fit(X_train, y_train)
```

---

## Q128. How is Feature Importance Calculated?

Feature importance in Decision Trees is calculated using the **total impurity reduction** contributed by each feature across all splits:

$$\text{FI}(f) = \sum_{\text{nodes splitting on } f} \frac{n_t}{n} \left[ H(t) - \frac{n_L}{n_t}H(L) - \frac{n_R}{n_t}H(R) \right]$$

Then normalized so all importances sum to 1.

- Features used in **earlier splits** (higher up the tree) tend to have higher importance (they affect more samples)
- Features **not used** in any split have importance = 0

```python
clf.fit(X_train, y_train)
importances = clf.feature_importances_

for name, imp in sorted(zip(feature_names, importances), key=lambda x: -x[1]):
    print(f"{name}: {imp:.4f}")
```

---

## Q129. What are Decision Tree Advantages?

| Advantage | Description |
|-----------|-------------|
| ✅ **Interpretable** | Rules are human-readable and explainable |
| ✅ **No scaling needed** | Features don't need normalization |
| ✅ **Handles mixed types** | Works with numerical and categorical features |
| ✅ **Non-linear** | Captures complex decision boundaries |
| ✅ **Feature selection** | Built-in feature importance |
| ✅ **Fast training & inference** | O(n log n) training, O(depth) prediction |
| ✅ **Handles missing values** | Some implementations support missing data |
| ✅ **No distributional assumptions** | Non-parametric |

---

## Q130. What are Decision Tree Disadvantages?

| Disadvantage | Description |
|-------------|-------------|
| ❌ **Overfitting** | Easily memorizes training data |
| ❌ **High variance** | Small data changes can produce very different trees |
| ❌ **Axis-aligned splits** | Can't model diagonal decision boundaries efficiently |
| ❌ **Greedy algorithm** | Not globally optimal |
| ❌ **Imbalanced datasets** | Biased toward majority class |
| ❌ **Poor extrapolation** | Cannot predict beyond the range of training labels |
| ❌ **Instability** | Sensitive to small changes in data |

> These weaknesses are largely addressed by ensemble methods like **Random Forest** and **Gradient Boosting**, which combine many trees.
