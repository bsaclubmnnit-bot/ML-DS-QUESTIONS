# Section 19: DBSCAN

---

## Q232. What is DBSCAN?

**DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** is a clustering algorithm that groups together points that are **closely packed** (high density regions) and marks as **outliers** points that lie in **low-density regions**.

**Key properties:**
- Does **not require K** to be specified
- Can find clusters of **arbitrary shape**
- Automatically identifies and labels **outliers/noise** as -1
- Based on two parameters: `epsilon` and `min_samples`

```python
from sklearn.cluster import DBSCAN
from sklearn.preprocessing import StandardScaler

X_scaled = StandardScaler().fit_transform(X)

dbscan = DBSCAN(eps=0.5, min_samples=5)
labels = dbscan.fit_predict(X_scaled)

# labels: -1 = noise, 0, 1, 2, ... = cluster IDs
n_clusters = len(set(labels)) - (1 if -1 in labels else 0)
n_noise = list(labels).count(-1)

print(f"Clusters: {n_clusters}, Noise points: {n_noise}")
```

> [!NOTE]
> DBSCAN was introduced by Ester et al. (1996) and is one of the most cited data mining algorithms. It won the ACM SIGKDD Test of Time award.

---

## Q233. What do epsilon and min_samples represent?

These two parameters define what "dense enough" means:

**`epsilon` (eps):**
- The **radius** of the neighborhood around each point
- Two points are "neighbors" if their distance ≤ ε
- **Smaller ε** → denser clusters, more noise points
- **Larger ε** → looser clusters, fewer noise points

**`min_samples`:**
- The **minimum number of points** (including the point itself) required within ε to form a dense region
- **Higher min_samples** → stricter definition of core point → more noise
- **Lower min_samples** → more lenient → fewer noise points

```python
# Tight, high-density clusters
dbscan_tight = DBSCAN(eps=0.3, min_samples=10)

# Loose, low-density acceptable
dbscan_loose = DBSCAN(eps=1.0, min_samples=3)
```

**Rule of thumb:** `min_samples ≥ dimensions + 1`, often set to `2 × dimensions`.

---

## Q234. What is a core point?

A **core point** is a point with **at least `min_samples` neighbors** (including itself) within radius `epsilon`:

```
Point p is a core point if: |N_ε(p)| ≥ min_samples
```

Where `N_ε(p)` = set of points within distance ε of p.

```python
import numpy as np
from sklearn.metrics import pairwise_distances

def find_core_points(X, eps, min_samples):
    dists = pairwise_distances(X)
    neighbor_counts = (dists <= eps).sum(axis=1)  # includes self
    return np.where(neighbor_counts >= min_samples)[0]

core_indices = find_core_points(X_scaled, eps=0.5, min_samples=5)

# In sklearn
dbscan = DBSCAN(eps=0.5, min_samples=5).fit(X_scaled)
core_indices = dbscan.core_sample_indices_
```

Core points are the **seeds** from which clusters grow. All core points within ε of each other belong to the same cluster.

---

## Q235. What is a border point?

A **border point** is a non-core point that falls within the neighborhood (ε) of a core point:

- Has **fewer than `min_samples` neighbors** (so not a core point itself)
- But is **reachable from** a core point
- Belongs to the **cluster of its neighboring core point**
- If reachable from multiple clusters' core points → belongs to the first one found (implementation-dependent)

```
Core point: ●  (≥ min_samples neighbors in radius ε)
Border point: ○  (< min_samples neighbors, but within ε of a core point)
Noise point: ✕  (not within ε of any core point)
```

Border points are part of the cluster but **do not expand** it further.

---

## Q236. What is a noise point?

A **noise point** (outlier) is a point that is:
- **Not a core point** (too few neighbors within ε)
- **Not reachable** from any core point

DBSCAN assigns noise points a label of **-1**.

```python
dbscan = DBSCAN(eps=0.5, min_samples=5).fit(X_scaled)
labels = dbscan.labels_

noise_mask = labels == -1
noise_points = X_scaled[noise_mask]

print(f"Number of noise points: {noise_mask.sum()}")

import matplotlib.pyplot as plt
plt.scatter(X_scaled[~noise_mask, 0], X_scaled[~noise_mask, 1],
            c=labels[~noise_mask], cmap='viridis', alpha=0.6, label='Clusters')
plt.scatter(noise_points[:, 0], noise_points[:, 1],
            c='red', marker='x', s=100, label='Noise')
plt.legend()
plt.title('DBSCAN: Clusters and Noise Points')
plt.show()
```

> [!TIP]
> The noise points identified by DBSCAN are a useful by-product — they can directly serve as an outlier detection result.

---

## Q237. How does DBSCAN discover clusters?

DBSCAN uses the concept of **density-reachability** to grow clusters:

**Algorithm:**
```
For each unvisited point p:
    Mark p as visited
    Find all neighbors N_ε(p) within radius ε
    
    If |N_ε(p)| < min_samples:
        Mark p as noise
    Else:
        Create new cluster C
        Add p to C
        For each neighbor q in N_ε(p):
            If q is unvisited:
                Mark q as visited
                Find N_ε(q)
                If |N_ε(q)| ≥ min_samples:
                    Add N_ε(q) to N_ε(p) (expand)
            If q is not in any cluster:
                Add q to C
```

**Key concepts:**
- **Directly density-reachable**: q is in N_ε(p) and p is a core point
- **Density-reachable**: Chain of directly density-reachable points from p to q
- **Density-connected**: Both p and q are density-reachable from a common core point o

---

## Q238. Why can DBSCAN find arbitrary shapes?

DBSCAN discovers clusters by **following the density** of points, not by fitting geometric shapes:

- It does **not assume clusters are spherical** (unlike K-Means)
- It follows **local density** — any connected dense region forms a cluster
- Works for **crescent, ring, S-curve**, and other non-convex shapes

```python
from sklearn.datasets import make_moons, make_circles

# Non-linear data that K-Means fails on
X_moons, _ = make_moons(n_samples=300, noise=0.05, random_state=42)
X_circles, _ = make_circles(n_samples=300, noise=0.05, factor=0.5, random_state=42)

# DBSCAN handles these well
for name, data in [('Moons', X_moons), ('Circles', X_circles)]:
    labels = DBSCAN(eps=0.2, min_samples=5).fit_predict(data)
    n = len(set(labels)) - (1 if -1 in labels else 0)
    print(f"{name}: {n} clusters found")
```

> [!NOTE]
> K-Means would fail on moons/circles since it assumes clusters are Voronoi cells (spherical). DBSCAN's density-following naturally captures any connected dense region.

---

## Q239. How does DBSCAN handle outliers?

DBSCAN handles outliers **natively and automatically**:

1. Points in sparse regions (far from any dense neighborhood) are labeled **-1 (noise)**
2. No outlier preprocessing needed
3. Outliers **don't affect cluster centroids** (unlike K-Means)

```python
from sklearn.datasets import make_blobs
import numpy as np

# Add outliers to data
X_clean, _ = make_blobs(n_samples=200, centers=3, random_state=42)
outliers = np.array([[10, 10], [-10, -10], [10, -10]])
X = np.vstack([X_clean, outliers])

dbscan = DBSCAN(eps=1.0, min_samples=5)
labels = dbscan.fit_predict(X)

# Outliers automatically labeled as -1
print(f"Outlier labels: {labels[-3:]}")  # Should be [-1, -1, -1]
```

**Using DBSCAN purely for outlier detection:**
```python
from sklearn.preprocessing import StandardScaler

X_scaled = StandardScaler().fit_transform(X)
labels = DBSCAN(eps=0.5, min_samples=5).fit_predict(X_scaled)
outlier_mask = labels == -1
```

---

## Q240. How do you choose epsilon?

The most principled method is the **k-distance plot**:

```python
from sklearn.neighbors import NearestNeighbors
import numpy as np
import matplotlib.pyplot as plt

# Use k = min_samples - 1
k = 4  # if min_samples=5

neigh = NearestNeighbors(n_neighbors=k)
neigh.fit(X_scaled)
distances, _ = neigh.kneighbors(X_scaled)

# Sort k-distances in descending order
k_distances = np.sort(distances[:, -1])[::-1]

plt.plot(k_distances)
plt.xlabel('Points (sorted by distance)')
plt.ylabel(f'{k}-NN Distance')
plt.title('K-Distance Plot')
plt.axhline(y=0.5, color='red', linestyle='--', label='ε = 0.5')
plt.legend()
plt.show()
```

**Reading the plot:** Look for the **"knee"** (sharp bend) in the curve — the distance at the knee is a good choice for ε.

> [!TIP]
> Use `sklearn.preprocessing.StandardScaler` before plotting. The k-distance plot only makes sense for properly scaled data.

---

## Q241. What is a k-distance plot?

A **k-distance plot** (also called k-NN distance graph) plots the distance from each point to its **k-th nearest neighbor**, sorted in descending order.

**Interpretation:**
- **Flat region** at the top: outliers (far from k-th neighbor)
- **Sharp knee**: transition from outliers to cluster points — this is the **optimal ε**
- **Flat region** at the bottom: dense core points (close to k-th neighbor)

```python
from sklearn.neighbors import NearestNeighbors
from kneed import KneeLocator

neigh = NearestNeighbors(n_neighbors=5)
neigh.fit(X_scaled)
distances, _ = neigh.kneighbors(X_scaled)
k_dists = np.sort(distances[:, -1])

# Automatic knee detection
kl = KneeLocator(range(len(k_dists)), k_dists,
                  curve='convex', direction='decreasing')
optimal_eps = k_dists[kl.knee]
print(f"Suggested ε: {optimal_eps:.4f}")
```

**Why use k = min_samples - 1?**  
This mimics the exact distance threshold used in DBSCAN's core point definition.

---

## Q242. Why does DBSCAN struggle with varying density?

DBSCAN uses **global** ε and `min_samples` parameters, which define a single density threshold:

**Problem:** If clusters have different densities:
- ε large enough for sparse clusters → merges dense clusters together
- ε small enough for dense clusters → sparse cluster points labeled as noise

```python
# Dense cluster: 100 tightly packed points
# Sparse cluster: 50 loosely spread points
# → No single ε works well for both!

from sklearn.datasets import make_blobs
import numpy as np

X1 = np.random.randn(200, 2) * 0.2   # dense
X2 = np.random.randn(100, 2) * 2.0 + [5, 5]  # sparse
X = np.vstack([X1, X2])

# DBSCAN with ε=0.3: misses sparse cluster
# DBSCAN with ε=1.5: merges everything
```

**Solutions:**
- **HDBSCAN** (Hierarchical DBSCAN): Handles varying density natively
- **OPTICS**: Orders points by density, extracts clusters at multiple ε thresholds

```python
# pip install hdbscan
import hdbscan

clusterer = hdbscan.HDBSCAN(min_cluster_size=10)
labels = clusterer.fit_predict(X)
```

> [!IMPORTANT]
> HDBSCAN is generally preferred over DBSCAN in practice — it handles varying density, requires fewer parameter choices, and is more robust.
