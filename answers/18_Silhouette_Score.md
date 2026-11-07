# Section 18: Silhouette Score

---

## Q226. What is the Silhouette Score?

The **Silhouette Score** is a metric for evaluating the quality of clustering without ground truth labels. It measures how **similar a point is to its own cluster** compared to **other clusters**.

**For a single point i:**
```
s(i) = (b(i) - a(i)) / max(a(i), b(i))
```

Where:
- **a(i)** = mean distance from point i to all other points **in the same cluster** (cohesion — lower is better)
- **b(i)** = mean distance from point i to all points in the **nearest other cluster** (separation — higher is better)

**Overall score:** Mean of `s(i)` across all points.

```python
from sklearn.metrics import silhouette_score, silhouette_samples
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=3, random_state=42).fit(X)
score = silhouette_score(X, kmeans.labels_)
print(f"Silhouette Score: {score:.4f}")

# Per-sample scores
sample_scores = silhouette_samples(X, kmeans.labels_)
```

---

## Q227. What does a high score indicate?

| Score Range | Interpretation |
|---|---|
| **0.71 – 1.00** | Strong structure — well-separated, compact clusters |
| **0.51 – 0.70** | Reasonable structure |
| **0.26 – 0.50** | Weak structure — may be artificial |
| **≤ 0.25** | No substantial structure found |

A **high score** (close to +1) indicates:
- Points are **tightly grouped** within their cluster (low a(i))
- Clusters are **well-separated** from each other (high b(i))
- The clustering structure is meaningful and robust

```python
# Visualize silhouette analysis
import matplotlib.pyplot as plt
import numpy as np

fig, ax = plt.subplots(figsize=(8, 5))
y_lower = 10

for k in range(3):
    cluster_scores = sample_scores[kmeans.labels_ == k]
    cluster_scores.sort()
    size = len(cluster_scores)
    y_upper = y_lower + size
    ax.fill_betweenx(np.arange(y_lower, y_upper), 0, cluster_scores)
    ax.text(-0.05, y_lower + 0.5 * size, str(k))
    y_lower = y_upper + 10

ax.axvline(x=score, color='red', linestyle='--', label=f'Avg={score:.2f}')
ax.set_xlabel('Silhouette Coefficient')
ax.set_title('Silhouette Analysis')
ax.legend()
plt.show()
```

---

## Q228. What is the range of the score?

The Silhouette Score ranges from **-1 to +1**:

```
s(i) = (b(i) - a(i)) / max(a(i), b(i))
```

| Value | Meaning |
|---|---|
| **+1** | Perfect: point is very close to its cluster, far from others |
| **0** | Borderline: point is on or near a cluster boundary |
| **-1** | Bad: point is closer to a neighboring cluster than its own |

**Derivation of bounds:**
- When `a(i) = 0`: `s(i) = b(i)/b(i) = 1` (perfect cohesion)
- When `b(i) = 0`: `s(i) = -a(i)/a(i) = -1` (perfectly misclassified)
- When `a(i) = b(i)`: `s(i) = 0` (on the boundary)

> [!NOTE]
> The range [-1, +1] makes the score intuitive and comparable across different datasets and clustering algorithms.

---

## Q229. What does a negative score indicate?

A **negative Silhouette Score** for a point means it is **closer to points in another cluster** than to points in its own assigned cluster — it is **likely misclassified**.

```python
sample_scores = silhouette_samples(X, kmeans.labels_)

# Points with negative scores are likely misclassified
misclassified = np.where(sample_scores < 0)[0]
print(f"Potentially misclassified: {len(misclassified)} points")

# Inspect them
print(X[misclassified[:5]])
```

**Negative scores signal:**
1. **Wrong K** — too many or too few clusters
2. **Overlapping clusters** — no clear separation in the data
3. **Poor initialization** — K-Means converged to a suboptimal solution
4. **Wrong algorithm** — data may have non-spherical clusters

> [!WARNING]
> Many negative scores across the dataset strongly suggest that the chosen K is inappropriate or the algorithm doesn't fit the data's geometry.

---

## Q230. How is it used to choose K?

The Silhouette Score is an excellent tool for selecting the optimal K:

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score
import matplotlib.pyplot as plt

scores = []
K_range = range(2, 11)

for k in K_range:
    km = KMeans(n_clusters=k, n_init=10, random_state=42)
    km.fit(X)
    score = silhouette_score(X, km.labels_)
    scores.append(score)
    print(f"K={k}: Silhouette={score:.4f}")

# Choose K with maximum silhouette score
best_k = K_range[scores.index(max(scores))]

plt.plot(list(K_range), scores, 'bo-')
plt.axvline(x=best_k, color='red', linestyle='--', label=f'Best K={best_k}')
plt.xlabel('Number of Clusters K')
plt.ylabel('Silhouette Score')
plt.title('Silhouette Score vs K')
plt.legend()
plt.show()
```

**Strategy:** Choose the K that **maximizes** the average Silhouette Score.

> [!TIP]
> Combine the Silhouette Score with the Elbow Method for a more robust K selection. When both methods agree, you can be more confident in the chosen K.

---

## Q231. What are its limitations?

| Limitation | Explanation |
|---|---|
| **Assumes convex clusters** | Silhouette score based on Euclidean distance; unfavorable for non-convex (e.g., crescent-shaped) clusters |
| **Computationally expensive** | O(n²) pairwise distance computation — slow for large datasets |
| **Can be misleading** | Non-Euclidean data (text, graphs) may give spurious scores |
| **High score ≠ meaningful clusters** | Even random partitions can score moderately well |
| **Doesn't measure external validity** | No ground truth comparison |
| **K=2 bias** | Often artificially high for K=2 due to mathematical construction |

**Alternatives for evaluation:**
```python
from sklearn.metrics import (
    davies_bouldin_score,    # lower is better
    calinski_harabasz_score  # higher is better
)

db_score = davies_bouldin_score(X, labels)
ch_score = calinski_harabasz_score(X, labels)

print(f"Davies-Bouldin: {db_score:.4f}")
print(f"Calinski-Harabasz: {ch_score:.4f}")
```

> [!NOTE]
> For DBSCAN or other density-based methods, the Silhouette Score can still be used but noise points (label=-1) must be excluded from calculation.
