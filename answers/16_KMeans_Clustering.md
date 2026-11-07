# Section 16: K-Means Clustering

---

## Q203. What is K-Means?

**K-Means** is an unsupervised learning algorithm that partitions data into **K non-overlapping clusters**, where each data point belongs to the cluster with the **nearest centroid**.

**Key properties:**
- Simple and computationally efficient
- Produces compact, spherical clusters
- Requires the number of clusters K to be specified in advance
- Minimizes **within-cluster variance (inertia)**

```python
from sklearn.cluster import KMeans
import numpy as np

# Fit K-Means with 3 clusters
kmeans = KMeans(n_clusters=3, random_state=42, n_init=10)
kmeans.fit(X)

labels = kmeans.labels_           # cluster assignments
centers = kmeans.cluster_centers_ # centroid coordinates
inertia = kmeans.inertia_         # sum of squared distances
```

> [!NOTE]
> K-Means is one of the most widely used clustering algorithms due to its simplicity and scalability to large datasets.

---

## Q204. What is a centroid?

A **centroid** is the **mean position** (geometric center) of all data points in a cluster.

```
μₖ = (1/|Cₖ|) · Σᵢ∈Cₖ xᵢ
```

- For a 2D dataset, the centroid is the (x̄, ȳ) mean of all cluster members
- Centroids are **not necessarily actual data points** — they are computed means
- They define the "representative" of each cluster

```python
import numpy as np
import matplotlib.pyplot as plt

# Visualize centroids
kmeans = KMeans(n_clusters=3).fit(X)

plt.scatter(X[:, 0], X[:, 1], c=kmeans.labels_, cmap='viridis', alpha=0.5)
plt.scatter(
    kmeans.cluster_centers_[:, 0],
    kmeans.cluster_centers_[:, 1],
    c='red', marker='X', s=200, label='Centroids'
)
plt.legend()
plt.title('K-Means Clusters and Centroids')
plt.show()
```

---

## Q205. How does K-Means work step by step?

K-Means uses an **iterative EM-like algorithm**:

```
Step 1: Initialize K centroids randomly (or via K-Means++)
Step 2: Assignment — assign each point to the nearest centroid
Step 3: Update — recompute centroids as the mean of assigned points
Step 4: Repeat steps 2–3 until convergence (centroids stop moving)
```

```python
# Manual K-Means illustration (simplified)
import numpy as np

def kmeans_manual(X, K, max_iter=100):
    # Initialize centroids randomly
    centroids = X[np.random.choice(len(X), K, replace=False)]

    for _ in range(max_iter):
        # Assignment step
        distances = np.linalg.norm(X[:, None] - centroids[None, :], axis=2)
        labels = np.argmin(distances, axis=1)

        # Update step
        new_centroids = np.array([X[labels == k].mean(axis=0) for k in range(K)])

        # Check convergence
        if np.allclose(centroids, new_centroids):
            break
        centroids = new_centroids

    return labels, centroids
```

**Convergence is guaranteed** — the inertia decreases monotonically at each step, so the algorithm always terminates.

---

## Q206. What is K-Means++?

**K-Means++** is a smarter initialization strategy that spreads initial centroids far apart, dramatically reducing the chance of poor convergence.

**Algorithm:**
1. Choose the first centroid randomly from the data points
2. For each subsequent centroid:
   - Compute distance `D(x)` from each point to the nearest existing centroid
   - Choose the next centroid with probability **proportional to D(x)²**
3. Repeat until K centroids are chosen

```python
# K-Means++ is the default in scikit-learn
kmeans = KMeans(n_clusters=3, init='k-means++', n_init=10)
kmeans.fit(X)

# Random initialization (not recommended)
kmeans_rand = KMeans(n_clusters=3, init='random', n_init=10)
```

**Benefits of K-Means++:**
- Faster convergence (fewer iterations needed)
- Consistently better results (avoids bad local optima)
- O(log K) approximation guarantee for the optimal solution

> [!IMPORTANT]
> Always use `init='k-means++'` (the sklearn default). Pure random initialization can produce highly suboptimal clusters.

---

## Q207. What objective function does K-Means minimize?

K-Means minimizes the **Within-Cluster Sum of Squares (WCSS)**, also called **inertia**:

```
WCSS = Σₖ Σᵢ∈Cₖ ||xᵢ - μₖ||²
```

Where:
- K = number of clusters
- Cₖ = set of points in cluster k
- μₖ = centroid of cluster k
- `||xᵢ - μₖ||²` = squared Euclidean distance from point to centroid

This is equivalent to maximizing **inter-cluster distance** while minimizing **intra-cluster distance**.

> [!WARNING]
> This objective is **NP-hard** to minimize globally. K-Means finds a **local minimum**, not the global optimum. Running with multiple random initializations (`n_init`) helps find better solutions.

---

## Q208. What is inertia?

**Inertia** is the **sum of squared distances** of each sample to its closest centroid — the value K-Means minimizes:

```python
kmeans = KMeans(n_clusters=3).fit(X)
print(f"Inertia: {kmeans.inertia_:.2f}")
```

**Properties of inertia:**
- Always ≥ 0 (lower is better)
- **Always decreases** as K increases
- Reaches 0 when K = N (each point is its own cluster)
- Not comparable across datasets with different scales

**Usage:**
- Used in the **Elbow Method** to choose K
- Measures cluster tightness (compactness)

> [!NOTE]
> Inertia alone should not be used to evaluate cluster quality in absolute terms — use it comparatively across different K values.

---

## Q209. How do you choose K?

Several methods help choose the optimal number of clusters:

| Method | Description |
|---|---|
| **Elbow Method** | Plot inertia vs K, choose the "elbow" |
| **Silhouette Score** | Choose K maximizing silhouette score |
| **Gap Statistic** | Compare inertia to random baseline |
| **Domain knowledge** | Use business requirements |
| **BIC/AIC** | For Gaussian Mixture Models |

```python
from sklearn.metrics import silhouette_score
import matplotlib.pyplot as plt

inertias = []
silhouettes = []
K_range = range(2, 11)

for k in K_range:
    km = KMeans(n_clusters=k, n_init=10, random_state=42)
    km.fit(X)
    inertias.append(km.inertia_)
    silhouettes.append(silhouette_score(X, km.labels_))

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))
ax1.plot(K_range, inertias, 'bo-')
ax1.set_title('Elbow Method')
ax2.plot(K_range, silhouettes, 'ro-')
ax2.set_title('Silhouette Score')
plt.show()
```

---

## Q210. What is the elbow method?

The **Elbow Method** plots **inertia vs K** and selects the K where the rate of decrease **sharply slows** (forming an "elbow"):

```
High K → Diminishing returns in inertia reduction
Elbow point → Optimal K (best compression/accuracy tradeoff)
```

```python
import matplotlib.pyplot as plt
from kneed import KneeLocator  # pip install kneed

inertias = []
K = range(1, 11)

for k in K:
    km = KMeans(n_clusters=k, n_init=10, random_state=42)
    km.fit(X)
    inertias.append(km.inertia_)

# Automatic elbow detection
kl = KneeLocator(list(K), inertias, curve='convex', direction='decreasing')
print(f"Optimal K: {kl.elbow}")

plt.plot(K, inertias, 'bo-')
plt.axvline(x=kl.elbow, color='red', linestyle='--', label=f'K={kl.elbow}')
plt.xlabel('Number of clusters K')
plt.ylabel('Inertia')
plt.title('Elbow Method')
plt.legend()
plt.show()
```

> [!NOTE]
> The elbow is not always clear-cut. When the curve is smooth, combine with Silhouette analysis for a better decision.

---

## Q211. Why is feature scaling important?

K-Means uses **Euclidean distance** to assign points to clusters. If features have **different scales**, high-magnitude features dominate the distance calculation:

**Example:** Age (0–100) vs. Salary (0–100,000) → Salary dominates

```python
from sklearn.preprocessing import StandardScaler

# Without scaling: salary dominates clustering
# With scaling: all features contribute equally

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

kmeans = KMeans(n_clusters=3, n_init=10)
kmeans.fit(X_scaled)
```

**Scaling methods for clustering:**
| Method | Best For |
|---|---|
| `StandardScaler` | Normal-ish distributions |
| `MinMaxScaler` | Bounded features |
| `RobustScaler` | Data with outliers |

> [!IMPORTANT]
> Always scale features before applying K-Means. Failure to scale is one of the most common mistakes in clustering practice.

---

## Q212. How do outliers affect K-Means?

K-Means is **highly sensitive to outliers** because:

1. Outliers pull centroids toward them (since centroids = means)
2. They can create **distorted, skewed clusters**
3. They may form their own **spurious clusters**
4. They inflate inertia significantly

```python
import numpy as np

# Outlier pulls centroid far from the main cluster
X_with_outlier = np.vstack([X, [100, 100]])  # extreme outlier

km = KMeans(n_clusters=3).fit(X_with_outlier)
# One centroid gets pulled toward [100, 100]
```

**Mitigation strategies:**
- Remove outliers before clustering (IQR, Z-score, Isolation Forest)
- Use **K-Medoids** (PAM) — uses actual data points as centers (robust to outliers)
- Use **DBSCAN** — treats outliers as noise

---

## Q213. What assumptions does K-Means make?

K-Means implicitly assumes:

| Assumption | Implication |
|---|---|
| **Spherical clusters** | Clusters are roughly circular/hyperspherical |
| **Equal cluster size** | Works poorly with very different-sized clusters |
| **Equal cluster density** | Struggles if some clusters are denser than others |
| **Euclidean distance is meaningful** | Requires numeric, scaled features |
| **K is known** | User must specify number of clusters |
| **No overlapping clusters** | Each point belongs to exactly one cluster |

> [!CAUTION]
> If your data has elongated, crescent-shaped, or irregularly sized clusters, K-Means will fail. Use DBSCAN, GMM, or Spectral Clustering instead.

---

## Q214. Why can K-Means converge to a local optimum?

The K-Means objective (WCSS) is **non-convex** — it has multiple local minima:

- Different random initializations → different final cluster assignments
- The algorithm **greedily minimizes** at each step but cannot escape local optima
- The result depends heavily on the initial centroid placement

**Solutions:**
```python
# Run multiple times with different initializations
kmeans = KMeans(n_clusters=3, n_init=20, random_state=42)  # 20 runs
# Returns the best result (lowest inertia) across all runs

# Use K-Means++ for better initialization
kmeans = KMeans(n_clusters=3, init='k-means++', n_init=10)
```

> [!TIP]
> Increasing `n_init` is the most reliable way to avoid bad local optima. The default `n_init=10` in sklearn is usually sufficient for most problems.

---

## Q215. What are K-Means limitations?

| Limitation | Explanation |
|---|---|
| **Must specify K** | Requires domain knowledge or trial-and-error |
| **Assumes spherical clusters** | Fails for elongated, irregular shapes |
| **Sensitive to outliers** | Outliers skew centroids |
| **Sensitive to initialization** | May converge to poor local optima |
| **Requires feature scaling** | Euclidean distance is scale-dependent |
| **Hard assignments** | Each point belongs to exactly one cluster |
| **Assumes equal variance** | Struggles with clusters of different densities |
| **Doesn't handle categoricals** | Needs numeric features; use K-Modes for categorical |

**Alternatives for different scenarios:**
```python
# Non-spherical clusters
from sklearn.cluster import DBSCAN, SpectralClustering

# Probabilistic soft assignments
from sklearn.mixture import GaussianMixture

# Categorical data
# pip install kmodes
from kmodes.kmodes import KModes

# Robust to outliers
from sklearn_extra.cluster import KMedoids
```
