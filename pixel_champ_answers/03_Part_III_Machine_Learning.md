# Part III: Machine Learning

> **255 Interview Questions & Comprehensive Technical Solutions**  
> *Topics: Supervised/Unsupervised Learning, Regression, Classification, Trees, Ensembles, Random Forest, XGBoost, Clustering*  
> *Part of the [PIXEL CHAMP Master Question Bank](https://github.com/bsaclubmnnit-bot/ML-DS-QUESTIONS)*

---

## ML-001: How do pipelines prevent data leakage?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Data leakage** occurs when test data information influences preprocessing (e.g., fitting a scaler on the entire dataset before splitting).

A `Pipeline` ensures preprocessing is **fit only on training data** and applied to test data:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('model', LinearRegression())
])

# During cross-validation, scaler is fit ONLY on training fold
scores = cross_val_score(pipe, X, y, cv=5, scoring='r2')
```

Without a pipeline, fitting the scaler on all data before CV would leak test statistics into training.

---

---

## ML-002: How does cross-validation work for regression?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

Cross-validation estimates model performance on unseen data by training and evaluating multiple times on different splits:

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LinearRegression

model = LinearRegression()
scores = cross_val_score(model, X, y, cv=5, scoring='neg_root_mean_squared_error')
print("Mean RMSE:", -scores.mean())
print("Std:", scores.std())
```

**K-Fold CV steps:**
1. Split data into K equal folds
2. Train on K-1 folds, validate on 1
3. Repeat K times (each fold used as validation once)
4. Average the K validation scores

For time series, use `TimeSeriesSplit` to maintain temporal order.

---

---

## ML-003: What are features and target variables?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Features (X):**
- Also called: independent variables, predictors, input variables, attributes, covariates.
- These are the **inputs** fed into the model.
- Can be numerical (age, salary), categorical (gender, country), or text/image data.
- Represented as a matrix of shape `(n_samples, n_features)`.

**Target Variable (y):**
- Also called: dependent variable, label, output variable, response variable.
- This is what the model is trying to **predict**.
- In regression: continuous value (e.g., house price)
- In classification: discrete class label (e.g., 0 or 1)
- Represented as a vector of shape `(n_samples,)`.

```python
import pandas as pd

df = pd.read_csv('housing.csv')

# Features (inputs)
X = df[['square_feet', 'num_bedrooms', 'location_score']]

# Target (output to predict)
y = df['price']
```

**Feature Engineering** is the process of creating or transforming features to improve model performance — one of the most impactful steps in ML.

---

---

## ML-004: What is MAE?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Mean Absolute Error** = average of absolute differences between predictions and actuals:
$$\text{MAE} = \frac{1}{n}\sum_{i=1}^n |y_i - \hat{y}_i|$$

- Robust to outliers (unlike MSE)
- Same unit as the target variable
- Intuitive: "on average, predictions are off by X units"

```python
from sklearn.metrics import mean_absolute_error
mae = mean_absolute_error(y_test, y_pred)
```

---

---

## ML-005: What is MSE?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Mean Squared Error** = average of squared differences:
$$\text{MSE} = \frac{1}{n}\sum_{i=1}^n (y_i - \hat{y}_i)^2$$

- Heavily penalizes large errors (squaring amplifies outliers)
- Differentiable, making it useful for optimization
- Unit is the square of the target variable

```python
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(y_test, y_pred)
```

---

---

## ML-006: What is RMSE?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Root Mean Squared Error** = square root of MSE:
$$\text{RMSE} = \sqrt{\frac{1}{n}\sum_{i=1}^n (y_i - \hat{y}_i)^2}$$

- Same unit as the target variable (unlike MSE)
- More sensitive to outliers than MAE
- Most commonly reported metric for regression

```python
import numpy as np
rmse = np.sqrt(mean_squared_error(y_test, y_pred))
# Or in newer sklearn:
rmse = mean_squared_error(y_test, y_pred, squared=False)
```

---

---

## ML-007: What is a decision boundary?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

A **decision boundary** is the surface (line, plane, or hyperplane) that **separates different classes** in the feature space. Points on different sides of the boundary are assigned to different classes.

- In **binary classification** with 2 features: it's a line in 2D space.
- In **3 features**: it's a plane in 3D space.
- In **n features**: it's a hyperplane in n-dimensional space.
- For non-linear classifiers (SVM with RBF kernel, neural networks): the boundary can be curved/non-linear.

**Examples:**
- **Logistic Regression**: Linear decision boundary → `θᵀx = 0`
- **SVM**: Optimal margin hyperplane
- **Decision Tree**: Axis-aligned rectangular boundaries
- **Neural Network**: Complex, non-linear boundaries

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression

# Visualize decision boundary (2D)
model = LogisticRegression()
model.fit(X_train, y_train)

x_min, x_max = X[:, 0].min() - 1, X[:, 0].max() + 1
y_min, y_max = X[:, 1].min() - 1, X[:, 1].max() + 1
xx, yy = np.meshgrid(np.linspace(x_min, x_max, 200),
                     np.linspace(y_min, y_max, 200))
Z = model.predict(np.c_[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)
plt.contourf(xx, yy, Z, alpha=0.4)
plt.scatter(X[:, 0], X[:, 1], c=y, edgecolors='k')
plt.title("Decision Boundary")
plt.show()
```

---

---

## ML-008: What is a loss function?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

A **loss function** (also called a **cost function** per-sample) measures **how wrong a single prediction is** compared to the true label. It quantifies the error for one training example.

- It's a function `L(ŷ, y)` where `ŷ` is predicted and `y` is actual.
- Lower loss = better prediction.
- The model is trained to **minimize** the total loss over the dataset.

**Common loss functions:**

| Task | Loss Function | Formula |
|------|--------------|---------|
| Regression | MSE | `(ŷ - y)²` |
| Regression | MAE | `|ŷ - y|` |
| Binary Classification | Binary Cross-Entropy | `-[y·log(ŷ) + (1-y)·log(1-ŷ)]` |
| Multiclass | Categorical Cross-Entropy | `-Σ yᵢ·log(ŷᵢ)` |

```python
import numpy as np

# MSE loss for regression
def mse_loss(y_true, y_pred):
    return np.mean((y_true - y_pred) ** 2)

# Binary cross-entropy loss
def binary_cross_entropy(y_true, y_pred):
    eps = 1e-15
    y_pred = np.clip(y_pred, eps, 1 - eps)
    return -np.mean(y_true * np.log(y_pred) + (1 - y_true) * np.log(1 - y_pred))
```

The choice of loss function depends on the task and the desired behavior of the model.

---

---

## ML-009: What is an objective function?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

An **objective function** is the broader function that the optimization algorithm seeks to **minimize (or maximize)** during training. It can include:

1. **Loss function** – measures prediction error
2. **Regularization term** – penalizes model complexity

> **Objective Function = Loss Function + Regularization**

For example, in Ridge Regression:
```
Objective = Σ(yᵢ - ŷᵢ)² + λ·Σθⱼ²
            ↑ Loss (MSE)    ↑ L2 Regularization
```

In Lasso Regression:
```
Objective = Σ(yᵢ - ŷᵢ)² + λ·Σ|θⱼ|
```

**Loss function vs. Objective function:**
- **Loss function** = per-sample or average prediction error only
- **Objective function** = what the optimizer actually minimizes (may include regularization or other terms)

In practice, these terms are often used interchangeably, but technically the objective function is the more general concept.

---

---

## ML-010: What is binary classification?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Binary classification** is a classification task where there are exactly **two possible output classes**.

- The model assigns each input to one of two mutually exclusive categories.
- Typically labeled as `0/1`, `True/False`, or `Positive/Negative`.

**Examples:**
- Email: Spam (1) vs. Not Spam (0)
- Medical: Disease present (1) vs. Absent (0)
- Fraud: Fraudulent (1) vs. Legitimate (0)

**Common algorithms:** Logistic Regression, SVM, Decision Tree, Naive Bayes

```python
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import make_classification

X, y = make_classification(n_samples=1000, n_classes=2, random_state=42)
model = LogisticRegression()
model.fit(X, y)
# y contains only 0 or 1
```

The output is typically a **probability** `P(y=1 | X)`, which is thresholded (usually at 0.5) to produce the final class label.

---

---

## ML-011: What is empirical risk minimization?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Empirical Risk Minimization (ERM)** is the principle of finding model parameters that **minimize the average loss over the training dataset**.

Since we can't compute the true expected risk (we don't know the full data distribution), we approximate it using the **empirical risk** — the average loss on our observed (empirical) training data:

```
Empirical Risk = (1/n) · Σᵢ L(f(xᵢ; θ), yᵢ)
```

Where:
- `n` = number of training samples
- `L` = loss function
- `f(xᵢ; θ)` = model prediction
- `yᵢ` = true label

**The ERM principle:** Choose `θ*` that minimizes the empirical risk:
```
θ* = argmin_θ (1/n) · Σᵢ L(f(xᵢ; θ), yᵢ)
```

**Key concern:** Minimizing training error too aggressively leads to **overfitting**. Regularization is added to the objective to combat this (this is called **Structural Risk Minimization**).

---

---

## ML-012: What is generalization?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Generalization** is a model's ability to perform well on **new, unseen data** that was not used during training.

- A model that generalizes well has learned the **underlying patterns** in the data, not just memorized the training examples.
- It is the fundamental goal of machine learning.

**Generalization error** = True Risk – Empirical Risk (gap between test and train performance)

**Factors affecting generalization:**
- **Model complexity**: Too simple → underfits; too complex → overfits
- **Training data size**: More data generally improves generalization
- **Data quality**: Noisy data harms generalization
- **Regularization**: Helps constrain the model for better generalization

**How to measure generalization:**
1. **Hold-out validation**: Set aside a test set not used in training
2. **Cross-validation**: k-fold CV gives a robust estimate of generalization
3. **Learning curves**: Plot train vs. validation error as training data grows

> A well-generalizing model finds the sweet spot on the **bias-variance tradeoff** — neither underfitting nor overfitting.

---

---

## ML-013: What is multiclass classification?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Multiclass classification** involves predicting one class from **more than two possible classes**, where each sample belongs to exactly one class.

- Each input maps to exactly one of `k > 2` classes.

**Examples:**
- Handwritten digit recognition: digits 0–9 (10 classes)
- Image classification: cat, dog, bird, car, etc.
- Language identification: English, French, Spanish, etc.

**Strategies:**
- **One-vs-Rest (OvR):** Train `k` binary classifiers, one per class.
- **One-vs-One (OvO):** Train `k(k-1)/2` classifiers for each pair of classes.
- **Native multiclass:** Algorithms like Decision Trees, Random Forests, and Neural Networks (with softmax) handle multiclass natively.

```python
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris

X, y = load_iris(return_X_y=True)
# y has 3 classes: 0, 1, 2
model = LogisticRegression(multi_class='multinomial', solver='lbfgs')
model.fit(X, y)
print(model.predict([[5.1, 3.5, 1.4, 0.2]]))  # e.g., [0]
```

---

---

## ML-014: What is multilabel classification?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Multilabel classification** is where each sample can belong to **multiple classes simultaneously** (non-mutually exclusive).

- Unlike multiclass (one label per sample), multilabel assigns a **subset of labels** to each sample.

**Examples:**
- A news article tagged as both "Sports" and "Finance"
- A movie with genres: "Action", "Adventure", "Sci-Fi"
- An image containing: a dog, a tree, and a car

**Approaches:**
- **Binary Relevance:** Train one binary classifier per label independently.
- **Classifier Chains:** Chain classifiers so each uses previous predictions as features.
- **Label Powerset:** Treat each unique label combination as a single class.

```python
from sklearn.multiclass import OneVsRestClassifier
from sklearn.linear_model import LogisticRegression
import numpy as np

# y is a binary matrix of shape (n_samples, n_labels)
y = np.array([[1, 0, 1], [0, 1, 1], [1, 1, 0]])
X = np.random.rand(3, 5)

model = OneVsRestClassifier(LogisticRegression())
model.fit(X, y)
```

> **Key distinction:** Multiclass → one label per sample. Multilabel → zero or more labels per sample.

---

---

## ML-015: What is overfitting?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Overfitting** is when a model **memorizes the training data**, including its noise and outliers, and fails to generalize to new data.

- Direct result of **high variance**
- The model is too closely fitted to the training examples

**Signs:**
- Very high training accuracy
- Low test/validation accuracy
- Big gap between train and test performance

**Example:**
```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split

X, y = make_classification(n_samples=200, random_state=42)
X_train, X_test, y_train, y_test = train_test_split(X, y)

model = DecisionTreeClassifier(max_depth=None)  # no limit — overfits
model.fit(X_train, y_train)

print("Train:", model.score(X_train, y_train))  # ~1.0
print("Test:", model.score(X_test, y_test))      # much lower
```

**Fix:** Regularization, more data, pruning, dropout, cross-validation.

---

---

## ML-016: What is regularization?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Regularization** is a set of techniques used to **reduce overfitting** by adding a penalty term to the objective function that discourages the model from learning overly complex patterns.

**General form:**
```
Objective = Loss + λ · Penalty(θ)
```

Where `λ` (lambda) is the **regularization strength** hyperparameter.

**Common types:**

| Type | Penalty | Effect |
|------|---------|--------|
| L2 (Ridge) | `λ·Σθⱼ²` | Shrinks coefficients toward zero |
| L1 (Lasso) | `λ·Σ\|θⱼ\|` | Drives some coefficients to exactly zero (sparse) |
| Elastic Net | `λ₁·Σ\|θⱼ\| + λ₂·Σθⱼ²` | Combination of L1 and L2 |
| Dropout | Random neuron deactivation | For neural networks |
| Early Stopping | Stop training early | For iterative methods |

**Effect on bias-variance tradeoff:**
- More regularization → higher bias, lower variance
- Less regularization → lower bias, higher variance

```python
from sklearn.linear_model import Ridge, Lasso

# L2 regularization
ridge = Ridge(alpha=1.0)  # alpha = lambda

# L1 regularization
lasso = Lasso(alpha=0.1)
```

---

---

## ML-017: What is the difference between parametric and non-parametric models?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Parametric Models** assume a **fixed functional form** for the data distribution. They have a fixed, finite number of parameters that don't grow with the training data.

- **Examples:** Linear Regression, Logistic Regression, Naive Bayes, Linear SVM
- **Pros:** Fast training/inference, require less data, interpretable
- **Cons:** Strong assumptions; poor fit if assumptions are wrong (high bias)

**Non-Parametric Models** make **fewer assumptions** about the data distribution. The complexity (number of effective parameters) can grow with the training data.

- **Examples:** k-Nearest Neighbors, Decision Trees, Random Forests, Kernel SVM, Gaussian Processes
- **Pros:** Flexible, can fit complex patterns
- **Cons:** Slower, require more data, risk overfitting, less interpretable

| Aspect | Parametric | Non-Parametric |
|--------|-----------|----------------|
| Parameters | Fixed number | Grows with data |
| Assumptions | Strong | Fewer/weaker |
| Training speed | Fast | Slower |
| Data required | Less | More |
| Flexibility | Lower | Higher |
| Bias-Variance | Higher bias | Higher variance |
| Examples | Linear Regression | kNN, Decision Tree |

> **Note:** "Non-parametric" doesn't mean no parameters — it means the number of parameters is not fixed in advance and can scale with data size.

---

## ML-018: What is the difference between regression and classification?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

Both are **supervised learning** tasks, but they differ in the type of output they predict.

**Regression** predicts a **continuous numerical value**.
- Examples: Predicting house prices, stock prices, temperature, age
- Output: `ŷ ∈ ℝ` (any real number)
- Common algorithms: Linear Regression, Ridge, Lasso, SVR, Random Forest Regressor
- Metrics: MAE, MSE, RMSE, R²

**Classification** predicts a **discrete class label**.
- Examples: Spam vs. not spam, digit recognition (0–9), sentiment (positive/negative/neutral)
- Output: `ŷ ∈ {class_1, class_2, ..., class_k}`
- Common algorithms: Logistic Regression, Decision Trees, SVM, kNN, Neural Networks
- Metrics: Accuracy, Precision, Recall, F1, AUC-ROC

```python
# Regression example
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train, y_train)  # y_train contains continuous values

# Classification example
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
model.fit(X_train, y_train)  # y_train contains class labels
```

---

---

## ML-019: What is the difference between supervised learning and unsupervised learning?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Supervised Learning** trains a model on **labeled data** — each input `X` has a corresponding output `y`. The model learns to map inputs to outputs.

- Examples: Linear Regression, Logistic Regression, Decision Trees, SVMs, Neural Networks
- Goal: Predict output for unseen inputs
- Use cases: Spam detection, house price prediction, image classification

**Unsupervised Learning** trains a model on **unlabeled data** — only inputs `X` are available, with no corresponding outputs.

- Examples: K-Means, DBSCAN, PCA, Autoencoders
- Goal: Discover hidden structure, patterns, or representations in data
- Use cases: Customer segmentation, anomaly detection, dimensionality reduction

| Aspect | Supervised | Unsupervised |
|--------|-----------|--------------|
| Labels | Required | Not required |
| Goal | Predict output | Find structure |
| Evaluation | Straightforward (accuracy, MSE) | Harder to evaluate |
| Examples | Classification, Regression | Clustering, Dimensionality Reduction |

> **Semi-supervised learning** is a hybrid: a small amount of labeled data + large amount of unlabeled data. Self-supervised learning (e.g., BERT pretraining) generates pseudo-labels from the data itself.

---

---

## ML-020: What is underfitting?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** HIGH

**Underfitting** is when a model is **too simple** to learn the underlying structure of the data — it performs poorly on both training and test sets.

- Direct result of **high bias**
- The model fails to capture important patterns

**Signs:**
- Low training accuracy
- Low test accuracy
- Learning curve plateaus at high error early

**Example:**
```python
# Fitting a line to clearly non-linear data
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1],[2],[3],[4],[5]])
y = np.array([1, 4, 9, 16, 25])  # quadratic relationship

model = LinearRegression().fit(X, y)
print(model.score(X, y))  # R² will be low — underfitting
```

**Fix:** Use a more complex model, add features, or reduce regularization.

---

---

## ML-021: How do you encode categorical variables?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

| Encoding | Use Case | Notes |
|----------|----------|-------|
| **One-Hot Encoding** | Nominal (no order) | Drops one column to avoid multicollinearity |
| **Ordinal Encoding** | Ordinal (e.g., Low/Med/High) | Preserves order |
| **Label Encoding** | Tree-based models only | Don't use for linear models |
| **Target Encoding** | High cardinality | Risk of leakage if not done carefully |

```python
from sklearn.preprocessing import OneHotEncoder
enc = OneHotEncoder(drop='first', sparse_output=False)
X_encoded = enc.fit_transform(X[['category_col']])
```

---

---

## ML-022: How do you handle missing values before regression?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

**Strategies:**

| Strategy | When to Use | Code |
|----------|-------------|------|
| Drop rows | Few missing values | `df.dropna()` |
| Mean/Median imputation | Random missing, numerical | `SimpleImputer(strategy='mean')` |
| Mode imputation | Categorical features | `SimpleImputer(strategy='most_frequent')` |
| Forward/Backward fill | Time-series data | `df.fillna(method='ffill')` |
| KNN imputation | Complex patterns | `KNNImputer(n_neighbors=5)` |
| Model-based imputation | Best quality, expensive | `IterativeImputer()` |

```python
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(strategy='median')
X_imputed = imputer.fit_transform(X)
```

Always fit on training data only, transform on both train and test to avoid leakage.

---

---

## ML-023: How do you implement Linear Regression using scikit-learn?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
import numpy as np

# Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train
model = LinearRegression()
model.fit(X_train, y_train)

# Predict
y_pred = model.predict(X_test)

# Evaluate
print("R²:", r2_score(y_test, y_pred))
print("RMSE:", np.sqrt(mean_squared_error(y_test, y_pred)))
print("Coefficients:", model.coef_)
print("Intercept:", model.intercept_)
```

---

---

## ML-024: How do you interpret residuals?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

**Residual** = $y_i - \hat{y}_i$ (actual minus predicted)

**Ideal residual plots:**
- **Residuals vs Fitted**: Random scatter around 0 (no pattern = linearity holds)
- **Q-Q Plot**: Points along diagonal line = normality of errors
- **Scale-Location**: Horizontal band = homoscedasticity
- **Residuals vs Leverage**: Identifies influential outliers

**What patterns indicate:**

| Pattern | Problem |
|---------|---------|
| U-shape or curve | Non-linearity — need polynomial features |
| Fan shape | Heteroscedasticity — consider log transform |
| Systematic shift | Omitted variable bias |
| Outliers with high leverage | Influential points distorting the fit |

```python
import matplotlib.pyplot as plt
residuals = y_test - y_pred
plt.scatter(y_pred, residuals)
plt.axhline(0, color='red', linestyle='--')
plt.xlabel('Predicted'); plt.ylabel('Residuals')
plt.title('Residuals vs Fitted')
plt.show()
```

---

## ML-025: How do you split data for regression?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,      # 80% train, 20% test
    random_state=42     # Reproducibility
)
```

For time-series data, **always split chronologically** (not randomly) to avoid data leakage:
```python
# Time series split
split_idx = int(0.8 * len(df))
train, test = df[:split_idx], df[split_idx:]
```

---

---

## ML-026: What common mistakes occur when applying this technique in production?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What common mistakes occur when applying this technique in production` is an essential technical question in Topic 19: Supervised and Unsupervised Learning.

**Detailed Technical Breakdown:**
- **Foundational Definition:** Serves as a primary building block within data science, statistical modeling, and applied AI workflows.
- **Operational Logic:** Ensures accurate data processing, statistical validity, and reproducible results in both experimental and production environments.
- **Practical Considerations:** Balances computational efficiency, mathematical correctness, and real-world domain constraints.

**Practical Python Snippet:**
```python
# Standard technical idiom for What common mistakes occur when applying this technique in production
import numpy as np

def technical_demonstration():
    return True
```

**Interview Takeaway:**
Explain both the theoretical foundation and practical trade-offs encountered when applying this technique to real-world datasets.

---

## ML-027: What metrics evaluate regression models?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **MAE** | $\frac{1}{n}\sum|y_i - \hat{y}_i|$ | Average absolute error |
| **MSE** | $\frac{1}{n}\sum(y_i - \hat{y}_i)^2$ | Penalizes large errors more |
| **RMSE** | $\sqrt{MSE}$ | Same unit as target |
| **R²** | $1 - \frac{SS_{res}}{SS_{tot}}$ | Proportion of variance explained |
| **Adj. R²** | Adjusted for # features | Better for multiple regression |
| **MAPE** | $\frac{1}{n}\sum\frac{|y_i - \hat{y}_i|}{y_i} \times 100$ | Percentage error |

---

---

## ML-028: When is MAE preferred over RMSE?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

| Prefer MAE | Prefer RMSE |
|-----------|------------|
| Outliers are present and should not dominate | Large errors are particularly undesirable |
| Target variable has heavy-tailed distribution | Smooth optimization is needed |
| Interpretability is key | Penalizing large deviations is important |
| Robust evaluation needed | Standard practice in a domain |

**Rule of thumb:** If large errors are especially bad (e.g., medical dosing), use RMSE. If the data has natural outliers that aren't mistakes, use MAE.

---

---

## ML-029: When should features be standardized?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** MEDIUM

**Standardize when:**
- Algorithm is distance-based (KNN, SVM, k-Means)
- Algorithm uses gradient descent (Linear Regression, Logistic Regression, Neural Networks)
- Using Ridge or Lasso (regularization is scale-sensitive)

**No need to standardize for:**
- Tree-based models (Decision Trees, Random Forest, XGBoost)
- Models that don't compute distances

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)  # Use training stats!
```

---

---

## ML-030: In a real-world project, how would you explain this concept to a non-technical stakeholder?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`In a real-world project, how would you explain this concept to a non-technical stakeholder` is an essential technical question in Topic 19: Supervised and Unsupervised Learning.

**Detailed Technical Breakdown:**
- **Foundational Definition:** Serves as a primary building block within data science, statistical modeling, and applied AI workflows.
- **Operational Logic:** Ensures accurate data processing, statistical validity, and reproducible results in both experimental and production environments.
- **Practical Considerations:** Balances computational efficiency, mathematical correctness, and real-world domain constraints.

**Practical Python Snippet:**
```python
# Standard technical idiom for In a real-world project, how would you explain this concept to a non-technical stakeholder
import numpy as np

def technical_demonstration():
    return True
```

**Interview Takeaway:**
Explain both the theoretical foundation and practical trade-offs encountered when applying this technique to real-world datasets.

---

## ML-031: What is MAPE and what are its limitations?

**Domain:** Topic 19: Supervised and Unsupervised Learning &nbsp;|&nbsp; **Priority:** LOWER

**Mean Absolute Percentage Error:**
$$\text{MAPE} = \frac{100\%}{n} \sum_{i=1}^n \left|\frac{y_i - \hat{y}_i}{y_i}\right|$$

**Advantages:** Scale-independent, easy to explain ("predictions are off by X%")

**Limitations:**
- **Undefined** when $y_i = 0$
- **Asymmetric**: over-forecasting and under-forecasting penalized differently
- **Biased** toward lower predictions for skewed distributions
- **Poor for small values**: 1 unit error on $y=2$ = 50% error

Alternative: **SMAPE** (Symmetric MAPE) handles some of these issues.

---

---

## ML-032: How can multicollinearity be detected?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

Several methods can detect multicollinearity:

**1. Correlation Matrix / Heatmap**
- Look for feature pairs with `|r| > 0.8`
- Simple but only captures pairwise relationships

**2. Variance Inflation Factor (VIF)**
- Most comprehensive method — detects multicollinearity among multiple features

**3. Eigenvalues of XᵀX**
- Very small eigenvalues indicate near-singular matrix (multicollinearity)
- Condition number = `max_eigenvalue / min_eigenvalue`; if > 30, concern

**4. Coefficient instability**
- Large changes in coefficients when removing/adding a variable

```python
import pandas as pd
import numpy as np
from statsmodels.stats.outliers_influence import variance_inflation_factor

# Create design matrix
X = pd.DataFrame({
    'x1': [1, 2, 3, 4, 5],
    'x2': [2, 4, 6, 8, 10],   # perfectly correlated with x1
    'x3': [1, 3, 2, 5, 4]
})

# Compute VIF for each feature
vif_data = pd.DataFrame()
vif_data['Feature'] = X.columns
vif_data['VIF'] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
print(vif_data)
# VIF for x1 and x2 will be very high (→ inf for perfect collinearity)
```

**Remedies:**
- Remove one of the correlated features
- Use Ridge Regression (handles multicollinearity via L2 penalty)
- Apply PCA to decorrelate features
- Collect more data

---

---

## ML-033: What are odds and log-odds?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Odds** = ratio of probability of success to probability of failure:
$$\text{Odds} = \frac{p}{1 - p}$$

**Log-odds (logit)** = natural log of the odds:
$$\text{logit}(p) = \ln\left(\frac{p}{1-p}\right) = w^T x + b$$

Logistic Regression models log-odds as a **linear function** of features. This is why it's called "logistic".

---

---

## ML-034: What does a predicted probability represent?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

$\hat{p} = P(y=1 | x)$ — the probability that the given input belongs to the positive class.

Example: If a spam classifier outputs 0.87, there is an 87% chance the email is spam. This is calibrated if the model is well-trained on representative data.

---

---

## ML-035: What is Adjusted R-squared?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Adjusted R²** is a modified version of R² that **penalizes the addition of features that don't improve the model**, adjusting for the number of predictors.

**Formula:**
```
Adjusted R² = 1 - [(1 - R²)(n - 1) / (n - p - 1)]
```

Where:
- `n` = number of observations
- `p` = number of predictor features

**Why it's better than R²:**
- R² can **only increase** (or stay the same) when features are added, even noise features
- Adjusted R² **increases only if the new feature improves the model more than expected by chance**
- Adjusted R² can **decrease** if an irrelevant feature is added

```python
def adjusted_r2(r2, n, p):
    return 1 - (1 - r2) * (n - 1) / (n - p - 1)

import numpy as np
from sklearn.metrics import r2_score

y_true = np.array([3, 5, 2, 8, 6])
y_pred = np.array([2.8, 5.2, 2.1, 7.9, 6.1])

r2 = r2_score(y_true, y_pred)
n, p = 5, 2

adj_r2 = adjusted_r2(r2, n, p)
print(f"R²: {r2:.4f}")
print(f"Adjusted R²: {adj_r2:.4f}")
```

> **Rule of thumb:** Use Adjusted R² when comparing models with different numbers of features.

---

---

## ML-036: What is Linear Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Linear Regression** is a supervised learning algorithm that models the relationship between one or more input features `X` and a continuous output `y` by fitting a **linear equation** to the data.

**Model form:**
```
ŷ = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ
```
Or in vector form: `ŷ = Xθ`

Where:
- `θ₀` = intercept (bias)
- `θ₁...θₙ` = coefficients (weights) for each feature
- `ŷ` = predicted output

**Goal:** Find the parameters `θ` that minimize the sum of squared differences between predicted and actual values.

```python
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1], [2], [3], [4], [5]])
y = np.array([2.1, 3.9, 6.2, 7.8, 10.1])

model = LinearRegression()
model.fit(X, y)

print(f"Intercept: {model.intercept_:.2f}")   # θ₀
print(f"Coefficient: {model.coef_[0]:.2f}")   # θ₁
print(f"Prediction for x=6: {model.predict([[6]])[0]:.2f}")
```

**Use cases:** House price prediction, salary estimation, demand forecasting, any continuous value prediction.

---

---

## ML-037: What is Logistic Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

Logistic Regression is a supervised learning algorithm used for **binary (and multiclass) classification**. Despite the name "regression", it predicts the probability of a class label using the **logistic (sigmoid) function** to squash a linear combination of features into the [0, 1] range.

$$\hat{y} = \sigma(w^T x + b) = \frac{1}{1 + e^{-(w^T x + b)}}$$

If $\hat{y} \geq 0.5$, predict class 1; else class 0.

---

---

## ML-038: What is Ordinary Least Squares?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Ordinary Least Squares (OLS)** is the standard method for estimating the parameters of a linear regression model by **minimizing the sum of squared residuals**.

**Objective:**
```
Minimize: RSS = Σᵢ (yᵢ - ŷᵢ)² = Σᵢ (yᵢ - θᵀxᵢ)²
```

**Closed-form (Normal Equation) solution:**
```
θ* = (XᵀX)⁻¹ Xᵀy
```

Where `X` is the `(n × p)` design matrix.

```python
import numpy as np

# Manual OLS implementation
X = np.column_stack([np.ones(len(X_raw)), X_raw])  # Add intercept column
theta = np.linalg.inv(X.T @ X) @ X.T @ y
print("OLS Parameters:", theta)
```

**Properties of OLS estimators (Gauss-Markov theorem):**
When the linear regression assumptions hold, OLS is **BLUE** — **Best Linear Unbiased Estimator**:
- **Unbiased:** `E[θ̂] = θ`
- **Best:** Minimum variance among all linear unbiased estimators

**Limitation:** The Normal Equation requires computing `(XᵀX)⁻¹`, which is `O(p³)` — computationally expensive for large numbers of features. Gradient descent is preferred in that case.

---

---

## ML-039: What is R-squared?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**R-squared (R², Coefficient of Determination)** measures the **proportion of variance in the target variable explained by the model**.

**Formula:**
```
R² = 1 - (SS_res / SS_tot)

SS_res = Σ(yᵢ - ŷᵢ)²    (residual sum of squares)
SS_tot = Σ(yᵢ - ȳ)²     (total sum of squares)
```

**Interpretation:**
| R² | Interpretation |
|----|---------------|
| 1.0 | Perfect fit — model explains all variance |
| 0.8 | Model explains 80% of variance |
| 0.0 | Model is no better than predicting the mean |
| < 0 | Model is worse than predicting the mean |

```python
from sklearn.metrics import r2_score
import numpy as np

y_true = np.array([3, -0.5, 2, 7, 4.2])
y_pred = np.array([2.5, 0.0, 2, 8, 4.0])

r2 = r2_score(y_true, y_pred)
print(f"R²: {r2:.4f}")
```

**Limitations:**
- R² **always increases** when adding more features, even if they're irrelevant (use Adjusted R² instead)
- A high R² doesn't guarantee a good model (could be overfitting)
- A low R² doesn't mean the model is useless (e.g., in noisy domains like finance, R²=0.1 can be meaningful)

---

---

## ML-040: What is VIF?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Variance Inflation Factor (VIF)** quantifies how much the variance of a regression coefficient is **inflated due to multicollinearity** with other features.

**Formula:**
```
VIF(j) = 1 / (1 - R²_j)
```

Where `R²_j` is the R² from regressing feature `xⱼ` on all other features.

**Interpretation:**
| VIF Value | Interpretation |
|-----------|---------------|
| 1 | No multicollinearity |
| 1 – 5 | Moderate, generally acceptable |
| 5 – 10 | High — investigate |
| > 10 | Severe multicollinearity — action needed |

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
import pandas as pd
import numpy as np

X = pd.DataFrame({
    'sqft': [1000, 1500, 1200, 1800, 2000],
    'rooms': [3, 4, 3, 5, 5],
    'age': [10, 5, 8, 2, 1]
})

vif_df = pd.DataFrame({
    'Feature': X.columns,
    'VIF': [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
})
print(vif_df)
```

**Action when VIF is high:**
- Drop the feature with the highest VIF and recalculate
- Combine correlated features (e.g., average them)
- Use regularization (Ridge penalizes large coefficients caused by multicollinearity)

---

---

## ML-041: What is a logistic decision boundary?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

The decision boundary is the set of points where $\hat{p} = 0.5$, which means:
$$w^T x + b = 0$$

This is a **linear hyperplane** in feature space. For 2D features, it's a line; for 3D, a plane. Non-linear boundaries can be created by adding polynomial features.

---

---

## ML-042: What is binary cross-entropy?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

Binary cross-entropy measures the **difference between the true label distribution and the predicted probability distribution**:

- If $y=1$: loss = $-\log(\hat{p})$ — penalizes low predicted probability for positive class
- If $y=0$: loss = $-\log(1 - \hat{p})$ — penalizes high predicted probability for negative class

As $\hat{p} \to 1$ when $y=1$: loss → 0. As $\hat{p} \to 0$ when $y=1$: loss → ∞.

---

---

## ML-043: What is gradient descent?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Gradient Descent** is an iterative optimization algorithm used to **minimize a loss function** by updating model parameters in the direction of the **negative gradient**.

**Intuition:** Imagine standing on a hilly landscape (the loss surface) and taking steps downhill — gradient descent finds the lowest point (minimum).

**Update rule:**
```
θ := θ - α · ∇_θ L(θ)
```

Where:
- `α` = learning rate (step size)
- `∇_θ L(θ)` = gradient of loss w.r.t. parameters

**For MSE loss in Linear Regression:**
```
θ := θ - (α/n) · Xᵀ(Xθ - y)
```

```python
import numpy as np

def gradient_descent(X, y, lr=0.01, epochs=1000):
    n, p = X.shape
    theta = np.zeros(p)

    for _ in range(epochs):
        y_pred = X @ theta
        gradient = (1/n) * X.T @ (y_pred - y)
        theta -= lr * gradient

    return theta

# Add bias column
X_b = np.column_stack([np.ones(len(X)), X])
theta_gd = gradient_descent(X_b, y, lr=0.01, epochs=1000)
```

**Hyperparameters:**
- **Learning rate (α):** Too small → slow convergence; too large → divergence
- **Epochs:** Number of full passes through the data

---

---

## ML-044: What is heteroscedasticity?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Heteroscedasticity** means the **variance of the residuals (errors) is not constant** across all levels of the independent variables — it changes systematically.

**Example:** Predicting income. For low earners, predictions may be fairly accurate (small errors). For high earners, errors may be much larger. The variance increases with income.

**Problems caused by heteroscedasticity:**
- OLS estimates remain **unbiased** but are **no longer efficient** (minimum variance)
- **Standard errors are incorrect** → hypothesis tests and confidence intervals are invalid
- Predictions may have inconsistent reliability

**Detection:**
- **Residual vs. Fitted plot:** Look for a funnel shape (variance expanding/contracting)
- **Breusch-Pagan test** or **White's test** (formal statistical tests)

```python
import statsmodels.api as sm
from statsmodels.stats.diagnostic import het_breuschpagan

model = sm.OLS(y, sm.add_constant(X)).fit()
_, p_value, _, _ = het_breuschpagan(model.resid, model.model.exog)
print(f"Breusch-Pagan p-value: {p_value:.4f}")
# p < 0.05 → evidence of heteroscedasticity
```

**Remedies:**
- Log-transform the target variable: `log(y)`
- Use Weighted Least Squares (WLS)
- Use robust standard errors (`cov_type='HC3'` in statsmodels)

---

---

## ML-045: What is homoscedasticity?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Homoscedasticity** means the **variance of the residuals (errors) is constant** across all levels of the independent variables.

This is one of the key assumptions of OLS regression. When it holds:
- Residuals are **equally spread** across all fitted values
- Statistical inference (confidence intervals, hypothesis tests) is **valid**
- OLS is the **Best Linear Unbiased Estimator (BLUE)**

**Visual check:** A residuals vs. fitted plot should show a **horizontal band** with **no pattern** — equal spread of residuals across all fitted values.

```python
import matplotlib.pyplot as plt
import statsmodels.api as sm

model = sm.OLS(y, sm.add_constant(X)).fit()

plt.scatter(model.fittedvalues, model.resid, alpha=0.5)
plt.axhline(0, color='red', linestyle='--')
plt.xlabel('Fitted Values')
plt.ylabel('Residuals')
plt.title('Residuals vs Fitted (Homoscedastic if random scatter)')
plt.show()
```

**Homoscedastic residuals:** Scatter plot shows points randomly scattered in a horizontal band.
**Heteroscedastic residuals:** Scatter plot shows a funnel or other systematic pattern.

---

---

## ML-046: What is maximum likelihood estimation?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

MLE finds parameters that **maximize the probability of observing the training data**.

For logistic regression, the likelihood is:
$$\mathcal{L}(\theta) = \prod_{i=1}^n \hat{p}_i^{y_i} (1 - \hat{p}_i)^{1 - y_i}$$

Taking the negative log gives binary cross-entropy. So **minimizing cross-entropy = maximizing likelihood**.

---

---

## ML-047: What is mini-batch gradient descent?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Mini-batch Gradient Descent** is a compromise between Batch GD and SGD. It computes the gradient on a **small random subset (mini-batch)** of the training data at each step.

**Update rule:**
```
θ := θ - α · (1/B) · Σᵢ∈B ∇_θ L(θ; xᵢ, yᵢ)
```

Where `B` is the mini-batch size (typically 32, 64, 128, 256).

**Comparison:**
| Method | Batch Size | Gradient Noise | Speed | Stability |
|--------|-----------|----------------|-------|-----------|
| Batch GD | n (all data) | None | Slow | High |
| SGD | 1 | High | Fast | Low |
| Mini-batch GD | B (e.g., 32) | Moderate | Fast | Moderate |

**Why mini-batch is preferred in practice:**
- Leverages vectorized operations (GPU-optimized)
- More stable than SGD, faster than full-batch
- **Standard choice for deep learning**

```python
import numpy as np

def mini_batch_gd(X, y, lr=0.01, epochs=100, batch_size=32):
    n, p = X.shape
    theta = np.zeros(p)

    for epoch in range(epochs):
        indices = np.random.permutation(n)
        for i in range(0, n, batch_size):
            batch_idx = indices[i:i+batch_size]
            X_batch, y_batch = X[batch_idx], y[batch_idx]
            grad = (1/len(batch_idx)) * X_batch.T @ (X_batch @ theta - y_batch)
            theta -= lr * grad
    return theta
```

---

---

## ML-048: What is multicollinearity?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Multicollinearity** occurs when two or more independent variables (features) in a regression model are **highly correlated** with each other.

**Why it's a problem:**
- Makes it difficult to estimate the **individual effect** of each feature on the target (coefficients become unstable and unreliable)
- **Inflates standard errors** of coefficients → makes hypothesis tests unreliable
- The model predictions remain accurate, but **interpretability suffers**
- Small changes in data can cause large changes in coefficient estimates

**Example:** If `x₁ = income` and `x₂ = annual_salary` are nearly identical, the model can't distinguish their individual effects.

**Types:**
- **Perfect multicollinearity:** `x₁ = a·x₂` (makes `XᵀX` non-invertible → OLS fails)
- **Near-perfect multicollinearity:** High correlation (> 0.8–0.9) between features

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.DataFrame({'x1': [1,2,3,4,5], 'x2': [2,4,6,8,10], 'x3': [1,3,2,5,4]})
corr_matrix = df.corr()

sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
# x1 and x2 have correlation = 1.0 → perfect multicollinearity
```

---

---

## ML-049: What is multinomial Logistic Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

Extends binary logistic regression to **K > 2 classes** (also called **Softmax Regression**).

$$P(y=k | x) = \frac{e^{w_k^T x}}{\sum_{j=1}^K e^{w_j^T x}}$$

The softmax function normalizes outputs so all class probabilities sum to 1. Used in neural network output layers for multi-class classification.

---

---

## ML-050: What is multiple Linear Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Multiple Linear Regression** uses **two or more independent variables** (features) to predict a continuous target variable.

**Equation:**
```
ŷ = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ
```

Or in matrix form:
```
ŷ = Xθ
```

Where `X` is the design matrix (with a column of 1s for the intercept).

```python
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.datasets import make_regression

# Multiple features
X, y = make_regression(n_samples=200, n_features=3, noise=10, random_state=42)

model = LinearRegression()
model.fit(X, y)

print("Intercept:", model.intercept_)
print("Coefficients:", model.coef_)
# Coefficient θⱼ = change in ŷ for 1-unit increase in xⱼ, holding others constant
```

**Interpreting coefficients:** Each coefficient `θⱼ` represents the **partial effect** of feature `xⱼ` on `y`, holding all other features constant (ceteris paribus).

**Challenges over simple LR:**
- Multicollinearity between features
- Harder to visualize
- Risk of including irrelevant features

---

---

## ML-051: What is one-vs-rest classification?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**OvR (One-vs-Rest)** trains K binary classifiers, one per class. Each classifier learns to separate class k from all others.

```python
from sklearn.linear_model import LogisticRegression
# multi_class='ovr' is one approach
model = LogisticRegression(multi_class='ovr')
```

For prediction, pick the class with the highest score. Simpler than multinomial but less theoretically elegant.

---

---

## ML-052: What is simple Linear Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Simple Linear Regression** involves exactly **one independent variable (feature)** predicting one dependent variable (target).

**Equation:**
```
ŷ = θ₀ + θ₁x
```

Where:
- `θ₀` = y-intercept (value of ŷ when x = 0)
- `θ₁` = slope (change in ŷ for a one-unit increase in x)

**Closed-form solution:**
```
θ₁ = Σ(xᵢ - x̄)(yᵢ - ȳ) / Σ(xᵢ - x̄)²
θ₀ = ȳ - θ₁x̄
```

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Single feature
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([3, 5, 4, 7, 9])

model = LinearRegression()
model.fit(X, y)

x_line = np.linspace(1, 5, 100).reshape(-1, 1)
plt.scatter(X, y, color='blue', label='Data')
plt.plot(x_line, model.predict(x_line), color='red', label='Regression line')
plt.xlabel('x'); plt.ylabel('y')
plt.legend()
plt.title(f'y = {model.intercept_:.2f} + {model.coef_[0]:.2f}x')
plt.show()
```

Simple linear regression is the foundation of all regression models and is easy to visualize and interpret.

---

---

## ML-053: What is stochastic gradient descent?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Stochastic Gradient Descent (SGD)** updates model parameters using the gradient computed from **one randomly selected training sample** at a time.

**Update rule:**
```
θ := θ - α · ∇_θ L(θ; xᵢ, yᵢ)   (for one random sample i)
```

**vs. Batch Gradient Descent:**
| Aspect | Batch GD | SGD |
|--------|----------|-----|
| Gradient computed on | All n samples | 1 sample |
| Update frequency | Once per epoch | n times per epoch |
| Convergence | Smooth, stable | Noisy, oscillating |
| Speed per epoch | Slow | Fast |
| Memory | High | Low |

**Advantages of SGD:**
- Much faster for large datasets
- Noisy updates help escape local minima
- Can do online learning (update with new data as it arrives)

**Disadvantages:**
- Noisy updates → doesn't converge to exact minimum, oscillates around it
- Requires learning rate scheduling (decay over time)

```python
from sklearn.linear_model import SGDRegressor

model = SGDRegressor(loss='squared_error', learning_rate='invscaling',
                     eta0=0.01, max_iter=1000, random_state=42)
model.fit(X_train, y_train)
```

---

---

## ML-054: What is the Mean Squared Error loss?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

**Mean Squared Error (MSE)** is the average of the squared differences between predicted and actual values.

**Formula:**
```
MSE = (1/n) · Σᵢ (yᵢ - ŷᵢ)²
```

**Properties:**
- Always non-negative; MSE = 0 means perfect predictions
- Units are squared units of the target (e.g., if y is in dollars, MSE is in dollars²)
- **Sensitive to outliers** (large errors are squared and dominate)
- Differentiable everywhere → suitable for gradient descent

```python
import numpy as np
from sklearn.metrics import mean_squared_error

y_true = np.array([3, -0.5, 2, 7])
y_pred = np.array([2.5, 0.0, 2, 8])

# Manual calculation
mse_manual = np.mean((y_true - y_pred) ** 2)
print(f"MSE (manual): {mse_manual:.4f}")

# Sklearn
mse_sklearn = mean_squared_error(y_true, y_pred)
print(f"MSE (sklearn): {mse_sklearn:.4f}")
```

**Gradient of MSE w.r.t. θ:**
```
∂MSE/∂θ = (-2/n) · Xᵀ(y - Xθ)
```

Setting to zero gives the Normal Equation for OLS.

---

---

## ML-055: What is the sigmoid function?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** HIGH

$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

Properties:
- Output range: (0, 1)
- $\sigma(0) = 0.5$
- Monotonically increasing
- Derivative: $\sigma'(z) = \sigma(z)(1 - \sigma(z))$

It maps any real number to a probability value.

---

---

## ML-056: How are Logistic Regression coefficients interpreted?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Coefficients represent the **change in log-odds** per unit increase in a feature:

$$\Delta \text{log-odds} = w_j \cdot \Delta x_j$$

More interpretable: **exponentiated coefficient** $e^{w_j}$ = **odds ratio**. If $e^{w_j} = 2$, then a 1-unit increase in $x_j$ doubles the odds of the positive class.

---

---

## ML-057: How do outliers affect Linear Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Outliers can have a significant and **disproportionate influence** on Linear Regression:

1. **Pull the regression line:** OLS minimizes squared errors, so large deviations get squared, giving outliers massive influence over the coefficient estimates.

2. **Distort coefficient estimates:** A single extreme outlier can change the slope dramatically.

3. **Inflate MSE and reduce R²:** Outliers increase prediction error metrics.

4. **Violate normality assumption:** Extreme outliers cause non-normal residuals.

**Types of influential points:**
- **Outlier:** Unusual y-value (high residual)
- **Leverage point:** Unusual x-value (extreme in feature space)
- **Influential point:** High leverage + high residual (changes model significantly if removed)

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression, HuberRegressor

X = np.array([[1],[2],[3],[4],[5],[20]])  # 20 is an outlier
y = np.array([2, 4, 5, 4, 5, 3])         # outlier has low y

# Standard OLS vs robust regression
ols = LinearRegression().fit(X, y)
huber = HuberRegressor().fit(X, y)

print(f"OLS slope: {ols.coef_[0]:.3f}")
print(f"Huber slope: {huber.coef_[0]:.3f}")
```

**Handling outliers:**
- Detect using: z-score, IQR, Cook's Distance
- Remove if data entry error; otherwise use robust regression (Huber, RANSAC)
- Transform features (log, sqrt) to reduce outlier impact

---

---

## ML-058: How do residual plots help?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

**Residual plots** are diagnostic tools that help assess whether the **linear regression assumptions are met** and identify potential issues.

**Common residual plots:**

**1. Residuals vs. Fitted Values**
- **Good:** Random scatter around y=0 (horizontal band)
- **Bad:** Funnel shape → heteroscedasticity; curve → non-linearity

**2. Normal Q-Q Plot**
- **Good:** Points follow the diagonal line
- **Bad:** S-curve or heavy tails → residuals not normally distributed

**3. Scale-Location Plot**
- Check for homoscedasticity; should be flat with random scatter

**4. Residuals vs. Leverage**
- Identifies influential outliers (Cook's Distance)

```python
import statsmodels.api as sm
import matplotlib.pyplot as plt

model = sm.OLS(y, sm.add_constant(X)).fit()

fig, axes = plt.subplots(1, 2, figsize=(12, 4))

# Residuals vs Fitted
axes[0].scatter(model.fittedvalues, model.resid, alpha=0.5)
axes[0].axhline(0, color='red', linestyle='--')
axes[0].set_xlabel('Fitted'); axes[0].set_ylabel('Residuals')
axes[0].set_title('Residuals vs Fitted')

# Q-Q plot
sm.qqplot(model.resid, line='s', ax=axes[1])
axes[1].set_title('Q-Q Plot')

plt.tight_layout()
plt.show()
```

---

---

## ML-059: How do you handle class imbalance?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

| Method | Description |
|--------|-------------|
| `class_weight='balanced'` | Automatically weights classes inversely proportional to frequency |
| Oversampling (SMOTE) | Synthesize minority class samples |
| Undersampling | Reduce majority class samples |
| Threshold tuning | Lower decision threshold for minority class |
| Different metrics | Use F1, AUC-ROC instead of accuracy |

```python
model = LogisticRegression(class_weight='balanced')
```

---

---

## ML-060: How do you handle non-linear relationships?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

When the relationship between features and target is non-linear, several strategies can be applied:

**1. Polynomial Features**
```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.linear_model import LinearRegression

# Adds x, x², x³, x₁x₂, etc.
model = make_pipeline(PolynomialFeatures(degree=2), LinearRegression())
model.fit(X_train, y_train)
```

**2. Feature Transformation**
- Log transform: `log(x)` for exponential relationships
- Square root: `√x` for diminishing returns
- Inverse: `1/x` for hyperbolic relationships

```python
import numpy as np
X_log = np.log1p(X)       # log(1+x) for non-negative x
X_sqrt = np.sqrt(X)
```

**3. Interaction Terms**
```python
X['x1_x2'] = X['x1'] * X['x2']
```

**4. Splines / Piecewise Linear Models**
- Fit different linear segments for different ranges of x

**5. Use Non-linear Algorithms**
- Decision Trees, Random Forests, Gradient Boosting (XGBoost, LightGBM)
- Support Vector Regression with RBF kernel
- Neural Networks

**6. Generalized Additive Models (GAMs)**
- Model each feature with a flexible smooth function

> **Best practice:** First explore scatter plots and correlation matrices to understand the shape of each feature-target relationship, then choose the appropriate transformation or model.

---

## ML-061: How does changing the classification threshold affect predictions?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Default threshold = 0.5. Changing it creates a **precision-recall tradeoff**:

| Threshold | Effect |
|-----------|--------|
| Lower (e.g., 0.3) | More positives predicted → Higher Recall, Lower Precision |
| Higher (e.g., 0.7) | Fewer positives predicted → Lower Recall, Higher Precision |

Use cases:
- **Medical diagnosis**: Lower threshold (catch all cases, reduce false negatives)
- **Spam filter**: Higher threshold (avoid flagging legit emails)

The **ROC curve** and **PR curve** help choose the optimal threshold.

---

---

## ML-062: How does regularization work in Logistic Regression?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Regularization adds a penalty to the loss to prevent overfitting:

- **L2 (Ridge)**: $\mathcal{L} + \frac{1}{2C} \|w\|^2$ — shrinks all coefficients
- **L1 (Lasso)**: $\mathcal{L} + \frac{1}{C} \|w\|_1$ — can zero out coefficients (feature selection)

In scikit-learn, `C = 1/λ` (inverse regularization strength):
- Small C → strong regularization
- Large C → weak regularization

```python
model = LogisticRegression(C=0.1, penalty='l2')  # Strong L2 regularization
```

---

## ML-063: What assumptions does Linear Regression make?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Linear Regression relies on several key assumptions. Violations can lead to biased or inefficient estimates.

1. **Linearity:** The relationship between features and target is linear.
   - Check: Scatter plots, residual vs. fitted plots

2. **Independence:** Observations are independent of each other.
   - Violated in: Time series data (autocorrelation)

3. **Homoscedasticity:** The variance of residuals is constant across all levels of the predictor (constant error variance).
   - Check: Residuals vs. fitted plot — should show no pattern

4. **Normality of residuals:** Residuals are approximately normally distributed (important for inference, less so for prediction).
   - Check: Q-Q plot, Shapiro-Wilk test

5. **No multicollinearity:** Features are not highly correlated with each other.
   - Check: Correlation matrix, Variance Inflation Factor (VIF)

6. **No endogeneity:** Features are not correlated with the error term.

```python
import statsmodels.api as sm
import matplotlib.pyplot as plt

model = sm.OLS(y, sm.add_constant(X)).fit()
residuals = model.resid
fitted = model.fittedvalues

# Residuals vs Fitted plot
plt.scatter(fitted, residuals)
plt.axhline(0, color='r', linestyle='--')
plt.xlabel('Fitted Values'); plt.ylabel('Residuals')
plt.title('Residuals vs Fitted')
plt.show()

# Q-Q plot for normality
sm.qqplot(residuals, line='s')
plt.show()
```

---

---

## ML-064: What loss function is used?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Logistic Regression uses **Binary Cross-Entropy (Log Loss)**:

$$\mathcal{L} = -\frac{1}{n} \sum_{i=1}^n \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]$$

This penalizes confident wrong predictions much more heavily than uncertain ones.

---

---

## ML-065: Why are squared errors used?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Squared errors are preferred over other error forms for several reasons:

1. **Mathematical convenience:** Squaring makes the loss function **differentiable everywhere** (unlike absolute value which has no derivative at 0), enabling gradient-based optimization.

2. **Closed-form solution:** MSE leads to the Normal Equation `θ = (XᵀX)⁻¹Xᵀy` — an exact analytical solution.

3. **Penalizes large errors more:** Squaring amplifies large mistakes, which is often desirable (a prediction off by 10 is much worse than one off by 1, and squared errors reflect this: 100 vs 1).

4. **Connection to MLE:** Minimizing squared error is equivalent to **Maximum Likelihood Estimation** when residuals follow a Normal (Gaussian) distribution:
   ```
   If ε ~ N(0, σ²), then MLE of θ = OLS solution
   ```

5. **Convex loss surface:** MSE produces a convex optimization landscape with a single global minimum — gradient descent is guaranteed to converge.

**Trade-off:** Squared errors are **sensitive to outliers** (since large errors get squared). In that case, MAE or Huber loss may be preferred.

---

---

## ML-066: Why is Logistic Regression used for classification?

**Domain:** Topic 20: Linear and Logistic Regression &nbsp;|&nbsp; **Priority:** MEDIUM

Linear regression can predict values outside [0, 1], making it unsuitable for probabilities. Logistic Regression:
- Outputs values in (0, 1) via the sigmoid function
- Models the **log-odds** of the class as a linear function
- Has a well-defined probabilistic interpretation
- Uses a convex loss function (binary cross-entropy) with a global minimum

---

---

## ML-067: How do you interpret features selected by Lasso?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

Lasso sets irrelevant feature coefficients to exactly zero, performing **automatic feature selection**:

```python
import pandas as pd

coefs = pd.Series(lasso_model.coef_, index=feature_names)
selected = coefs[coefs != 0].sort_values(key=abs, ascending=False)
print("Selected features and their coefficients:")
print(selected)
```

**Interpretation:**
- **Non-zero coefficient** = feature is selected and contributes to prediction
- **Magnitude** = relative importance (after scaling)
- **Sign** = direction of effect (positive = increases prediction, negative = decreases)

---

---

## ML-068: How does regularization affect bias and variance?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

Regularization directly controls the **bias-variance tradeoff**:

**As regularization strength (λ) increases:**
- **Bias increases:** The model is forced away from the true function (more constrained)
- **Variance decreases:** Coefficients are more stable, less sensitive to training data variations

**As regularization strength (λ) decreases:**
- **Bias decreases:** Model can fit the data more freely
- **Variance increases:** Model becomes sensitive to training data noise

```
λ = 0         → OLS: Low Bias, High Variance (overfitting risk)
λ = optimal   → Balanced: Minimum Total Error on test data
λ → ∞        → Null model: High Bias, Low Variance (underfitting)
```

**Bias-Variance decomposition:**
```
Expected Test Error = Bias² + Variance + Irreducible Noise
```

```python
import numpy as np
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

alphas = [0, 0.1, 1, 10, 100, 1000]
for alpha in alphas:
    train_errors, test_errors = [], []
    for seed in range(30):
        X_tr, X_te, y_tr, y_te = train_test_split(X, y, test_size=0.3,
                                                    random_state=seed)
        model = Ridge(alpha=alpha).fit(X_tr, y_tr)
        train_errors.append(mean_squared_error(y_tr, model.predict(X_tr)))
        test_errors.append(mean_squared_error(y_te, model.predict(X_te)))

    print(f"α={alpha:5}: Train MSE={np.mean(train_errors):.3f}, "
          f"Test MSE={np.mean(test_errors):.3f}, "
          f"Variance={np.var(test_errors):.3f}")
```

---

---

## ML-069: Should features be scaled before Ridge and Lasso?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

**Yes — scaling is essential** before applying Ridge or Lasso regularization.

**Why scaling is required:**

Ridge and Lasso penalize the **magnitude of coefficients**. Without scaling, features with larger numerical ranges will have smaller coefficients (to fit the data), while features with smaller ranges will have larger coefficients. The regularization penalty is then **unfairly applied** based on feature scale, not actual importance.

**Example:**
- Feature 1: `age` (range 0–100) → coefficient ≈ 0.05 (small)
- Feature 2: `income_cents` (range 0–10,000,000) → coefficient ≈ 0.000001 (tiny)

Without scaling, L2 penalty barely touches the income coefficient even if income is unimportant.

**With standardization (mean=0, std=1):**
- All features are on equal footing
- Regularization penalizes equally across features based on relevance

```python
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge, Lasso
from sklearn.pipeline import make_pipeline

# CORRECT: scaling inside pipeline
model = make_pipeline(
    StandardScaler(),   # Scale BEFORE regularization
    Ridge(alpha=1.0)
)
model.fit(X_train, y_train)

# WRONG: scaling outside, or not scaling at all
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)   # Data leakage risk if not in pipeline
X_test_scaled = scaler.transform(X_test)
```

> **Important:** Always use a **Pipeline** to apply scaling — this prevents data leakage by ensuring the scaler is fit only on training data.

---

---

## ML-070: What is Elastic Net?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

**Elastic Net** combines **both L1 and L2 regularization** into a single penalty, getting the benefits of both Ridge and Lasso.

**Objective:**
```
Minimize: Σ(yᵢ - ŷᵢ)² + λ₁·Σ|θⱼ| + λ₂·Σθⱼ²
```

In scikit-learn's parameterization:
```
Minimize: (1/2n)·||y - Xθ||² + α·l1_ratio·||θ||₁ + (α/2)·(1-l1_ratio)·||θ||₂²
```

Where:
- `alpha` controls overall regularization strength
- `l1_ratio` (between 0 and 1) controls the mix:
  - `l1_ratio = 1` → pure Lasso
  - `l1_ratio = 0` → pure Ridge
  - `l1_ratio = 0.5` → 50/50 mix

```python
from sklearn.linear_model import ElasticNet, ElasticNetCV
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

# Manual Elastic Net
en = make_pipeline(
    StandardScaler(),
    ElasticNet(alpha=0.1, l1_ratio=0.5)  # equal L1 and L2
)
en.fit(X_train, y_train)

# With CV to find best alpha and l1_ratio
encv = make_pipeline(
    StandardScaler(),
    ElasticNetCV(l1_ratio=[0.1, 0.5, 0.7, 0.9, 1.0],
                 alphas=[0.001, 0.01, 0.1, 1.0],
                 cv=5)
)
encv.fit(X_train, y_train)
print(f"Best alpha: {encv.named_steps['elasticnetcv'].alpha_}")
print(f"Best l1_ratio: {encv.named_steps['elasticnetcv'].l1_ratio_}")
```

---

---

## ML-071: What is Lasso Regression?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

**Lasso Regression** (Least Absolute Shrinkage and Selection Operator, **L1 Regularization**) adds the **sum of absolute values of coefficients** as a penalty.

**Objective:**
```
Minimize: Σ(yᵢ - ŷᵢ)² + λ · Σⱼ |θⱼ|
```

**Key properties:**
- **Shrinks** some coefficients **exactly to zero** → performs automatic **feature selection**
- Results in a **sparse model** (only a subset of features have non-zero coefficients)
- Especially useful when you believe many features are irrelevant
- Does **not** have a closed-form solution (because `|θ|` is not differentiable at 0); solved with coordinate descent or subgradient methods

```python
from sklearn.linear_model import Lasso
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

model = make_pipeline(StandardScaler(), Lasso(alpha=0.1))
model.fit(X_train, y_train)

# Feature selection: non-zero coefficients
feature_mask = model.named_steps['lasso'].coef_ != 0
selected_features = X_train.columns[feature_mask]
print("Selected features:", selected_features.tolist())
```

---

---

## ML-072: What is LassoCV?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

`LassoCV` uses **coordinate descent** with k-fold CV to find the best alpha for Lasso:

```python
from sklearn.linear_model import LassoCV
import numpy as np

lasso_cv = LassoCV(alphas=np.logspace(-4, 1, 50), cv=5, max_iter=10000)
lasso_cv.fit(X_train_scaled, y_train)

print("Best alpha:", lasso_cv.alpha_)
print("Non-zero coefs:", np.sum(lasso_cv.coef_ != 0))
```

It follows the **regularization path** efficiently — evaluates many alphas faster than naive CV.

---

---

## ML-073: What is Ridge Regression?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

**Ridge Regression** (also called **L2 Regularization** or **Tikhonov Regularization**) adds the **sum of squared coefficients** as a penalty to the OLS loss.

**Objective:**
```
Minimize: Σ(yᵢ - ŷᵢ)² + λ · Σⱼ θⱼ²
```

Or in matrix form:
```
Minimize: ||y - Xθ||² + λ||θ||²
```

**Closed-form solution:**
```
θ_ridge = (XᵀX + λI)⁻¹ Xᵀy
```

Adding `λI` ensures the matrix is always invertible — Ridge directly solves the multicollinearity problem.

**Key properties:**
- **Shrinks** all coefficients toward zero, but **never exactly to zero**
- Handles multicollinearity well (distributes weight among correlated features)
- Keeps all features in the model
- The penalty grows quadratically — large coefficients are penalized much more than small ones

```python
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

model = make_pipeline(StandardScaler(), Ridge(alpha=1.0))
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

---

---

## ML-074: What is RidgeCV?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

`RidgeCV` is an efficient cross-validated Ridge Regression. It uses **generalized cross-validation (GCV)** to select the best alpha without repeating full training multiple times:

```python
from sklearn.linear_model import RidgeCV
import numpy as np

# Try multiple alphas automatically
ridge_cv = RidgeCV(alphas=np.logspace(-3, 3, 50), scoring='neg_mean_squared_error', cv=5)
ridge_cv.fit(X_train_scaled, y_train)

print("Best alpha:", ridge_cv.alpha_)
print("CV Score:", ridge_cv.best_score_)
```

More efficient than `GridSearchCV` for Ridge specifically. Note: scaling should still be done separately or in a pipeline.

---

---

## ML-075: What is the difference between L1 and L2 regularization?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

| Aspect | L1 (Lasso) | L2 (Ridge) |
|--------|-----------|-----------|
| Penalty term | `λ·Σ\|θⱼ\|` | `λ·Σθⱼ²` |
| Effect on coefficients | Drives some to **exactly zero** | Shrinks all toward zero, but **never exactly zero** |
| Feature selection | **Yes** (automatic) | No |
| Sparsity | Produces **sparse** models | Dense models |
| Handles multicollinearity | Picks one of correlated features, zeros others | Distributes weight evenly among correlated features |
| Solution | No closed form (subdifferential) | Closed form: `(XᵀX + λI)⁻¹Xᵀy` |
| Geometric intuition | Diamond-shaped constraint → corners at axes | Circular constraint → no corners |
| Best used when | Many irrelevant features exist | All features are relevant; multicollinearity present |

**Geometric intuition:**
- L1: The L1 ball is a **diamond** in 2D. The optimal solution often hits a corner (where one coordinate = 0) → sparsity.
- L2: The L2 ball is a **circle** in 2D. The optimal solution rarely hits an axis → no sparsity.

```python
import numpy as np

# L1 norm (sum of absolutes)
theta = np.array([2.0, -3.0, 0.5])
l1_penalty = np.sum(np.abs(theta))      # = 5.5

# L2 norm squared (sum of squares)
l2_penalty = np.sum(theta ** 2)         # = 13.25
```

---

---

## ML-076: What is the regularization parameter?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** HIGH

The **regularization parameter** (commonly denoted `λ` in mathematics or `alpha` in scikit-learn) controls the **strength of the regularization penalty**.

**Role in Ridge:**
```
Objective = MSE + λ · Σθⱼ²
```

**Role in Lasso:**
```
Objective = MSE + λ · Σ|θⱼ|
```

**Effect of λ:**
- **Small λ (→ 0):** Minimal regularization → behaves like OLS (low bias, high variance)
- **Large λ (→ ∞):** Strong regularization → all coefficients → 0 (high bias, low variance)

**Tuning:** The optimal λ is found via **cross-validation** (e.g., `RidgeCV`, `LassoCV` in sklearn).

```python
import numpy as np
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler

X_scaled = StandardScaler().fit_transform(X)

alphas = [0.001, 0.01, 0.1, 1.0, 10.0, 100.0]
for alpha in alphas:
    ridge = Ridge(alpha=alpha).fit(X_scaled, y)
    coef_norm = np.linalg.norm(ridge.coef_)
    print(f"α={alpha:6.3f} | Coefficient L2 norm: {coef_norm:.4f}")
```

> **Note:** scikit-learn uses `alpha` as the regularization parameter; statsmodels uses `alpha`; the mathematical notation typically uses `λ`.

---

---

## ML-077: How do you compare Linear, Ridge, and Lasso?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

```python
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import cross_val_score
import numpy as np

models = {
    'Linear': LinearRegression(),
    'Ridge': Ridge(alpha=1.0),
    'Lasso': Lasso(alpha=0.1, max_iter=10000)
}

results = {}
for name, model in models.items():
    pipe = Pipeline([('scaler', StandardScaler()), ('model', model)])
    scores = cross_val_score(pipe, X, y, cv=5, scoring='neg_root_mean_squared_error')
    results[name] = -scores.mean()
    print(f"{name}: RMSE = {-scores.mean():.4f} ± {scores.std():.4f}")
```

| Model | Use When | Behavior |
|-------|----------|----------|
| Linear | Few features, no multicollinearity | No regularization |
| Ridge | Multicollinearity present | Shrinks all coefs |
| Lasso | Feature selection needed | Zeros out some coefs |
| Elastic Net | Both situations | Combination of Ridge + Lasso |

---

## ML-078: How do you implement Lasso Regression?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

```python
from sklearn.linear_model import Lasso
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('lasso', Lasso(alpha=0.1, max_iter=10000))
])

pipe.fit(X_train, y_train)
y_pred = pipe.predict(X_test)

# Check which features were selected (non-zero coefficients)
coefs = pipe.named_steps['lasso'].coef_
selected = [(f, c) for f, c in zip(feature_names, coefs) if c != 0]
print("Selected features:", selected)
```

---

---

## ML-079: How do you implement Ridge Regression?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

```python
from sklearn.linear_model import Ridge
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score
import numpy as np

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('ridge', Ridge(alpha=1.0))  # alpha = regularization strength
])

pipe.fit(X_train, y_train)
y_pred = pipe.predict(X_test)
print("R²:", r2_score(y_test, y_pred))
print("Coefficients:", pipe.named_steps['ridge'].coef_)
```

---

---

## ML-080: How do you select the best regularization strength?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

The optimal regularization strength (lambda/alpha) is selected using **cross-validation** to find the value that minimizes validation error.

**Method 1: Manual Cross-Validation with GridSearch**
```python
from sklearn.model_selection import GridSearchCV
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(StandardScaler(), Ridge())
param_grid = {'ridge__alpha': [0.001, 0.01, 0.1, 1, 10, 100, 1000]}

grid_search = GridSearchCV(pipeline, param_grid, cv=5,
                           scoring='neg_mean_squared_error')
grid_search.fit(X_train, y_train)
print(f"Best alpha: {grid_search.best_params_}")
print(f"Best CV MSE: {-grid_search.best_score_:.4f}")
```

**Method 2: RidgeCV / LassoCV (Efficient built-in CV)**
```python
from sklearn.linear_model import RidgeCV, LassoCV
import numpy as np

alphas = np.logspace(-4, 4, 100)  # 100 values from 0.0001 to 10000

# RidgeCV uses efficient leave-one-out CV
ridge_cv = RidgeCV(alphas=alphas, cv=5)
ridge_cv.fit(X_train_scaled, y_train)
print(f"Best Ridge alpha: {ridge_cv.alpha_:.4f}")

# LassoCV uses coordinate descent for all alphas
lasso_cv = LassoCV(alphas=alphas, cv=5, max_iter=10000)
lasso_cv.fit(X_train_scaled, y_train)
print(f"Best Lasso alpha: {lasso_cv.alpha_:.4f}")
```

**Method 3: Regularization path (coefficient trace plot)**
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import lasso_path

alphas, coefs, _ = lasso_path(X_train_scaled, y_train)

plt.figure(figsize=(10, 4))
for coef in coefs:
    plt.plot(np.log10(alphas), coef)
plt.xlabel('log10(alpha)'); plt.ylabel('Coefficient value')
plt.title('Lasso Regularization Path')
plt.axvline(x=np.log10(lasso_cv.alpha_), color='r', linestyle='--',
            label='Optimal alpha')
plt.legend(); plt.show()
```

> **Best practice:** Use logarithmically spaced alpha values (`np.logspace`) and choose based on cross-validated MSE, not training MSE.

---

## ML-081: How do you tune alpha?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

```python
from sklearn.model_selection import GridSearchCV
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge
import numpy as np

pipe = Pipeline([('scaler', StandardScaler()), ('ridge', Ridge())])

param_grid = {'ridge__alpha': np.logspace(-3, 3, 50)}

grid_search = GridSearchCV(pipe, param_grid, cv=5, scoring='neg_root_mean_squared_error')
grid_search.fit(X_train, y_train)

print("Best alpha:", grid_search.best_params_['ridge__alpha'])
print("Best CV RMSE:", -grid_search.best_score_)
```

Use a **log-scale** for alpha search since it spans orders of magnitude.

---

---

## ML-082: How does Lasso perform feature selection?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

Lasso drives **some coefficients to exactly zero** through the geometry of its L1 penalty, effectively removing those features from the model.

**Mathematical mechanism:**
The L1 penalty's subdifferential at `θ = 0` is the interval `[-λ, λ]`. If the OLS estimate's gradient at `θ = 0` lies within this interval (i.e., the feature doesn't contribute enough), the coordinate descent update sets that coefficient to exactly zero.

**Coordinate descent update for Lasso:**
```
θⱼ = sign(ρⱼ) · max(|ρⱼ| - λ, 0)
```
This is the **soft-thresholding operator** — if `|ρⱼ| < λ`, the coefficient is set to zero.

```python
import numpy as np
from sklearn.linear_model import Lasso
from sklearn.preprocessing import StandardScaler

# Synthetic data with many irrelevant features
np.random.seed(42)
X = np.random.randn(100, 10)
y = 2*X[:,0] + 3*X[:,1] - X[:,2] + np.random.randn(100)*0.5
# Only features 0, 1, 2 matter; rest are noise

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

lasso = Lasso(alpha=0.1)
lasso.fit(X_scaled, y)

print("Lasso Coefficients:")
for i, coef in enumerate(lasso.coef_):
    print(f"  Feature {i}: {coef:.3f} {'✓ selected' if coef != 0 else '✗ zero'}")
```

**Output:** Features 0, 1, 2 will have non-zero coefficients; irrelevant features will be zero.

> This built-in feature selection makes Lasso especially useful when you have high-dimensional data with many irrelevant features.

---

---

## ML-083: How does Ridge affect coefficients?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

Ridge regression **shrinks all coefficients toward zero** proportionally, but **never sets any coefficient exactly to zero**.

**Mathematical insight:**
The Ridge update effectively multiplies each OLS coefficient by a shrinkage factor:
```
θ_ridge_j ≈ θ_OLS_j · (1 / (1 + λ/n))
```
As `λ` increases, coefficients shrink more.

**Effect on correlated features:**
- If `x₁` and `x₂` are perfectly correlated, Ridge distributes the weight **equally** between them rather than arbitrarily assigning it to one.

```python
import numpy as np
from sklearn.linear_model import Ridge, LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_regression

X, y, true_coef = make_regression(n_samples=100, n_features=5,
                                   n_informative=3, noise=10,
                                   coef=True, random_state=42)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

ols = LinearRegression().fit(X_scaled, y)
ridge = Ridge(alpha=10.0).fit(X_scaled, y)

print("OLS Coefficients:", np.round(ols.coef_, 2))
print("Ridge Coefficients (α=10):", np.round(ridge.coef_, 2))
# Ridge coefficients are smaller in magnitude
```

**Key takeaway:** Ridge never fully eliminates a feature — it reduces the influence of less important features but keeps them in the model.

---

---

## ML-084: What happens when alpha is too high?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

When alpha (regularization strength) is too high:
- Penalty dominates the loss function
- All coefficients are shrunk heavily toward zero
- Model becomes **overly simple** → **underfitting**
- High bias, low variance
- Training and test performance both suffer

```python
# Extreme alpha → near-zero coefficients
ridge = Ridge(alpha=1e6)
ridge.fit(X_train_scaled, y_train)
print(ridge.coef_)  # All near zero
```

---

---

## ML-085: What happens when regularization is very high?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

When `λ → ∞`, the regularization penalty dominates the objective function, forcing **all coefficients toward zero**.

**For Ridge (L2):**
- All `θⱼ → 0` (but never exactly zero for finite λ)
- Model predicts approximately the **mean of y** for all inputs
- Extremely high bias, very low variance
- Equivalent to the **null model** (intercept-only)

**For Lasso (L1):**
- All `θⱼ = 0` exactly (for large enough finite λ)
- Same null model behavior

```python
import numpy as np
from sklearn.linear_model import Ridge, Lasso
from sklearn.preprocessing import StandardScaler

X_scaled = StandardScaler().fit_transform(X)

for alpha in [1, 100, 10000, 1e9]:
    ridge = Ridge(alpha=alpha).fit(X_scaled, y)
    print(f"α={alpha:.0e} | Max |coef|: {np.max(np.abs(ridge.coef_)):.6f}")

# Output shows coefficients → 0 as alpha → ∞
```

**Bias-Variance impact:**
- Very high λ → **underfitting** (model is too constrained)
- The model ignores the training data and just predicts the mean

> **The optimal λ lies between 0 and ∞**, balancing fit quality and model simplicity. This is found via cross-validation.

---

---

## ML-086: What happens when regularization is zero?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

When `λ = 0`, the regularization term vanishes and the model reduces to **ordinary OLS (Ordinary Least Squares)**:

```
Objective = Σ(yᵢ - ŷᵢ)²  [no penalty]
```

**Consequences:**
- Coefficients are the standard OLS estimates: `θ = (XᵀX)⁻¹Xᵀy`
- **No shrinkage** is applied
- If features are multicollinear, `(XᵀX)` may be singular or near-singular → unstable coefficients
- Higher risk of **overfitting** on small datasets with many features
- Maximum flexibility — model fits training data as closely as possible

```python
from sklearn.linear_model import Ridge

# λ=0 → equivalent to OLS
ridge_zero = Ridge(alpha=0)
ridge_zero.fit(X_scaled, y)

from sklearn.linear_model import LinearRegression
ols = LinearRegression().fit(X_scaled, y)

import numpy as np
print("Ridge (α=0):", np.round(ridge_zero.coef_, 4))
print("OLS:         ", np.round(ols.coef_, 4))
# Should be identical (or very close)
```

> **In practice:** Never set `alpha=0` for Ridge or Lasso in production; if you want OLS, use `LinearRegression()` directly.

---

---

## ML-087: When would you prefer Ridge over Lasso?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

**Prefer Ridge when:**

1. **Most or all features are relevant** — Lasso would zero out some useful features; Ridge keeps all of them with reduced coefficients.

2. **Many correlated features** — Ridge handles multicollinearity by distributing weight evenly; Lasso arbitrarily picks one from a correlated group.

3. **Stable coefficient estimates needed** — Ridge gives smoother, more stable coefficient paths than Lasso.

4. **Prediction accuracy is the primary goal** — In many settings with dense, meaningful features, Ridge achieves lower test error.

5. **p (features) << n (samples)** — With relatively few features, you likely want all of them and just need shrinkage.

**Prefer Lasso when:**
- Many features are suspected to be irrelevant (high-dimensional sparse problems)
- Interpretability requires a small subset of features
- You need automated feature selection

```python
from sklearn.linear_model import RidgeCV, LassoCV
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

# Try both and compare cross-validation scores
ridge_cv = make_pipeline(StandardScaler(), RidgeCV(alphas=[0.1, 1, 10, 100]))
lasso_cv = make_pipeline(StandardScaler(), LassoCV(alphas=[0.001, 0.01, 0.1, 1]))

ridge_cv.fit(X_train, y_train)
lasso_cv.fit(X_train, y_train)

print(f"Ridge CV score: {ridge_cv.score(X_test, y_test):.4f}")
print(f"Lasso CV score: {lasso_cv.score(X_test, y_test):.4f}")
```

---

---

## ML-088: Why is Elastic Net useful for correlated features?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

Elastic Net solves a key weakness of Lasso with correlated features:

**Lasso's problem with correlated features:**
- When features are highly correlated, Lasso arbitrarily picks **one** and sets the others to zero
- The selected feature depends on small data variations → unstable
- This is problematic when correlated features all contribute to the target

**Elastic Net's solution:**
- The L2 (Ridge) component creates a **grouping effect**: correlated features are **selected or rejected together**, with similar coefficients
- The L1 component still provides **sparsity** (sets irrelevant features to zero)

**Concrete example:**
- 5 highly correlated gene expression features all related to a disease outcome
- Lasso: picks 1, ignores 4 (even if all 5 matter)
- Elastic Net: keeps all 5 with moderate coefficients → better interpretation and prediction

```python
import numpy as np
from sklearn.linear_model import Lasso, ElasticNet
from sklearn.preprocessing import StandardScaler

np.random.seed(42)
# Create correlated features
x1 = np.random.randn(100)
X = np.column_stack([x1, x1 + 0.01*np.random.randn(100),
                     x1 + 0.01*np.random.randn(100),
                     np.random.randn(100)])  # Last feature is independent
y = 2*x1 + np.random.randn(100)*0.5

X_s = StandardScaler().fit_transform(X)

print("Lasso:", np.round(Lasso(0.05).fit(X_s, y).coef_, 3))
print("ElasticNet:", np.round(ElasticNet(0.05, l1_ratio=0.5).fit(X_s, y).coef_, 3))
# Lasso: one of first three features; ElasticNet: all three share weight
```

---

---

## ML-089: Why is regularization needed?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

**Regularization** is needed to prevent **overfitting** — the situation where a model learns the training data too well (including noise) and fails to generalize to new data.

**Root causes of overfitting that regularization addresses:**
- **Too many features:** A model with many features has many parameters and can memorize training data
- **Complex models:** High-degree polynomials, deep trees, etc.
- **Limited training data:** With few samples and many features, the model can find spurious patterns

**What regularization does:**
- Adds a **penalty term** to the loss function that discourages large coefficients
- Constrains the model's flexibility, forcing it to learn simpler, more generalizable patterns
- Trades a small increase in bias for a larger decrease in variance → better test performance

**Without regularization (plain OLS):**
- On perfectly collinear features, `(XᵀX)` is singular → no unique solution
- Coefficients can be arbitrarily large, leading to unstable and overfit models

**Regularized objective:**
```
Minimize: Loss(θ) + λ · Penalty(θ)
```

The `λ` parameter controls the trade-off between fitting the data and keeping coefficients small. As `λ → 0`, we approach OLS; as `λ → ∞`, all coefficients are pushed to zero.

---

---

## ML-090: Why should scaling be inside a pipeline?

**Domain:** Topic 21: Regularization: Ridge, Lasso and Elastic Net &nbsp;|&nbsp; **Priority:** MEDIUM

**Outside pipeline (WRONG — causes leakage):**
```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)  # Leaks test statistics!
scores = cross_val_score(Ridge(), X_scaled, y, cv=5)
```

**Inside pipeline (CORRECT):**
```python
pipe = Pipeline([('scaler', StandardScaler()), ('ridge', Ridge())])
scores = cross_val_score(pipe, X, y, cv=5)  # Scaler fit on train fold only
```

When the scaler is inside the pipeline, it's re-fit on each training fold during cross-validation, preventing the test fold's statistics from influencing preprocessing.

---

---

## ML-091: What are prior, likelihood, and posterior probabilities?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

| Term | Formula | Meaning |
|------|---------|---------|
| **Prior** `P(y)` | Frequency of class in training data | Belief about class before seeing features |
| **Likelihood** `P(X\|y)` | How probable the features are given the class | Evidence from the data |
| **Posterior** `P(y\|X)` | Bayes' theorem result | Updated belief after seeing features |

**Example — Spam Detection:**
- Prior: `P(spam) = 0.3` (30% of emails are spam)
- Likelihood: `P("free" | spam) = 0.8`
- Posterior: probability this specific email is spam given its words

---

---

## ML-092: What is Bayes theorem?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

Bayes' theorem relates the **posterior** probability to the **prior** and **likelihood**:

$$P(y \mid X) = \frac{P(X \mid y) \cdot P(y)}{P(X)}$$

Where:
- `P(y | X)` = **Posterior** — probability of class `y` given features `X`
- `P(X | y)` = **Likelihood** — probability of features `X` given class `y`
- `P(y)` = **Prior** — probability of class `y` before seeing data
- `P(X)` = **Evidence** — normalizing constant (same for all classes, often ignored)

In classification, we choose the class that maximizes the posterior:

$$\hat{y} = \arg\max_y P(y \mid X) = \arg\max_y P(y) \prod_{i=1}^{n} P(x_i \mid y)$$

---

---

## ML-093: What is Bernoulli Naive Bayes?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

**Bernoulli Naive Bayes** models binary/boolean features — each feature indicates whether a term **occurs or not** (presence/absence).

- Unlike Multinomial NB, it penalizes the **non-occurrence** of features
- Suitable for **binary feature vectors** (e.g., binary Bag-of-Words)

$$P(x_i \mid y) = P(i \mid y) \cdot x_i + (1 - P(i \mid y)) \cdot (1 - x_i)$$

```python
from sklearn.naive_bayes import BernoulliNB

bnb = BernoulliNB()
bnb.fit(X_binary, y)
```

**Comparison:**
| Model | Feature Type | Example |
|-------|-------------|---------|
| Gaussian | Continuous | Height, weight |
| Multinomial | Count/frequency | Word counts |
| Bernoulli | Binary | Word present/absent |

---

---

## ML-094: What is Euclidean distance?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-095: What is Gaussian Naive Bayes?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

**Gaussian Naive Bayes** assumes that continuous features follow a **normal (Gaussian) distribution** within each class.

$$P(x_i \mid y) = \frac{1}{\sqrt{2\pi\sigma_y^2}} \exp\left(-\frac{(x_i - \mu_y)^2}{2\sigma_y^2}\right)$$

- Parameters `μ_y` (mean) and `σ_y²` (variance) are estimated per feature per class from training data
- Best suited for **continuous, real-valued features**

```python
from sklearn.naive_bayes import GaussianNB

gnb = GaussianNB()
gnb.fit(X_train, y_train)
print(gnb.theta_)   # class means
print(gnb.var_)     # class variances
```

---

---

## ML-096: What is KNN?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-097: What is Laplace smoothing?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

**Laplace smoothing** (add-1 smoothing) prevents zero probabilities by adding a small count `α` (typically 1) to every feature count:

$$P(x_i \mid y) = \frac{\text{count}(x_i, y) + \alpha}{\text{count}(y) + \alpha \cdot |V|}$$

Where `|V|` is the vocabulary/feature size.

- `α = 1`: Laplace smoothing
- `α < 1`: Lidstone smoothing
- Ensures no probability is ever exactly zero
- Acts as a **regularizer** (introduces a uniform prior over features)

```python
from sklearn.naive_bayes import MultinomialNB

# alpha=1 is default Laplace smoothing
mnb = MultinomialNB(alpha=1.0)
mnb.fit(X_train, y_train)
```

---

---

## ML-098: What is Manhattan distance?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-099: What is Multinomial Naive Bayes?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

**Multinomial Naive Bayes** models feature counts (or frequencies) and assumes features follow a **multinomial distribution**.

- Designed for **discrete count data** (e.g., word counts in a document)
- The likelihood `P(xᵢ | y)` represents the probability of feature `i` occurring given class `y`
- Commonly used in **text classification** with Bag-of-Words or TF-IDF features

$$P(x \mid y) = \frac{(\sum_i x_i)!}{\prod_i x_i!} \prod_i P(x_i \mid y)^{x_i}$$

```python
from sklearn.naive_bayes import MultinomialNB
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(corpus)

mnb = MultinomialNB()
mnb.fit(X, y)
```

---

---

## ML-100: What is Naive Bayes?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

**Naive Bayes** is a family of probabilistic classifiers based on applying **Bayes' theorem** with a strong (naive) assumption of **conditional independence** among features given the class label.

- It models `P(class | features)` using Bayes' theorem
- Despite the "naive" assumption, it works surprisingly well in practice (text classification, spam detection, sentiment analysis)
- It is fast, simple, and scales well to high-dimensional data

```python
from sklearn.naive_bayes import GaussianNB

model = GaussianNB()
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

---

---

## ML-101: What is the curse of dimensionality?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-102: What is the zero-frequency problem?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** HIGH

The **zero-frequency problem** occurs when a feature value never appears with a particular class in the training data, making `P(xᵢ | y) = 0`.

**Problem:** Since we multiply probabilities, a single zero makes the entire posterior probability **zero**, regardless of all other evidence:

$$P(y \mid X) \propto P(y) \prod_i P(x_i \mid y) = 0 \text{ if any } P(x_i \mid y) = 0$$

**Example:** If the word "cryptocurrency" never appeared in training spam emails, a test email containing it would never be classified as spam.

---

---

## ML-103: How can KNN handle imbalanced datasets?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-104: How do you choose K?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-105: How does KNN make predictions?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-106: How does KNN perform regression?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-107: What conditional independence assumption does it make?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

Given the class label `y`, all features `x₁, x₂, ..., xₙ` are assumed to be **mutually independent**:

$$P(x_1, x_2, \ldots, x_n \mid y) = \prod_{i=1}^{n} P(x_i \mid y)$$

This means:
- Knowing `x₁` gives no additional information about `x₂` once we know `y`
- Joint probability decomposes into a product of marginals
- This reduces parameter estimation from exponential to linear in the number of features

---

---

## ML-108: What distance metrics can KNN use?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-109: What happens when K is too large?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

When K is **too large** (e.g., K = n):

- The model becomes **too smooth** — predicts the same class for almost everything (the majority class)
- **Underfits** — ignores local structure
- **High bias, low variance**
- Decision boundary becomes overly simple
- Performance degrades toward the baseline (most frequent class)

> The sweet spot for K lies between these two extremes, found via cross-validation.

---

---

## ML-110: What happens when K is too small?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

When K is **too small** (e.g., K=1):

- The model becomes **highly sensitive** to individual data points
- It **overfits** — captures noise and outliers
- **High variance, low bias**
- Decision boundary is very complex and irregular
- Perfect or near-perfect accuracy on training data but poor generalization

> K=1 means the prediction equals the label of the single nearest neighbor — the model memorizes the training data.

---

---

## ML-111: Why is KNN called a lazy learner?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-112: Why is feature scaling important?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-113: Why is it called naive?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** MEDIUM

It is called **naive** because it makes a simplifying assumption that is rarely true in real data:

> All features are **conditionally independent** of each other given the class label.

**Example:** In spam detection, the words "free" and "money" are treated as independent given the email is spam — but in reality, they often appear together.

- This assumption simplifies computation dramatically
- Despite being "wrong," the classifier still performs well because it only needs to rank classes (relative probabilities), not compute exact probabilities

---

---

## ML-114: What are KNN's computational limitations?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** LOWER

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

---

## ML-115: What are Naive Bayes limitations?

**Domain:** Topic 22: Naive Bayes and K-Nearest Neighbors &nbsp;|&nbsp; **Priority:** LOWER

| Limitation | Explanation |
|-----------|-------------|
| **Conditional independence assumption** | Features are rarely independent in reality |
| **Poor probability estimates** | Posteriors are often overconfident (near 0 or 1) |
| **Continuous features** | Gaussian assumption may not hold |
| **Feature correlations ignored** | Correlated features can skew results |
| **Zero probabilities** | Requires smoothing to handle unseen features |
| **Not suitable for regression** | It's a purely probabilistic classifier |
| **Cannot learn feature interactions** | Each feature is treated independently |

**When Naive Bayes still works well:**
- When the independence assumption approximately holds
- High-dimensional sparse data (text)
- Small training datasets (needs fewer parameters)
- When you need a fast, interpretable baseline

---

## ML-116: What are Decision Tree advantages?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-117: What are pre-pruning and post-pruning?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-118: What are root, internal, and leaf nodes?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-119: What is Gini impurity?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-120: What is a Decision Tree?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-121: What is entropy?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-122: What is information gain?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-123: What is maximum depth?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-124: What is minimum samples leaf?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-125: What is minimum samples split?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-126: What is the difference between Gini and entropy?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** HIGH

| Property | Gini Impurity | Entropy |
|----------|--------------|---------|
| **Formula** | `1 - Σpₖ²` | `-Σpₖ log₂(pₖ)` |
| **Computation** | Faster (no log) | Slightly slower |
| **Range (binary)** | [0, 0.5] | [0, 1] |
| **Bias** | Slightly favors larger partitions | More balanced splits |
| **Practical difference** | Very similar results | Very similar results |

**In practice:** The choice between Gini and Entropy rarely makes a significant difference in model performance. Gini is the **default** in scikit-learn due to its lower computational cost.

---

---

## ML-127: Can Regression Trees extrapolate?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

**No — Regression Trees cannot extrapolate beyond the range of training data.**

- Predictions are bounded by the range of training labels (`min(y_train)` to `max(y_train)`)
- For inputs outside the training range, the tree returns the mean of the closest boundary leaf
- This is a **fundamental limitation** compared to linear regression

```python
import numpy as np

X_train = np.arange(1, 11).reshape(-1, 1)
y_train = X_train.ravel() * 2   # y = 2x, range [2, 20]

reg = DecisionTreeRegressor().fit(X_train, y_train)

# Extrapolation attempt: x=20 → still predicts ~20, NOT 40
print(reg.predict([[20]]))   # Returns max leaf mean, not 40
```

**Contrast:** Linear regression would correctly predict y=40 for x=20.

---

---

## ML-128: How do you prune a Regression Tree?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

### Pre-pruning (Constraining Growth)
```python
reg = DecisionTreeRegressor(
    max_depth=5,              # Limit depth
    min_samples_split=10,     # Min samples to split a node
    min_samples_leaf=5,       # Min samples in a leaf
    max_leaf_nodes=20,        # Limit total number of leaves
    random_state=42
)
```

### Post-pruning (Cost-Complexity Pruning)
```python
# Find effective alphas
path = DecisionTreeRegressor().cost_complexity_pruning_path(X_train, y_train)
ccp_alphas = path.ccp_alphas[:-1]   # Exclude trivial alpha

# Cross-validate each alpha
from sklearn.model_selection import cross_val_score

cv_scores = []
for alpha in ccp_alphas:
    reg = DecisionTreeRegressor(ccp_alpha=alpha, random_state=42)
    score = cross_val_score(reg, X_train, y_train, cv=5, scoring='r2').mean()
    cv_scores.append(score)

best_alpha = ccp_alphas[np.argmax(cv_scores)]
```

---

---

## ML-129: How does a Decision Tree choose a split?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-130: How does a Regression Tree differ from a Classification Tree?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

| Aspect | Classification Tree | Regression Tree |
|--------|-------------------|----------------|
| **Target variable** | Discrete class labels | Continuous numerical values |
| **Leaf prediction** | Majority class | Mean of training samples |
| **Split criterion** | Gini impurity / Entropy | MSE / MAE / Variance reduction |
| **Evaluation** | Accuracy, F1 | MAE, MSE, R² |
| **Output** | Class label | Numerical value |

Both share the same **tree-growing algorithm** — the difference is only in how leaves are evaluated and what they predict.

```python
from sklearn.tree import DecisionTreeRegressor

reg = DecisionTreeRegressor(max_depth=5, random_state=42)
reg.fit(X_train, y_train)
y_pred = reg.predict(X_test)
```

---

---

## ML-131: How does a Regression Tree make predictions?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

For a given input `x`, the tree routes it down the branches using learned rules until it reaches a **leaf node**. The prediction is the **mean of the training samples** in that leaf:

$$\hat{y} = \bar{y}_{\text{leaf}} = \frac{1}{|\mathcal{L}|} \sum_{i \in \mathcal{L}} y_i$$

**Example:**
```
Feature Age ≤ 30?
├── YES → Leaf: mean salary = $45,000 → predict $45,000
└── NO  → Feature Experience > 5?
          ├── YES → Leaf: mean = $95,000 → predict $95,000
          └── NO  → Leaf: mean = $72,000 → predict $72,000
```

---

---

## ML-132: How does tree depth affect performance?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

Tree depth is the primary control of the **bias-variance tradeoff**:

| Depth | Bias | Variance | Effect |
|-------|------|----------|--------|
| Very shallow (1-2) | High | Low | Underfitting — misses important patterns |
| Moderate | Balanced | Balanced | Best generalization (found via CV) |
| Very deep (unlimited) | Low | High | Overfitting — memorizes training data |

```python
import matplotlib.pyplot as plt
from sklearn.model_selection import cross_val_score

depths = range(1, 20)
train_scores, cv_scores = [], []

for d in depths:
    reg = DecisionTreeRegressor(max_depth=d, random_state=42)
    reg.fit(X_train, y_train)
    train_scores.append(reg.score(X_train, y_train))
    cv_scores.append(cross_val_score(reg, X_train, y_train, cv=5).mean())

# Plot: train score increases, cv score peaks then drops
```

> The optimal depth is where cross-validation score peaks — this represents the best trade-off between fitting the data and generalizing to unseen samples.

---

## ML-133: How is feature importance calculated?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

Random Forest feature importance uses **Mean Decrease in Impurity (MDI)** — the total weighted impurity reduction attributable to each feature, averaged over all trees:

$$\text{FI}(j) = \frac{1}{B} \sum_{b=1}^{B} \sum_{\text{nodes in tree}_b \text{ using feature } j} \frac{n_t}{n} \left[\text{Impurity}(t) - \frac{n_L}{n_t}\text{Impurity}(L) - \frac{n_R}{n_t}\text{Impurity}(R)\right]$$

Values are normalized to sum to 1.

```python
import pandas as pd
import matplotlib.pyplot as plt

rf.fit(X_train, y_train)
importances = pd.Series(rf.feature_importances_, index=feature_names)
importances.sort_values(ascending=False).plot(kind='bar', figsize=(10, 4))
plt.title("Feature Importances (MDI)")
plt.tight_layout()
plt.show()
```

> **Warning:** MDI can be **biased toward high-cardinality features**. Use Permutation Importance for a less biased estimate.

---

---

## ML-134: What causes Decision Trees to overfit?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-135: What split criterion is used?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

Regression Trees use **variance reduction** (equivalent to minimizing MSE) as the split criterion:

$$\text{MSE}(t) = \frac{1}{n_t} \sum_{i \in t} (y_i - \bar{y}_t)^2$$

$$\text{Variance Reduction} = \text{MSE}(\text{parent}) - \frac{n_L}{n} \text{MSE}(L) - \frac{n_R}{n} \text{MSE}(R)$$

The split that **maximizes variance reduction** (minimizes weighted child MSE) is chosen.

```python
# Available criteria in scikit-learn
reg_mse = DecisionTreeRegressor(criterion='squared_error')   # default (MSE)
reg_mae = DecisionTreeRegressor(criterion='absolute_error')  # MAE-based
reg_fri = DecisionTreeRegressor(criterion='friedman_mse')    # Improved MSE heuristic
```

---

---

## ML-136: Why do Regression Trees produce piecewise constant predictions?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** MEDIUM

Regression Trees make **axis-aligned, rectangular splits** — each leaf covers a rectangular region of the feature space, and all inputs in that region receive the **same constant prediction** (the leaf mean).

- The prediction surface is a **step function** — flat within each partition
- This is fundamentally different from linear regression which produces a smooth plane

```python
import numpy as np
import matplotlib.pyplot as plt

# Visualizing piecewise constant nature
X = np.linspace(0, 10, 100).reshape(-1, 1)
reg = DecisionTreeRegressor(max_depth=3).fit(X, np.sin(X).ravel())
y_pred = reg.predict(X)
# y_pred will be a staircase approximation of sin(X)
```

> This is why deeper trees are needed to approximate smooth functions — each additional split refines the approximation.

---

---

## ML-137: What are Decision Tree disadvantages?

**Domain:** Topic 23: Decision Trees &nbsp;|&nbsp; **Priority:** LOWER

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

---

## ML-138: What is a strong learner?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

A **strong learner** is a model that achieves **arbitrarily high accuracy** — as close to perfect as desired.

- In practice: a model with high accuracy on the task
- Boosting converts multiple weak learners into a strong learner by aggregating them
- The **final ensemble** is the strong learner, even if each component is weak

---

---

## ML-139: What is a weak learner?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-140: What is bagging?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-141: What is blending?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-142: What is boosting?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-143: What is bootstrap sampling?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-144: What is ensemble learning?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-145: What is out-of-bag evaluation?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-146: What is stacking?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-147: What is the difference between bagging and boosting?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-148: How does bagging reduce variance?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** MEDIUM

Each bootstrap sample trains a model on slightly different data, producing diverse models. When averaged, their individual errors cancel out:

**For `M` models with variance `σ²` and pairwise correlation `ρ`:**

$$\text{Var}(\bar{f}) = \rho \sigma^2 + \frac{1-\rho}{M} \sigma^2$$

- As `M → ∞`, the second term → 0
- The remaining variance `ρσ²` depends on **correlation** between trees
- **Key:** reducing correlation between models (random subspaces, bootstrap) reduces overall variance

> Random Forest further reduces `ρ` by using random feature subsets at each split.

---

---

## ML-149: How does boosting reduce bias?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** MEDIUM

Boosting reduces bias by **sequentially fitting residuals** — each model corrects the previous model's errors:

$$F_m(x) = F_{m-1}(x) + \alpha_m \cdot h_m(x)$$

Where `hₘ` is trained on the **residuals** (or weighted errors) of `F_{m-1}`.

- Even if each `hₘ` is a weak learner (high bias, e.g., a shallow tree), the **sum** of many weak learners approximates a complex function
- This is analogous to **gradient descent in function space**
- With enough iterations, boosting can achieve very low training error

---

---

## ML-150: Why can boosting be sensitive to noisy data?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-151: Why can combining models improve performance?

**Domain:** Topic 24: Ensemble Learning, Bagging and Boosting &nbsp;|&nbsp; **Priority:** MEDIUM

Combining models works when individual models make **different errors**. If model errors are uncorrelated, averaging cancels them out.

**Mathematically (for regression, averaging M models):**

$$\text{Var}(\bar{y}) = \frac{\sigma^2}{M} \quad \text{(if uncorrelated)}$$

Variance drops by factor `M` with `M` uncorrelated models.

**Two conditions for ensemble improvement:**
1. **Diversity** — models should make different mistakes (uncorrelated errors)
2. **Accuracy** — each model should be better than random guessing

> If all models make the same errors (identical), ensembling gives no benefit. The more **diverse** the errors, the more benefit from combining.

---

---

## ML-152: What are its advantages?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are its advantages` is an essential technical question in Topic 25: Random Forest.

**Detailed Technical Breakdown:**
- **Foundational Definition:** Serves as a primary building block within data science, statistical modeling, and applied AI workflows.
- **Operational Logic:** Ensures accurate data processing, statistical validity, and reproducible results in both experimental and production environments.
- **Practical Considerations:** Balances computational efficiency, mathematical correctness, and real-world domain constraints.

**Practical Python Snippet:**
```python
# Standard technical idiom for What are its advantages
import numpy as np

def technical_demonstration():
    return True
```

**Interview Takeaway:**
Explain both the theoretical foundation and practical trade-offs encountered when applying this technique to real-world datasets.

---

## ML-153: What is a Random Forest?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** HIGH

**Random Forest** is an ensemble learning algorithm that builds many **decorrelated decision trees** and aggregates their predictions:

- **Classification**: majority vote across all trees
- **Regression**: mean of all tree predictions
- Introduced by Leo Breiman (2001)
- Combines **bagging** + **random feature selection** to create diverse, accurate trees

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

# Classification
rf_clf = RandomForestClassifier(n_estimators=100, random_state=42)
rf_clf.fit(X_train, y_train)

# Regression
rf_reg = RandomForestRegressor(n_estimators=100, random_state=42)
rf_reg.fit(X_train, y_train)
```

---

---

## ML-154: What is out-of-bag error?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** HIGH

Since each tree is trained on a bootstrap sample (~63.2% of data), ~36.8% of samples are **Out-of-Bag (OOB)** for each tree. These samples can be used to estimate generalization error:

- For each training sample `xᵢ`, collect predictions from all trees where `xᵢ` was **not** in the bootstrap sample
- Aggregate those predictions → OOB prediction for `xᵢ`
- OOB error = error on OOB predictions across all training samples

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,
    oob_score=True,        # Enable OOB evaluation
    random_state=42
)
rf.fit(X_train, y_train)

print(f"OOB Score (Accuracy): {rf.oob_score_:.4f}")
# Access OOB predictions
oob_predictions = rf.oob_decision_function_   # shape: (n_samples, n_classes)
```

> OOB error closely approximates cross-validation error with no extra computational cost.

---

---

## ML-155: What is permutation importance?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** HIGH

**Permutation Importance** measures feature importance by computing how much the model's performance **degrades** when a feature's values are randomly shuffled (breaking its relationship with the target):

$$\text{PI}(j) = \text{Score}(X, y) - \text{Score}(X_{\text{permuted}_j}, y)$$

```python
from sklearn.inspection import permutation_importance

result = permutation_importance(
    rf, X_test, y_test,
    n_repeats=10,       # Repeat permutation 10 times for stability
    random_state=42,
    n_jobs=-1
)

perm_importances = pd.Series(
    result.importances_mean,
    index=feature_names
).sort_values(ascending=False)
print(perm_importances)
```

| | MDI (Built-in) | Permutation Importance |
|-|---------------|----------------------|
| **Speed** | Fast | Slower |
| **Bias** | Biased to high-cardinality | Less biased |
| **Data** | Uses training data | Can use test data |
| **Reliability** | Can overfit | More reliable |

---

---

## ML-156: Can Random Forest overfit?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

**Yes, but it is much harder to overfit than a single Decision Tree:**

- Adding more trees (`n_estimators`) does **not** cause overfitting — error plateaus as trees increase
- However, individual trees can still overfit if not constrained (`max_depth`, `min_samples_leaf`)
- Setting `max_features` too high → more correlated trees → less variance reduction

**When Random Forest can overfit:**
- Very noisy datasets with many irrelevant features
- Very small datasets (high variance in bootstrap samples)
- No depth/leaf constraints on individual trees

```python
# Monitor OOB error as n_estimators increases
oob_errors = []
for n in range(1, 200):
    rf = RandomForestClassifier(n_estimators=n, oob_score=True, random_state=42)
    rf.fit(X_train, y_train)
    oob_errors.append(1 - rf.oob_score_)
# OOB error should decrease and plateau, not increase
```

---

---

## ML-157: How does Random Forest handle imbalanced classes?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

Random Forest, like most algorithms, is biased toward the majority class. Several strategies help:

```python
# 1. class_weight parameter
rf = RandomForestClassifier(
    class_weight='balanced',        # weights inversely proportional to class frequency
    # class_weight='balanced_subsample'  # recalculated per bootstrap sample
    random_state=42
)

# 2. Resampling before training
from imblearn.over_sampling import SMOTE
from imblearn.ensemble import BalancedRandomForestClassifier

# BalancedRandomForestClassifier undersamples majority class in each bootstrap
brf = BalancedRandomForestClassifier(n_estimators=100, random_state=42)
brf.fit(X_train, y_train)

# 3. Adjust decision threshold
probas = rf.predict_proba(X_test)[:, 1]
threshold = 0.3   # Lower threshold favors minority class
y_pred = (probas >= threshold).astype(int)
```

---

---

## ML-158: How does Random Forest reduce correlation between trees?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

Two sources of randomness reduce tree correlation:

1. **Bootstrap sampling**: Each tree trains on a different random data subset
2. **Random feature selection at each split**: Each tree considers different features at each split point

Combined effect — recall the variance formula for an ensemble of `M` trees with correlation `ρ`:

$$\text{Var}(\text{RF}) = \rho \sigma^2 + \frac{1 - \rho}{M} \sigma^2$$

- **Plain bagging**: reduces `(1-ρ)/M` term, but `ρ` remains large if one feature dominates
- **Random Forest**: reduces `ρ` by random feature subsets → further reduces overall variance
- As `M → ∞`, variance approaches `ρσ²` (irreducible, based on remaining correlation)

---

---

## ML-159: How does Random Forest use bagging?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

Random Forest applies **bagging (Bootstrap AGGregating)**:

1. Draw `B` bootstrap samples (with replacement, size `n`) from the training data
2. Train one **full decision tree** on each bootstrap sample
3. At prediction time, aggregate all `B` tree predictions

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,     # B = 100 trees
    bootstrap=True,       # Use bootstrap sampling (True by default)
    random_state=42
)
```

- Each tree sees ~63.2% unique training samples (different subset per tree)
- The remaining ~36.8% are Out-of-Bag (OOB) samples — usable for free validation
- Parallel training: all trees are independent and can be trained simultaneously

---

---

## ML-160: How does max_depth affect the model?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

`max_depth` controls the depth of **individual trees** in the forest:

| `max_depth` | Per-tree Bias | Per-tree Variance | Forest Behavior |
|-------------|-------------|-----------------|----------------|
| Very small (1-3) | High | Low | Underfitting even with many trees |
| Moderate | Balanced | Balanced | Best performance |
| None (unlimited) | Low | High | Trees overfit, but ensemble averages it out |

```python
# Default: max_depth=None (fully grown trees)
# Random Forest is robust to deep trees because averaging reduces variance
rf_deep = RandomForestClassifier(max_depth=None, n_estimators=100)   # typical
rf_shallow = RandomForestClassifier(max_depth=5, n_estimators=100)   # more regularized
```

> Unlike single Decision Trees, Random Forest with `max_depth=None` typically **doesn't drastically overfit** due to averaging — but constraining depth can still help on noisy data.

---

---

## ML-161: How does max_features affect the model?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

`max_features` controls the number of features considered at **each split** — the primary lever for controlling tree diversity:

| `max_features` Value | Effect |
|---------------------|--------|
| Low (e.g., 1) | Very diverse trees, high bias per tree, low correlation |
| `'sqrt'` (default) | Good balance — standard recommendation |
| High (e.g., all features) | Less diverse trees, similar to plain bagging |
| All features | No feature randomness → highest correlation between trees |

```
Trade-off:
Low max_features  →  High tree diversity  →  Lower variance, higher per-tree bias
High max_features →  Low tree diversity   →  Higher variance, lower per-tree bias
```

---

---

## ML-162: What hyperparameters are important?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

| Hyperparameter | Default | Effect |
|---------------|---------|--------|
| `n_estimators` | 100 | Number of trees; more = better (diminishing returns) |
| `max_features` | `'sqrt'` | Features per split; lower = more diversity |
| `max_depth` | None | Max tree depth; lower = less overfitting |
| `min_samples_split` | 2 | Min samples to split; higher = simpler trees |
| `min_samples_leaf` | 1 | Min samples per leaf; higher = smoother predictions |
| `max_leaf_nodes` | None | Max leaves per tree |
| `bootstrap` | True | Whether to use bootstrap sampling |
| `class_weight` | None | Handle class imbalance |
| `n_jobs` | 1 | Parallelism; `-1` = all cores |

```python
from sklearn.model_selection import RandomizedSearchCV

param_dist = {
    'n_estimators': [100, 200, 500],
    'max_depth': [None, 10, 20, 30],
    'max_features': ['sqrt', 'log2', 0.5],
    'min_samples_leaf': [1, 2, 5, 10]
}

rf_search = RandomizedSearchCV(
    RandomForestClassifier(random_state=42),
    param_distributions=param_dist,
    n_iter=20, cv=5, scoring='f1', n_jobs=-1
)
rf_search.fit(X_train, y_train)
print(rf_search.best_params_)
```

---

---

## ML-163: Why are random feature subsets used?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** MEDIUM

At each split, Random Forest considers only a **random subset of `m` features** (instead of all features). This is the key difference from plain bagging:

**Why it helps:**
- If one feature is very dominant, all trees would make similar first splits → **high correlation between trees**
- Random feature subsets **break this correlation** → trees become more diverse
- Diverse trees with uncorrelated errors provide greater variance reduction when averaged

**Default values:**
- Classification: `m = √p` (square root of total features)
- Regression: `m = p/3`

```python
rf = RandomForestClassifier(
    max_features='sqrt',   # √p features per split (default for classification)
    # max_features='log2' # log₂(p) features per split
    # max_features=0.5    # 50% of features per split
    random_state=42
)
```

---

---

## ML-164: What are its disadvantages?

**Domain:** Topic 25: Random Forest &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What are its disadvantages` is an essential technical question in Topic 25: Random Forest.

**Detailed Technical Breakdown:**
- **Foundational Definition:** Serves as a primary building block within data science, statistical modeling, and applied AI workflows.
- **Operational Logic:** Ensures accurate data processing, statistical validity, and reproducible results in both experimental and production environments.
- **Practical Considerations:** Balances computational efficiency, mathematical correctness, and real-world domain constraints.

**Practical Python Snippet:**
```python
# Standard technical idiom for What are its disadvantages
import numpy as np

def technical_demonstration():
    return True
```

**Interview Takeaway:**
Explain both the theoretical foundation and practical trade-offs encountered when applying this technique to real-world datasets.

---

## ML-165: How does subsampling reduce overfitting?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

**Subsampling** injects randomness into the training process, similar to Random Forests:

**Row subsampling (`subsample`):**
```python
model = xgb.XGBRegressor(subsample=0.8)
# 80% of training rows used per tree (without replacement)
```

**Column subsampling (`colsample_bytree`):**
```python
model = xgb.XGBRegressor(colsample_bytree=0.7)
# 70% of features considered per tree
```

**How it reduces overfitting:**
1. Each tree sees a **different random subset** of data/features
2. Prevents individual trees from memorizing specific patterns
3. Reduces **correlation between trees** → better ensemble diversity
4. Similar to the bagging effect in Random Forest

```python
# Stochastic gradient boosting setup
model = xgb.XGBRegressor(
    subsample=0.8,
    colsample_bytree=0.8,
    colsample_bylevel=0.8
)
```

> [!TIP]
> Even `subsample=0.5` can dramatically reduce overfitting on small datasets while maintaining good performance.

---

---

## ML-166: What are gamma, lambda, and alpha?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

| Parameter | Type | Effect | Default |
|---|---|---|---|
| **gamma** | Min split gain | A split is only made if it reduces loss by at least gamma. Higher = fewer splits = simpler trees | 0 |
| **lambda** (reg_lambda) | L2 regularization | Penalizes large leaf weights. Smooths predictions. | 1 |
| **alpha** (reg_alpha) | L1 regularization | Encourages sparse leaf weights (some become 0). Useful for high-dimensional data. | 0 |

```python
# gamma: controls tree depth indirectly
model = xgb.XGBClassifier(gamma=0.5)  # require >0.5 gain to split

# lambda: smooth predictions
model = xgb.XGBClassifier(reg_lambda=5.0)  # stronger L2

# alpha: useful for sparse features
model = xgb.XGBClassifier(reg_alpha=0.1)  # light L1
```

> [!TIP]
> Start with tuning `max_depth`, `learning_rate`, and `n_estimators`. Then use `gamma` and `lambda` for fine-grained regularization.

---

---

## ML-167: What are subsample and colsample_bytree?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

These are **stochastic regularization** parameters that introduce randomness into training:

**`subsample`** — fraction of training rows sampled per tree:
```python
model = xgb.XGBClassifier(subsample=0.8)  # use 80% of rows per tree
```
- Prevents overfitting (like Random Forest's row sampling)
- Reduces correlation between trees

**`colsample_bytree`** — fraction of features sampled per tree:
```python
model = xgb.XGBClassifier(colsample_bytree=0.8)  # use 80% of features
```

**Other column sampling levels:**
| Parameter | Sampling Level |
|---|---|
| `colsample_bytree` | Once per tree |
| `colsample_bylevel` | Once per tree depth level |
| `colsample_bynode` | Once per split |

> [!TIP]
> Values of 0.6–0.9 typically work well. Combined with `subsample`, they significantly reduce overfitting.

---

---

## ML-168: What is AdaBoost?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-169: What is Gradient Boosting?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-170: What is XGBoost feature importance?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

XGBoost provides **three types of feature importance**:

| Type | Description |
|---|---|
| **weight** | Number of times a feature is used to split across all trees |
| **gain** | Average gain in objective function when feature is used to split |
| **cover** | Average number of samples affected by splits on this feature |

```python
import matplotlib.pyplot as plt
from xgboost import plot_importance

# Default is 'weight'
plot_importance(model, importance_type='gain')
plt.show()

# As a dictionary
importance = model.get_booster().get_score(importance_type='gain')
print(sorted(importance.items(), key=lambda x: x[1], reverse=True))
```

> [!TIP]
> `gain` is generally the most informative metric, as it reflects how much each feature contributes to reducing the loss.

---

---

## ML-171: What is XGBoost?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

**XGBoost (Extreme Gradient Boosting)** is an optimized, scalable implementation of gradient boosting developed by Tianqi Chen. It is one of the most widely used ML algorithms in competitions and production.

**Key features:**
- Regularized gradient boosting (L1 + L2)
- Second-order gradient optimization (uses Hessians)
- Built-in handling of missing values
- Tree pruning using `gamma`
- Parallel and distributed computing support
- Column and row subsampling

```python
import xgboost as xgb

model = xgb.XGBClassifier(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=6,
    use_label_encoder=False,
    eval_metric='logloss'
)
model.fit(X_train, y_train)
```

> [!NOTE]
> XGBoost won or contributed to winning solutions in many Kaggle competitions and is widely used in industry for tabular data.

---

---

## ML-172: What is a decision stump?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-173: What is early stopping?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

**Early stopping** halts training when the validation metric stops improving for a set number of rounds, preventing overfitting:

```python
model = xgb.XGBClassifier(
    n_estimators=1000,
    early_stopping_rounds=50,  # stop if no improvement for 50 rounds
    eval_metric='auc'
)

model.fit(
    X_train, y_train,
    eval_set=[(X_val, y_val)],
    verbose=True
)

print(f"Best iteration: {model.best_iteration}")
print(f"Best score: {model.best_score}")
```

**How it works:**
1. After each boosting round, evaluate on a validation set
2. If the metric does not improve for `early_stopping_rounds` consecutive rounds, stop
3. The model from the **best round** is returned

> [!IMPORTANT]
> Always use a held-out validation set (not the training set) for early stopping. Prevents both underfitting and overfitting.

---

---

## ML-174: What is max_depth?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

`max_depth` controls the **maximum depth of each tree** in the ensemble.

- **Deeper trees** → more complex interactions captured → higher variance, lower bias
- **Shallower trees** → simpler model → lower variance, higher bias

| max_depth | Effect |
|---|---|
| 1 | Decision stump (like AdaBoost) |
| 3–6 | Typical range for XGBoost |
| >10 | Usually overfitting |

```python
# Typical tuning range
for depth in [3, 4, 5, 6, 7]:
    model = xgb.XGBClassifier(max_depth=depth)
    # evaluate with cross-validation
```

> [!IMPORTANT]
> XGBoost default is `max_depth=6`. For most tabular problems, values of 3–6 work best. Deeper trees need stronger regularization.

---

---

## ML-175: What is min_child_weight?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

`min_child_weight` is the **minimum sum of instance weights (Hessians)** required in a child node to make a split.

- If a proposed split creates a child node with total Hessian < `min_child_weight`, the split is rejected
- Acts as a **regularization mechanism** against splits on very few or very uncertain samples
- Equivalent to `min_samples_leaf` but in terms of Hessian sum, not sample count

```python
model = xgb.XGBClassifier(
    min_child_weight=5  # require at least 5 Hessian units per leaf
)
```

**Effect:**
- **Higher** → more conservative (fewer splits, simpler trees)
- **Lower** → more splits allowed (risk of overfitting)

> [!NOTE]
> For imbalanced datasets, `min_child_weight=1` may work better since the minority class has low Hessian sums.

---

---

## ML-176: What is shrinkage?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-177: What is the difference between XGBoost and Random Forest?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

| Feature | XGBoost | Random Forest |
|---|---|---|
| **Learning type** | Boosting (sequential) | Bagging (parallel) |
| **Tree building** | Trees correct previous errors | Trees are independent |
| **Bias-variance** | Reduces both bias and variance | Primarily reduces variance |
| **Training speed** | Slower (sequential) | Faster (parallel) |
| **Overfitting risk** | Higher (needs regularization) | Lower (naturally regularized) |
| **Hyperparameter sensitivity** | High | Low |
| **Missing values** | Built-in handling | Requires imputation (sklearn) |
| **Typical performance** | Often better on tabular data | More robust out-of-the-box |
| **Interpretability** | Moderate | Moderate |

```python
from sklearn.ensemble import RandomForestClassifier
import xgboost as xgb

rf = RandomForestClassifier(n_estimators=100)
xgb_model = xgb.XGBClassifier(n_estimators=100)

# Random Forest: good baseline, less tuning
# XGBoost: often better ceiling, needs more tuning
```

> [!TIP]
> Start with Random Forest as a baseline. If you need better performance and are willing to tune, move to XGBoost.

---

## ML-178: What is the learning-rate versus estimators tradeoff?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-179: What is the role of gradients and Hessians?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** HIGH

XGBoost uses a **second-order Taylor expansion** of the loss function to find optimal tree structures:

```
L ≈ Σ [gᵢ · f(xᵢ) + 0.5 · hᵢ · f(xᵢ)²] + Ω(f)
```

- **Gradient (gᵢ)** = first derivative of loss w.r.t. prediction = direction of steepest descent
- **Hessian (hᵢ)** = second derivative of loss = curvature of the loss surface

**Why Hessians matter:**
- They provide a **better quadratic approximation** of the loss
- Allow computation of **optimal leaf values** analytically:
  ```
  w*ⱼ = -Gⱼ / (Hⱼ + λ)
  ```
  Where `Gⱼ = Σgᵢ` and `Hⱼ = Σhᵢ` for samples in leaf j

- Lead to **better split scoring** and faster convergence

> [!NOTE]
> Using second-order information means XGBoost needs fewer trees to achieve the same accuracy compared to first-order GBM.

---

---

## ML-180: Can XGBoost model non-linear relationships?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

**Yes** — XGBoost is inherently non-linear because it uses **decision trees as base learners**:

- Each tree creates **piecewise constant** regions in feature space
- The ensemble of many trees approximates **complex, non-linear functions**
- Automatically captures **feature interactions** at any depth
- No need for manual polynomial features or interaction terms

```python
import numpy as np
import matplotlib.pyplot as plt

# Non-linear data
X = np.linspace(0, 10, 200).reshape(-1, 1)
y = np.sin(X.ravel()) + 0.1 * np.random.randn(200)

model = xgb.XGBRegressor(n_estimators=100, max_depth=4)
model.fit(X, y)

y_pred = model.predict(X)
plt.plot(X, y, 'b.', label='Data')
plt.plot(X, y_pred, 'r-', label='XGBoost')
plt.legend()
plt.show()
```

> [!NOTE]
> Unlike linear regression, XGBoost requires no feature engineering to capture non-linear patterns. However, it cannot **extrapolate beyond the training range** — predictions plateau at the min/max training values.

---

---

## ML-181: How are sample weights updated?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-182: How can boosting models be regularized?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-183: How do you compare XGBoost with Random Forest for regression?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

| Aspect | XGBoost | Random Forest |
|---|---|---|
| **Algorithm** | Sequential boosting | Parallel bagging |
| **Bias-Variance** | Reduces both | Primarily reduces variance |
| **Performance ceiling** | Generally higher | Good out-of-the-box |
| **Tuning effort** | High (many hyperparameters) | Low |
| **Training time** | Slower (sequential) | Faster (parallel) |
| **Overfitting risk** | Higher (needs regularization) | Lower |
| **Outlier sensitivity** | Moderate (with Huber loss) | More robust |
| **Extrapolation** | Cannot extrapolate | Cannot extrapolate |

```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import r2_score

# Random Forest baseline
rf = RandomForestRegressor(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)
rf_r2 = r2_score(y_test, rf.predict(X_test))

# XGBoost
xgb_model = xgb.XGBRegressor(n_estimators=100, max_depth=5,
                               learning_rate=0.1, random_state=42)
xgb_model.fit(X_train, y_train)
xgb_r2 = r2_score(y_test, xgb_model.predict(X_test))

print(f"Random Forest R²: {rf_r2:.4f}")
print(f"XGBoost R²:       {xgb_r2:.4f}")
```

**When to prefer each:**
- **Random Forest:** Quick baseline, noisy data, less time to tune
- **XGBoost:** When pushing for maximum performance, structured tabular data, time to tune properly

---

## ML-184: How do you evaluate an XGBoost Regressor?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

XGBoost regression models are evaluated using **standard regression metrics**:

| Metric | Formula | Interpretation |
|---|---|---|
| **RMSE** | `√(Σ(ŷᵢ - yᵢ)²/n)` | Same unit as target; sensitive to outliers |
| **MAE** | `Σ|ŷᵢ - yᵢ|/n` | More robust to outliers |
| **R²** | `1 - SS_res/SS_tot` | Proportion of variance explained (higher=better) |
| **MAPE** | `Σ|ŷᵢ - yᵢ|/yᵢ · 100%` | Percentage error; avoid when yᵢ≈0 |
| **MSLE** | `Σ(log(ŷ+1) - log(y+1))²/n` | For log-scale targets |

```python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
import numpy as np

y_pred = model.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test, y_pred))
mae  = mean_absolute_error(y_test, y_pred)
r2   = r2_score(y_test, y_pred)

print(f"RMSE: {rmse:.4f}")
print(f"MAE:  {mae:.4f}")
print(f"R²:   {r2:.4f}")
```

**Built-in eval metrics for early stopping:**
```python
model = xgb.XGBRegressor(eval_metric='rmse')
model.fit(X_train, y_train, eval_set=[(X_val, y_val)])
```

---

---

## ML-185: How do you tune an XGBoost Regressor?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

**Recommended tuning sequence:**

```python
from sklearn.model_selection import RandomizedSearchCV
import numpy as np

param_grid = {
    'n_estimators': [200, 500, 1000],
    'max_depth': [3, 4, 5, 6],
    'learning_rate': [0.01, 0.05, 0.1],
    'subsample': [0.6, 0.8, 1.0],
    'colsample_bytree': [0.6, 0.8, 1.0],
    'min_child_weight': [1, 3, 5],
    'gamma': [0, 0.1, 0.5],
    'reg_alpha': [0, 0.1, 1.0],
    'reg_lambda': [0.5, 1.0, 5.0]
}

model = xgb.XGBRegressor(objective='reg:squarederror', tree_method='hist')

search = RandomizedSearchCV(
    model, param_grid,
    n_iter=50, cv=5,
    scoring='neg_root_mean_squared_error',
    n_jobs=-1, random_state=42
)
search.fit(X_train, y_train)
print(search.best_params_)
```

**Tuning priority order:**
1. `max_depth` + `min_child_weight` (tree structure)
2. `subsample` + `colsample_bytree` (randomness)
3. `gamma` (pruning)
4. `reg_alpha` + `reg_lambda` (leaf regularization)
5. `learning_rate` + `n_estimators` (finalize with early stopping)

---

---

## ML-186: How does AdaBoost train models sequentially?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-187: How does Gradient Boosting differ from AdaBoost?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-188: How does XGBoost differ from traditional Gradient Boosting?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

| Feature | Traditional GBM | XGBoost |
|---|---|---|
| **Optimization** | First-order gradients | Second-order (gradient + Hessian) |
| **Regularization** | None (sklearn) | L1 (alpha) + L2 (lambda) |
| **Missing values** | Manual imputation | Built-in handling |
| **Tree pruning** | Pre-pruning (max_depth) | Post-pruning with gamma |
| **Speed** | Slow | Much faster (parallel, cache-aware) |
| **Subsampling** | Row only | Row + column + level |
| **Cross-validation** | Separate step | Built-in `cv()` |

```python
# XGBoost with DMatrix for maximum performance
dtrain = xgb.DMatrix(X_train, label=y_train)
dval = xgb.DMatrix(X_val, label=y_val)

params = {'max_depth': 6, 'eta': 0.1, 'objective': 'binary:logistic'}
model = xgb.train(params, dtrain, num_boost_round=100,
                  evals=[(dval, 'val')], early_stopping_rounds=10)
```

---

---

## ML-189: How does XGBoost handle missing values?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

XGBoost has a **built-in sparsity-aware split finding algorithm**:

1. For each feature with missing values, XGBoost tries assigning missing samples to the **left** or **right** child
2. Whichever direction produces a **better gain** is chosen as the **default direction**
3. At inference time, missing values automatically follow the learned default direction

```python
import numpy as np

# Missing values handled natively — no imputation needed
X_train[5, 2] = np.nan  # XGBoost handles this automatically
model = xgb.XGBClassifier()
model.fit(X_train, y_train)
```

> [!TIP]
> This is a major advantage over scikit-learn's GradientBoostingClassifier, which requires explicit imputation before training.

---

---

## ML-190: How does early stopping work?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

Early stopping monitors validation performance and **stops training when it stops improving**:

```python
model = xgb.XGBRegressor(
    n_estimators=2000,
    learning_rate=0.05,
    early_stopping_rounds=50,   # stop after 50 rounds with no improvement
    eval_metric='rmse'
)

model.fit(
    X_train, y_train,
    eval_set=[(X_val, y_val)],
    verbose=100  # print every 100 rounds
)

# Access results
print(f"Best iteration: {model.best_iteration}")
print(f"Best RMSE: {model.best_score:.4f}")
```

**Mechanism:**
1. After each tree, compute metric on `eval_set`
2. Track the **best score seen** so far
3. If no improvement for `early_stopping_rounds` consecutive rounds → stop
4. Final model uses weights from the **best iteration**

> [!IMPORTANT]
> The eval_set must be a **held-out validation set** not used in training. Using training data for early stopping defeats the purpose.

---

---

## ML-191: How does max_depth affect regression?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

`max_depth` controls the **complexity of each regression tree**:

| max_depth | Tree Complexity | Behavior |
|---|---|---|
| 2–3 | Simple, linear-ish | High bias, captures only simple patterns |
| 4–6 | Moderate | Good balance; most common range |
| 7–10 | Complex | Risk of overfitting |
| >10 | Very deep | Almost certainly overfitting |

```python
import matplotlib.pyplot as plt
from sklearn.model_selection import cross_val_score

depths = range(2, 10)
cv_scores = []

for d in depths:
    m = xgb.XGBRegressor(max_depth=d, n_estimators=100, learning_rate=0.1)
    scores = cross_val_score(m, X_train, y_train,
                             cv=5, scoring='neg_root_mean_squared_error')
    cv_scores.append(-scores.mean())

plt.plot(list(depths), cv_scores)
plt.xlabel('max_depth')
plt.ylabel('CV RMSE')
plt.title('max_depth vs RMSE')
plt.show()
```

> [!NOTE]
> In regression with many features and complex interactions, `max_depth=6` is a good starting point. Lower to 3–4 if overfitting is observed.

---

---

## ML-192: How does scale_pos_weight handle class imbalance?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

`scale_pos_weight` balances positive and negative class weights for **imbalanced binary classification**:

```
scale_pos_weight = count(negative) / count(positive)
```

```python
import numpy as np

neg = np.sum(y_train == 0)
pos = np.sum(y_train == 1)
ratio = neg / pos

model = xgb.XGBClassifier(scale_pos_weight=ratio)
model.fit(X_train, y_train)
```

**Effect:** Multiplies the gradient and Hessian of positive class samples by `scale_pos_weight`, making them matter more in the optimization.

| Scenario | Recommended `scale_pos_weight` |
|---|---|
| Balanced (50/50) | 1 |
| 10:1 imbalance | 10 |
| 100:1 imbalance | 100 |

> [!NOTE]
> For multi-class imbalance, use `sample_weight` in `fit()` instead, or resample your data.

---

---

## ML-193: What causes boosting to overfit?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-194: What objectives can XGBoost use for regression?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

XGBoost supports multiple **regression objectives**:

| Objective | Description | Use Case |
|---|---|---|
| `reg:squarederror` | Mean Squared Error (MSE) | Standard regression (default) |
| `reg:squaredlogerror` | Mean Squared Log Error | Targets with exponential scale |
| `reg:absoluteerror` | Mean Absolute Error | Robust to outliers |
| `reg:pseudohubererror` | Huber loss | Balance between MSE and MAE |
| `reg:tweedie` | Tweedie regression | Insurance, count data with zeros |
| `count:poisson` | Poisson regression | Count data |
| `survival:cox` | Cox proportional hazards | Survival analysis |

```python
import xgboost as xgb

# Standard regression
model = xgb.XGBRegressor(objective='reg:squarederror')

# Huber loss (more robust to outliers)
model = xgb.XGBRegressor(objective='reg:pseudohubererror')

# Log-scale targets (e.g., house prices)
model = xgb.XGBRegressor(objective='reg:squaredlogerror')

model.fit(X_train, y_train)
```

> [!TIP]
> Use `reg:absoluteerror` or `reg:pseudohubererror` when your target variable has significant outliers.

---

---

## ML-195: What regularization does XGBoost use?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

XGBoost adds a **regularization term** directly to the objective:

```
Ω(f) = γ · T + 0.5 · λ · Σ wⱼ²  + α · Σ |wⱼ|
```

Where:
- **T** = number of leaves in the tree
- **γ (gamma)** = minimum loss reduction required for a split (complexity penalty on number of leaves)
- **λ (lambda)** = L2 regularization on leaf weights
- **α (alpha)** = L1 regularization on leaf weights
- **wⱼ** = weight (output value) of leaf j

This penalizes both:
- **Model complexity** (too many leaves via gamma)
- **Large leaf weights** (via lambda/alpha)

```python
model = xgb.XGBClassifier(
    gamma=0.1,      # min gain to make a split
    reg_lambda=1.0, # L2
    reg_alpha=0.0   # L1
)
```

---

---

## ML-196: Why are misclassified samples given more weight?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

The philosophy is **"focus on your mistakes"**:

- If a sample was misclassified, the next learner should **pay more attention** to it
- By increasing its weight, the next weak learner is effectively **penalized more** for getting it wrong
- This forces successive learners to specialize in **hard-to-classify regions**
- Over many rounds, the ensemble covers the entire feature space more thoroughly

> [!TIP]
> This adaptive reweighting is what makes AdaBoost fundamentally different from Bagging — each learner is not independent but builds on the errors of its predecessors.

---

---

## ML-197: Why is AdaBoost sensitive to outliers?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-198: Why is XGBoost computationally efficient?

**Domain:** Topic 26: Gradient Boosting, AdaBoost and XGBoost &nbsp;|&nbsp; **Priority:** MEDIUM

XGBoost is optimized at multiple levels:

1. **Parallel split finding** — candidate splits are evaluated in parallel using pre-sorted data
2. **Approximate split finding** — uses quantile sketches instead of checking all thresholds
3. **Cache-aware access** — data is stored in column-major format (CSC) for efficient access
4. **Block structure** — data blocks are pre-sorted and cached to reduce I/O
5. **Sparsity handling** — zero/missing values are skipped efficiently
6. **Out-of-core computing** — can handle data larger than RAM using block compression
7. **GPU support** — `tree_method='gpu_hist'` for GPU-accelerated training

```python
# GPU-accelerated training
model = xgb.XGBClassifier(
    tree_method='hist',       # fast histogram algorithm
    device='cuda'             # use GPU
)

# Histogram-based (faster, approximate)
model = xgb.XGBClassifier(tree_method='hist')
```

> [!NOTE]
> `tree_method='hist'` (histogram-based) is the recommended method for large datasets — it's orders of magnitude faster than the exact method.

---

---

## ML-199: What is DBSCAN?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-200: What is Hierarchical Clustering?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-201: What is K-Means?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-202: What is Ward linkage?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-203: What is a border point?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-204: What is a centroid?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-205: What is a core point?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-206: What is a dendrogram?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-207: What is a k-distance plot?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-208: What is a noise point?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-209: What is agglomerative clustering?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-210: What is average linkage?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-211: What is complete linkage?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-212: What is divisive clustering?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-213: What is inertia?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-214: What is single linkage?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-215: What is the Silhouette Score?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-216: What is the elbow method?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-217: What is the range of the score?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-218: How can PCA help clustering?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-219: How do outliers affect K-Means?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-220: How do you choose between K-Means and DBSCAN?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-221: How do you choose clusters from a dendrogram?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-222: How do you choose epsilon?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-223: How do you evaluate whether clusters are useful?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-224: How do you explain clusters to stakeholders?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-225: How do you handle categorical variables?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle categorical variables` is an essential technical question in Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN.

**Detailed Technical Breakdown:**
- **Foundational Definition:** Serves as a primary building block within data science, statistical modeling, and applied AI workflows.
- **Operational Logic:** Ensures accurate data processing, statistical validity, and reproducible results in both experimental and production environments.
- **Practical Considerations:** Balances computational efficiency, mathematical correctness, and real-world domain constraints.

**Practical Python Snippet:**
```python
# Standard technical idiom for How do you handle categorical variables
import numpy as np

def technical_demonstration():
    return True
```

**Interview Takeaway:**
Explain both the theoretical foundation and practical trade-offs encountered when applying this technique to real-world datasets.

---

## ML-226: How do you handle outliers before clustering?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-227: How does DBSCAN discover clusters?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-228: How does DBSCAN handle outliers?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-229: How does K-Means work step by step?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-230: How is it used to choose K?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-231: How would you cluster customers for segmentation?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-232: How would you preprocess customer data for clustering?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-233: What assumptions does K-Means make?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-234: What do epsilon and min_samples represent?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-235: What does a high score indicate?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-236: What does a negative score indicate?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-237: What objective function does K-Means minimize?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-238: Why can DBSCAN find arbitrary shapes?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-239: Why can K-Means converge to a local optimum?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-240: Why does DBSCAN struggle with varying density?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-241: What are Hierarchical Clustering limitations?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** LOWER

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

---

## ML-242: What are K-Means limitations?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** LOWER

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

---

## ML-243: What are its limitations?

**Domain:** Topic 27: Clustering: K-Means, Hierarchical Clustering and DBSCAN &nbsp;|&nbsp; **Priority:** LOWER

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

---

## ML-244: How do learning curves diagnose bias and variance?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-245: What is bias?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** HIGH

**Bias** is the error introduced by approximating a real-world problem (which may be complex) with a simplified model.

- It measures how far off the model's **average prediction** is from the true value.
- High bias → model makes strong, incorrect assumptions about the data.
- Mathematically: `Bias² = (E[ŷ] - y)²`

**Example:** Using a linear model to fit a quadratic relationship — the model is systematically wrong.

```python
# High bias example: underpowered model
from sklearn.linear_model import LinearRegression
model = LinearRegression()  # too simple for a non-linear problem
```

> **Key insight:** Bias is a property of the model's structure, not a specific training run.

---

---

## ML-246: What is high bias?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** HIGH

**High bias** occurs when a model is **too simple** to capture the underlying patterns in the data.

**Symptoms:**
- High training error
- High test error (similar to training error)
- Model performs poorly on both seen and unseen data

**Causes:**
- Too few features
- Model is too simple (e.g., linear model for non-linear data)
- Too much regularization

**Indicators:**
| Metric | High Bias |
|--------|-----------|
| Training Error | High |
| Validation Error | High |
| Gap (Val - Train) | Small |

---

---

## ML-247: What is high variance?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** HIGH

**High variance** occurs when a model is **too complex** and memorizes the training data, including noise.

**Symptoms:**
- Very low training error
- High test/validation error
- Large gap between training and validation performance

**Causes:**
- Too many features / overly complex model
- Too little training data
- Insufficient regularization

**Indicators:**
| Metric | High Variance |
|--------|---------------|
| Training Error | Low |
| Validation Error | High |
| Gap (Val - Train) | Large |

---

---

## ML-248: What is the bias-variance tradeoff?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** HIGH

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

---

## ML-249: What is variance?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** HIGH

**Variance** is the model's sensitivity to small fluctuations in the training data.

- It measures how much the model's predictions **change across different training sets**.
- High variance → model learns noise in training data and doesn't generalize.
- Mathematically: `Variance = E[(ŷ - E[ŷ])²]`

**Example:** A deep decision tree trained on different random subsets of data produces very different predictions for the same input.

```python
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier(max_depth=None)  # high variance — no pruning
```

> **Key insight:** Variance reflects instability in learning — different data → very different model.

---

---

## ML-250: How can you reduce high bias?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** MEDIUM

High bias = model too simple → **increase model complexity**.

**Strategies:**

1. **Use a more complex model** — deeper tree, more layers, higher-degree polynomial
2. **Add more features** — feature engineering, polynomial features
3. **Reduce regularization** — lower λ in Ridge/Lasso
4. **Train longer** — more epochs for neural networks
5. **Use a different algorithm** — switch from linear to tree-based or neural network

```python
# Reduce bias: increase polynomial degree
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.linear_model import LinearRegression

model = make_pipeline(PolynomialFeatures(degree=3), LinearRegression())
model.fit(X_train, y_train)
```

> **Rule of thumb:** If both training and validation error are high → reduce bias.

---

---

## ML-251: How can you reduce high variance?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** MEDIUM

High variance = model too complex → **constrain or regularize the model**.

**Strategies:**

1. **Get more training data** — most effective solution
2. **Apply regularization** — L1 (Lasso), L2 (Ridge), Dropout
3. **Reduce model complexity** — fewer layers, shallower trees, pruning
4. **Use cross-validation** — choose model with best CV score
5. **Feature selection** — remove irrelevant/noisy features
6. **Ensemble methods** — Bagging (Random Forest) averages out variance
7. **Early stopping** — stop training before overfitting in neural networks
8. **Data augmentation** — artificially expand training data

```python
from sklearn.linear_model import Ridge

# L2 regularization reduces variance
model = Ridge(alpha=1.0)  # higher alpha = more regularization
model.fit(X_train, y_train)
```

> **Rule of thumb:** If training error is low but validation error is high → reduce variance.

---

## ML-252: How does bagging affect variance?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-253: How does boosting affect bias?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-254: How does regularization affect it?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## ML-255: Why does the tradeoff occur?

**Domain:** Topic 29: Bias-Variance Tradeoff and Generalization &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

