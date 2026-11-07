# Section 8: KNN

---

## Q102. What is KNN?

**K-Nearest Neighbors (KNN)** is a simple, non-parametric, instance-based learning algorithm used for both **classification** and **regression**.

- It makes predictions by looking at the **K closest training examples** (neighbors) to a new data point
- No model is explicitly trained — predictions are made at query time
- Works on the principle: *"similar inputs tend to have similar outputs"*

```python
from sklearn.neighbors import KNeighborsClassifier

knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train, y_train)
predictions = knn.predict(X_test)
```

---

## Q103. Why is KNN called a Lazy Learner?

KNN is called a **lazy learner** because it defers all computation to prediction time:

| | Lazy Learner (KNN) | Eager Learner (SVM, Decision Tree) |
|--|---|---|
| **Training** | Just stores data — O(1) | Fits a model — O(n) |
| **Prediction** | Searches all training data | Uses pre-built model |
| **Memory** | Stores entire dataset | Only stores model parameters |

- There is **no explicit training phase** — the algorithm simply memorizes the training set
- All generalization is deferred until a query arrives
- This makes training fast but **prediction slow** for large datasets

---

## Q104. How does KNN make predictions?

**For Classification:**
1. Compute distance from the query point to all training points
2. Select the **K nearest** training points
3. Take a **majority vote** among K neighbors' labels
4. Assign that label to the query point

**For Regression:**
1. Find the K nearest neighbors
2. Return the **mean** (or weighted mean) of their target values

```python
# Classification: majority vote
from sklearn.neighbors import KNeighborsClassifier
knn_clf = KNeighborsClassifier(n_neighbors=5, weights='uniform')

# Regression: mean of neighbors
from sklearn.neighbors import KNeighborsRegressor
knn_reg = KNeighborsRegressor(n_neighbors=5, weights='distance')
```

**Weighted voting** (`weights='distance'`): closer neighbors get more influence via `weight = 1/distance`.

---

## Q105. How do you choose K?

Choosing the right K is crucial and is treated as a **hyperparameter tuning** problem:

- **Cross-validation**: Try multiple K values and pick the one with best CV score
- **Rule of thumb**: `K ≈ √n` where `n` is the number of training samples
- **Odd K** is preferred for binary classification to avoid ties

```python
from sklearn.model_selection import cross_val_score
import numpy as np

k_values = range(1, 31)
cv_scores = []

for k in k_values:
    knn = KNeighborsClassifier(n_neighbors=k)
    scores = cross_val_score(knn, X_train, y_train, cv=5, scoring='accuracy')
    cv_scores.append(scores.mean())

best_k = k_values[np.argmax(cv_scores)]
print(f"Best K: {best_k}")
```

---

## Q106. What happens when K is too small?

When K is **too small** (e.g., K=1):

- The model becomes **highly sensitive** to individual data points
- It **overfits** — captures noise and outliers
- **High variance, low bias**
- Decision boundary is very complex and irregular
- Perfect or near-perfect accuracy on training data but poor generalization

> K=1 means the prediction equals the label of the single nearest neighbor — the model memorizes the training data.

---

## Q107. What happens when K is too large?

When K is **too large** (e.g., K = n):

- The model becomes **too smooth** — predicts the same class for almost everything (the majority class)
- **Underfits** — ignores local structure
- **High bias, low variance**
- Decision boundary becomes overly simple
- Performance degrades toward the baseline (most frequent class)

> The sweet spot for K lies between these two extremes, found via cross-validation.

---

## Q108. Why is feature scaling important for KNN?

KNN relies on **distance metrics**. If features are on different scales, features with larger magnitudes will **dominate** the distance calculation.

**Example:** Age (0–80) vs. Income (0–1,000,000) — income would dominate Euclidean distance.

**Solution: Normalize or standardize features before applying KNN:**

```python
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline
from sklearn.neighbors import KNeighborsClassifier

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('knn', KNeighborsClassifier(n_neighbors=5))
])
pipeline.fit(X_train, y_train)
```

- `StandardScaler`: zero mean, unit variance — `z = (x - μ) / σ`
- `MinMaxScaler`: scales to [0, 1] — `x' = (x - min) / (max - min)`

---

## Q109. What distance metrics can KNN use?

| Metric | Formula | Best Used For |
|--------|---------|--------------|
| **Euclidean** | `√Σ(xᵢ - yᵢ)²` | Continuous features, low dimensions |
| **Manhattan** | `Σ\|xᵢ - yᵢ\|` | High dimensions, robust to outliers |
| **Minkowski** | `(Σ\|xᵢ - yᵢ\|ᵖ)^(1/p)` | Generalization (p=2→Euclidean, p=1→Manhattan) |
| **Hamming** | Fraction of differing positions | Categorical/binary features |
| **Cosine** | `1 - (X·Y)/(‖X‖‖Y‖)` | Text data, directional similarity |

```python
knn = KNeighborsClassifier(n_neighbors=5, metric='manhattan')
knn = KNeighborsClassifier(n_neighbors=5, metric='minkowski', p=2)
```

---

## Q110. What is Euclidean Distance?

**Euclidean distance** is the straight-line distance between two points in n-dimensional space:

$$d(A, B) = \sqrt{\sum_{i=1}^{n} (A_i - B_i)^2}$$

- Default metric for KNN in scikit-learn
- Sensitive to scale (requires normalization)
- Works well in low dimensions with continuous features

```python
import numpy as np

A = np.array([1, 2, 3])
B = np.array([4, 6, 3])
euclidean = np.sqrt(np.sum((A - B)**2))
print(euclidean)  # 5.0
```

---

## Q111. What is Manhattan Distance?

**Manhattan distance** (also called L1 distance or city-block distance) is the sum of absolute differences:

$$d(A, B) = \sum_{i=1}^{n} |A_i - B_i|$$

- Named after navigating a city grid — you can only move horizontally/vertically
- Less sensitive to outliers than Euclidean distance
- Often preferred in **high-dimensional spaces**

```python
import numpy as np

A = np.array([1, 2, 3])
B = np.array([4, 6, 3])
manhattan = np.sum(np.abs(A - B))
print(manhattan)  # 7
```

---

## Q112. What is the Curse of Dimensionality?

The **curse of dimensionality** refers to the phenomenon where the performance of distance-based algorithms degrades as the number of features (dimensions) increases:

- In high dimensions, **all points become approximately equidistant** from each other
- The concept of "nearest neighbor" loses meaning — there's no meaningful notion of closeness
- The amount of data needed grows **exponentially** with dimensions to maintain coverage
- Distance metrics become less discriminative

**Practical impact on KNN:**
- Neighbors found in high dimensions may not be truly similar
- Accuracy drops; computation cost increases
- **Solutions:** Dimensionality reduction (PCA, t-SNE), feature selection, or using alternative algorithms

---

## Q113. How does KNN perform regression?

In **KNN Regression**:
1. Find the K nearest neighbors to the query point
2. Predict the **average** (or weighted average) of the neighbors' target values

$$\hat{y} = \frac{1}{K} \sum_{i \in \mathcal{N}_K} y_i \quad \text{(uniform)}$$

$$\hat{y} = \frac{\sum_{i \in \mathcal{N}_K} w_i y_i}{\sum_{i \in \mathcal{N}_K} w_i} \quad \text{where } w_i = \frac{1}{d_i} \text{ (distance-weighted)}$$

```python
from sklearn.neighbors import KNeighborsRegressor

knn_reg = KNeighborsRegressor(n_neighbors=5, weights='distance')
knn_reg.fit(X_train, y_train)
y_pred = knn_reg.predict(X_test)
```

- Small K → captures local variation (can overfit)
- Large K → smoother predictions (can underfit)

---

## Q114. What are KNN's Computational Limitations?

| Limitation | Detail |
|-----------|--------|
| **Slow prediction** | O(n·d) per query — must scan all training points |
| **High memory** | Stores entire training dataset |
| **Scales poorly** | Performance degrades with large `n` or high `d` |
| **No model compression** | Can't summarize patterns into a compact model |

**Mitigation strategies:**
- **KD-Tree / Ball-Tree**: Spatial data structures for faster neighbor search (effective for low-to-moderate dimensions)
- **Approximate Nearest Neighbors**: FAISS, Annoy, HNSW for large-scale search
- **Dimensionality reduction**: PCA before KNN

```python
knn = KNeighborsClassifier(n_neighbors=5, algorithm='ball_tree')
# algorithm options: 'auto', 'ball_tree', 'kd_tree', 'brute'
```

---

## Q115. How can KNN handle imbalanced datasets?

KNN is inherently biased toward the **majority class** in imbalanced settings because more majority-class points exist among the K neighbors.

**Strategies:**

1. **Weighted voting by class prior** — penalize majority class contributions
2. **Resampling** — oversample minority (`SMOTE`) or undersample majority class
3. **Distance-weighted KNN** — closer neighbors (often minority) get more weight
4. **Adjust K** — use a smaller K to give minority samples more influence
5. **Class-weighted metrics** — evaluate with F1-score, not accuracy

```python
from imblearn.over_sampling import SMOTE
from sklearn.neighbors import KNeighborsClassifier
from imblearn.pipeline import Pipeline

pipeline = Pipeline([
    ('smote', SMOTE(random_state=42)),
    ('knn', KNeighborsClassifier(n_neighbors=5, weights='distance'))
])
pipeline.fit(X_train, y_train)
```
