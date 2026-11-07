# Section 1: Regression & Classification Fundamentals

## Q1. What is the difference between supervised learning and unsupervised learning?

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

## Q2. What is the difference between regression and classification?

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

## Q3. What is binary classification?

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

## Q4. What is multiclass classification?

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

## Q5. What is multilabel classification?

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

## Q6. What are features and target variables?

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

## Q7. What is a loss function?

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

## Q8. What is an objective function?

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

## Q9. What is empirical risk minimization?

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

## Q10. What is overfitting?

**Overfitting** occurs when a model learns the training data **too well**, including its noise and random fluctuations, resulting in **poor performance on unseen data**.

- The model has **high variance** and **low bias**.
- It memorizes training data rather than learning generalizable patterns.

**Symptoms:**
- Very low training error, but high validation/test error
- Large gap between train and validation performance

**Causes:**
- Model is too complex (too many parameters)
- Insufficient training data
- Training too long (neural networks)
- Lack of regularization

**Prevention strategies:**
- Regularization (L1, L2, Dropout)
- Cross-validation
- More training data / data augmentation
- Early stopping
- Pruning (Decision Trees)
- Reducing model complexity

```python
# Example: overfitted polynomial regression
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.linear_model import LinearRegression

# Degree 15 polynomial → likely overfits
overfit_model = make_pipeline(PolynomialFeatures(15), LinearRegression())
overfit_model.fit(X_train, y_train)
# train score high, test score low
```

---

## Q11. What is underfitting?

**Underfitting** occurs when a model is **too simple** to capture the underlying patterns in the data, resulting in poor performance on both training and test data.

- The model has **high bias** and **low variance**.
- It fails to learn the signal in the data.

**Symptoms:**
- High training error AND high validation/test error
- Training and validation errors are close but both high

**Causes:**
- Model too simple (e.g., linear model for non-linear data)
- Too few features
- Too much regularization
- Insufficient training time (neural networks)

**Solutions:**
- Increase model complexity
- Add more relevant features / feature engineering
- Reduce regularization
- Train longer

```
              Underfitting     Good Fit     Overfitting
Bias:            High           Low           Low
Variance:        Low            Low           High
Train Error:     High           Low           Very Low
Test Error:      High           Low           High
```

---

## Q12. What is generalization?

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

## Q13. What is regularization?

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

## Q14. What is a decision boundary?

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

## Q15. What is the difference between parametric and non-parametric models?

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
