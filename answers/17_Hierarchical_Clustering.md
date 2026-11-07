# Section 17: Hierarchical Clustering

---

## Q216. What is Hierarchical Clustering?

**Hierarchical Clustering** is an unsupervised algorithm that builds a **tree of nested clusters** (a hierarchy) without requiring K to be specified upfront.

**Two main approaches:**
- **Agglomerative** (bottom-up): Start with each point as its own cluster, merge closest pairs
- **Divisive** (top-down): Start with one cluster containing all points, recursively split

**Key advantages:**
- No need to specify K in advance
- Produces a full hierarchy (dendrogram) for visualization
- Can capture nested cluster structure

```python
from sklearn.cluster import AgglomerativeClustering

# Agglomerative with Ward linkage
hc = AgglomerativeClustering(n_clusters=3, linkage='ward')
labels = hc.fit_predict(X)
```

> [!NOTE]
> Hierarchical clustering is particularly useful when you want to understand the structure of your data at multiple levels of granularity.

---

## Q217. What is agglomerative clustering?

**Agglomerative clustering** is a **bottom-up** hierarchical approach:

**Algorithm:**
```
1. Initialize: Each of N points = its own cluster (N clusters)
2. Compute pairwise distances between all clusters
3. Merge the two closest clusters into one
4. Update distances between the new cluster and remaining clusters
5. Repeat steps 3–4 until only 1 cluster remains (or desired K is reached)
```

```python
from scipy.cluster.hierarchy import linkage, dendrogram
import matplotlib.pyplot as plt

# Compute linkage matrix
Z = linkage(X, method='ward')

# Plot dendrogram
plt.figure(figsize=(12, 5))
dendrogram(Z, truncate_mode='level', p=5)
plt.xlabel('Sample index')
plt.ylabel('Distance')
plt.title('Agglomerative Clustering Dendrogram')
plt.show()
```

**Complexity:** O(n² log n) time, O(n²) space — **does not scale well** to very large datasets.

---

## Q218. What is divisive clustering?

**Divisive clustering** is a **top-down** hierarchical approach:

**Algorithm:**
```
1. Start: All N points in one cluster
2. Split: Divide the cluster into two sub-clusters (using K-Means, K=2, or other methods)
3. Recursively split each sub-cluster until each point is its own cluster
```

| Feature | Agglomerative | Divisive |
|---|---|---|
| Direction | Bottom-up | Top-down |
| Common | Very common (sklearn) | Less common |
| Complexity | O(n³) naive | O(2ⁿ) naive |
| Efficiency | Moderate | Less efficient |

> [!NOTE]
> Divisive clustering (DIANA algorithm) is less commonly implemented in standard libraries. Agglomerative is almost always preferred in practice.

---

## Q219. What is a dendrogram?

A **dendrogram** is a tree diagram that represents the **complete hierarchy** of cluster merges (agglomerative) or splits (divisive).

- **X-axis**: Data points (or cluster labels)
- **Y-axis**: Distance/dissimilarity at which clusters merge
- **Horizontal lines**: Merge events — height indicates merge distance

```python
from scipy.cluster.hierarchy import linkage, dendrogram
import matplotlib.pyplot as plt

Z = linkage(X_scaled, method='ward', metric='euclidean')

plt.figure(figsize=(14, 6))
dn = dendrogram(
    Z,
    leaf_rotation=90,
    leaf_font_size=8,
    color_threshold=7.5  # horizontal line to cut at
)
plt.axhline(y=7.5, color='red', linestyle='--', label='Cut point')
plt.title('Hierarchical Clustering Dendrogram')
plt.xlabel('Sample index')
plt.ylabel('Euclidean Distance')
plt.legend()
plt.tight_layout()
plt.show()
```

**Reading a dendrogram:** A **horizontal cut** at any height gives a particular clustering — the number of vertical lines the cut crosses = number of clusters.

---

## Q220. What is single linkage?

**Single linkage** (nearest neighbor) defines the distance between two clusters as the **minimum distance** between any pair of points, one from each cluster:

```
d(A, B) = min { dist(a, b) : a ∈ A, b ∈ B }
```

```python
hc = AgglomerativeClustering(n_clusters=3, linkage='single')
```

**Properties:**
- **Chaining effect**: Can create long, "stringy" clusters that chain together
- Good at detecting elongated clusters
- Very sensitive to outliers (a single outlier can chain two large clusters)

```
Cluster A: ●●●●           ●  ←-- outlier connected
Cluster B:              ●●●●●●
Single linkage merges A and B early due to the outlier bridge
```

---

## Q221. What is complete linkage?

**Complete linkage** (furthest neighbor) defines the distance between clusters as the **maximum distance** between any pair of points:

```
d(A, B) = max { dist(a, b) : a ∈ A, b ∈ B }
```

```python
hc = AgglomerativeClustering(n_clusters=3, linkage='complete')
```

**Properties:**
- Produces **compact, roughly equal-sized clusters**
- Avoids the chaining problem of single linkage
- More robust to outliers than single linkage
- Biased toward finding **spherical clusters**
- Can break large, valid clusters to enforce compactness

> [!TIP]
> Complete linkage is a good default when you want more balanced clusters without the chaining problem.

---

## Q222. What is average linkage?

**Average linkage** defines cluster distance as the **mean distance** between all pairs of points, one from each cluster:

```
d(A, B) = (1/|A||B|) · Σₐ∈A Σᵦ∈B dist(a, b)
```

```python
hc = AgglomerativeClustering(n_clusters=3, linkage='average')
```

**Properties:**
- A **compromise** between single and complete linkage
- Less susceptible to chaining than single linkage
- Less biased toward compact clusters than complete linkage
- More robust to outliers than single linkage

| Linkage | Sensitive to Outliers | Chaining | Compact Clusters |
|---|---|---|---|
| Single | High | Yes | No |
| Complete | Moderate | No | Yes |
| Average | Low-Moderate | No | Moderate |
| Ward | Low | No | Yes |

---

## Q223. What is Ward linkage?

**Ward linkage** merges the pair of clusters that results in the **minimum increase in total within-cluster variance (WCSS)**:

```
Δ(A, B) = WCSS(A∪B) - WCSS(A) - WCSS(B)
         = (|A|·|B|)/(|A|+|B|) · ||μₐ - μᵦ||²
```

```python
hc = AgglomerativeClustering(n_clusters=3, linkage='ward')
```

**Properties:**
- Produces the most **compact, well-separated clusters**
- Equivalent to minimizing the K-Means objective greedily
- Generally the **best-performing linkage** for most datasets
- Works best with **Euclidean distance** (only supported metric for Ward in sklearn)

> [!IMPORTANT]
> Ward linkage is the **recommended default** for most clustering tasks. It consistently produces natural, well-separated clusters.

---

## Q224. How do you choose clusters from a dendrogram?

Three main approaches to extract a flat clustering from a dendrogram:

**1. Cut at a fixed height:**
```python
from scipy.cluster.hierarchy import fcluster

Z = linkage(X_scaled, method='ward')
labels = fcluster(Z, t=7.5, criterion='distance')  # cut at height 7.5
```

**2. Specify number of clusters:**
```python
labels = fcluster(Z, t=3, criterion='maxclust')  # get exactly 3 clusters
```

**3. Visual inspection — find the longest vertical lines:**
- Look for the **largest gap** between consecutive merge heights
- Draw a horizontal line through the gap
- Number of vertical lines crossed = number of clusters

```python
# Find optimal cut automatically
heights = Z[:, 2]  # merge heights
diffs = np.diff(heights)
best_cut_idx = np.argmax(diffs)
cut_height = (heights[best_cut_idx] + heights[best_cut_idx + 1]) / 2

labels = fcluster(Z, t=cut_height, criterion='distance')
print(f"Suggested K: {len(np.unique(labels))}")
```

---

## Q225. What are Hierarchical Clustering limitations?

| Limitation | Details |
|---|---|
| **Scalability** | O(n²) memory and O(n³) or O(n² log n) time — slow for n > 10,000 |
| **Irreversible merges** | Once merged, clusters cannot be split (agglomerative) |
| **No global objective** | Each step is locally greedy, not globally optimal |
| **Sensitivity to noise/outliers** | Especially with single linkage |
| **Linkage choice matters** | Results vary significantly with linkage method |
| **No natural K** | Still requires judgment to cut the dendrogram |
| **Euclidean only (Ward)** | Ward linkage only works with Euclidean distance |

**Alternatives for large datasets:**
```python
# BIRCH: scalable hierarchical clustering
from sklearn.cluster import Birch
birch = Birch(n_clusters=3)
birch.fit(X)

# Mini-batch K-Means for very large datasets
from sklearn.cluster import MiniBatchKMeans
mb_kmeans = MiniBatchKMeans(n_clusters=3)
mb_kmeans.fit(X)
```

> [!CAUTION]
> Avoid hierarchical clustering for datasets with more than ~10,000 samples — the quadratic memory requirement will be prohibitive.
