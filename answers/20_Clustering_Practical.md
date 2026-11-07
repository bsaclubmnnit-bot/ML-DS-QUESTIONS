# Section 20: Clustering Practical Examples

## Q243. How would you preprocess customer data for clustering?

**Step-by-step preprocessing pipeline:**

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer

# Define feature types
numeric_features = ['age', 'income', 'purchase_frequency', 'avg_basket_size']
categorical_features = ['region', 'membership_tier']

# Preprocessing pipeline
numeric_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(drop='first', sparse_output=False))
])

preprocessor = ColumnTransformer([
    ('num', numeric_transformer, numeric_features),
    ('cat', categorical_transformer, categorical_features)
])

X_preprocessed = preprocessor.fit_transform(df)
```

Key steps:
1. Handle missing values (impute rather than drop)
2. Encode categorical variables
3. **Scale all features** (critical for distance-based clustering)
4. Optionally apply PCA for dimensionality reduction
5. Remove or cap outliers

---

## Q244. How would you cluster customers for segmentation?

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score
import matplotlib.pyplot as plt

# Find optimal K using elbow + silhouette
inertias, silhouettes = [], []
K_range = range(2, 11)

for k in K_range:
    km = KMeans(n_clusters=k, random_state=42, n_init=10)
    labels = km.fit_predict(X_preprocessed)
    inertias.append(km.inertia_)
    silhouettes.append(silhouette_score(X_preprocessed, labels))

# Plot and choose optimal K
# Fit final model
km_final = KMeans(n_clusters=4, random_state=42, n_init=10)
df['segment'] = km_final.fit_predict(X_preprocessed)

# Profile each cluster
print(df.groupby('segment')[numeric_features].mean())
```

Common customer segments found: High-value loyalists, Bargain hunters, Occasional buyers, Churned customers.

---

## Q245. How do you handle categorical variables in clustering?

**Option 1: One-Hot Encoding** (most common)
```python
from sklearn.preprocessing import OneHotEncoder
enc = OneHotEncoder(sparse_output=False)
X_cat = enc.fit_transform(df[['category_col']])
```

**Option 2: Binary Encoding** (for high cardinality)
```python
import category_encoders as ce
enc = ce.BinaryEncoder()
X_cat = enc.fit_transform(df[['high_card_col']])
```

**Option 3: Gower Distance** (handles mixed types natively)
```python
import gower
dist_matrix = gower.gower_matrix(df)
from sklearn.cluster import AgglomerativeClustering
model = AgglomerativeClustering(metric='precomputed', linkage='average')
labels = model.fit_predict(dist_matrix)
```

**Option 4: K-Modes / K-Prototypes** (for purely/mixed categorical data)
```python
from kmodes.kprototypes import KPrototypes
kp = KPrototypes(n_clusters=4)
labels = kp.fit_predict(df.values, categorical=[2, 3])  # specify cat column indices
```

---

## Q246. How do you evaluate whether clusters are useful?

**Internal metrics (no ground truth needed):**

| Metric | Good Value | Notes |
|--------|-----------|-------|
| **Silhouette Score** | Close to +1 | Measures cohesion vs separation |
| **Davies-Bouldin Index** | Close to 0 | Lower = better |
| **Calinski-Harabasz** | Higher = better | Ratio of between/within cluster dispersion |
| **Inertia (WCSS)** | Lower = better | Elbow method |

```python
from sklearn.metrics import silhouette_score, davies_bouldin_score, calinski_harabasz_score

print("Silhouette:", silhouette_score(X, labels))
print("Davies-Bouldin:", davies_bouldin_score(X, labels))
print("Calinski-Harabasz:", calinski_harabasz_score(X, labels))
```

**External validation (if ground truth exists):**
- Adjusted Rand Index
- Normalized Mutual Information

**Business validation:** Do clusters make intuitive sense? Are they actionable?

---

## Q247. How do you explain clusters to stakeholders?

**1. Profile each cluster with descriptive statistics:**
```python
cluster_profiles = df.groupby('cluster').agg({
    'age': 'mean',
    'income': 'mean',
    'purchase_freq': 'mean',
    'lifetime_value': 'mean'
}).round(2)
```

**2. Give each cluster a business-friendly name:**
- "High-Value Loyalists" (high income, high frequency)
- "Deal Seekers" (low income, high frequency during sales)
- "Occasional Splurgers" (high income, low frequency)

**3. Use visualizations:**
```python
import seaborn as sns
# Radar/spider chart for multi-dimensional comparison
# Bar charts for cluster sizes
# Scatter plots with cluster coloring
```

**4. Focus on actionability:** "Cluster 2 customers respond well to email promotions — we should target 23% of our base with this campaign."

---

## Q248. How do you choose between K-Means and DBSCAN?

| Factor | K-Means | DBSCAN |
|--------|---------|--------|
| **Cluster shape** | Spherical/convex | Arbitrary shapes |
| **Number of clusters** | Must specify K | Automatically determined |
| **Outlier handling** | Assigns all points | Labels outliers as noise |
| **Scalability** | Very fast (O(nKd)) | Slower for high-density data |
| **Density** | Assumes similar sizes | Handles varying density (but struggles with extreme variation) |
| **Use case** | Customer segmentation, image compression | Anomaly detection, geospatial clustering |

**Decision rule:**
- Known K, spherical clusters, large data → **K-Means**
- Unknown K, irregular shapes, noise present → **DBSCAN**
- Hierarchical structure needed → **Hierarchical Clustering**

---

## Q249. How can PCA help clustering?

**Benefits of applying PCA before clustering:**
1. **Reduces dimensionality** → fewer dimensions = faster clustering
2. **Removes noise** → only principal components capture variance
3. **Removes multicollinearity** → PCA components are orthogonal
4. **Enables 2D/3D visualization** of clusters

```python
from sklearn.decomposition import PCA
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Reduce to 2D for visualization
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

# Cluster in PCA space
km = KMeans(n_clusters=4, random_state=42)
labels = km.fit_predict(X_pca)

# Visualize
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=labels, cmap='tab10')
plt.xlabel(f'PC1 ({pca.explained_variance_ratio_[0]:.1%} variance)')
plt.ylabel(f'PC2 ({pca.explained_variance_ratio_[1]:.1%} variance)')
plt.title('Customer Segments in PCA Space')
plt.show()
```

**Rule of thumb:** Keep enough components to explain 80-95% of variance.

---

## Q250. How do you handle outliers before clustering?

**Why it matters:** K-Means centroids are pulled toward outliers; outliers can form their own spurious clusters.

**Detection methods:**
```python
from scipy import stats
import numpy as np

# Z-score method
z_scores = np.abs(stats.zscore(X_scaled))
outlier_mask = (z_scores > 3).any(axis=1)
print(f"Outliers detected: {outlier_mask.sum()}")

# IQR method
Q1 = np.percentile(X_scaled, 25, axis=0)
Q3 = np.percentile(X_scaled, 75, axis=0)
IQR = Q3 - Q1
outlier_mask = ((X_scaled < Q1 - 1.5 * IQR) | (X_scaled > Q3 + 1.5 * IQR)).any(axis=1)
```

**Strategies:**
| Strategy | Description |
|----------|-------------|
| **Remove outliers** | If they are data errors |
| **Use DBSCAN first** | Outliers labeled as noise, then cluster clean data with K-Means |
| **Cap/Winsorize** | Replace extreme values with percentile boundaries |
| **Use robust algorithms** | K-Medoids (PAM) is more robust than K-Means to outliers |

```python
# Winsorize to 1st-99th percentile
from scipy.stats.mstats import winsorize
X_winsorized = winsorize(X_scaled, limits=[0.01, 0.01], axis=0)
```

