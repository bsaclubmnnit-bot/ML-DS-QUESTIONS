# Section 4: Logistic Regression

## Q51. What is Logistic Regression?

Logistic Regression is a supervised learning algorithm used for **binary (and multiclass) classification**. Despite the name "regression", it predicts the probability of a class label using the **logistic (sigmoid) function** to squash a linear combination of features into the [0, 1] range.

$$\hat{y} = \sigma(w^T x + b) = \frac{1}{1 + e^{-(w^T x + b)}}$$

If $\hat{y} \geq 0.5$, predict class 1; else class 0.

---

## Q52. Why is Logistic Regression used for classification?

Linear regression can predict values outside [0, 1], making it unsuitable for probabilities. Logistic Regression:
- Outputs values in (0, 1) via the sigmoid function
- Models the **log-odds** of the class as a linear function
- Has a well-defined probabilistic interpretation
- Uses a convex loss function (binary cross-entropy) with a global minimum

---

## Q53. What is the sigmoid function?

$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

Properties:
- Output range: (0, 1)
- $\sigma(0) = 0.5$
- Monotonically increasing
- Derivative: $\sigma'(z) = \sigma(z)(1 - \sigma(z))$

It maps any real number to a probability value.

---

## Q54. What are odds and log-odds?

**Odds** = ratio of probability of success to probability of failure:
$$\text{Odds} = \frac{p}{1 - p}$$

**Log-odds (logit)** = natural log of the odds:
$$\text{logit}(p) = \ln\left(\frac{p}{1-p}\right) = w^T x + b$$

Logistic Regression models log-odds as a **linear function** of features. This is why it's called "logistic".

---

## Q55. What is a logistic decision boundary?

The decision boundary is the set of points where $\hat{p} = 0.5$, which means:
$$w^T x + b = 0$$

This is a **linear hyperplane** in feature space. For 2D features, it's a line; for 3D, a plane. Non-linear boundaries can be created by adding polynomial features.

---

## Q56. What loss function is used?

Logistic Regression uses **Binary Cross-Entropy (Log Loss)**:

$$\mathcal{L} = -\frac{1}{n} \sum_{i=1}^n \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]$$

This penalizes confident wrong predictions much more heavily than uncertain ones.

---

## Q57. What is binary cross-entropy?

Binary cross-entropy measures the **difference between the true label distribution and the predicted probability distribution**:

- If $y=1$: loss = $-\log(\hat{p})$ — penalizes low predicted probability for positive class
- If $y=0$: loss = $-\log(1 - \hat{p})$ — penalizes high predicted probability for negative class

As $\hat{p} \to 1$ when $y=1$: loss → 0. As $\hat{p} \to 0$ when $y=1$: loss → ∞.

---

## Q58. What is maximum likelihood estimation?

MLE finds parameters that **maximize the probability of observing the training data**.

For logistic regression, the likelihood is:
$$\mathcal{L}(\theta) = \prod_{i=1}^n \hat{p}_i^{y_i} (1 - \hat{p}_i)^{1 - y_i}$$

Taking the negative log gives binary cross-entropy. So **minimizing cross-entropy = maximizing likelihood**.

---

## Q59. What does a predicted probability represent?

$\hat{p} = P(y=1 | x)$ — the probability that the given input belongs to the positive class.

Example: If a spam classifier outputs 0.87, there is an 87% chance the email is spam. This is calibrated if the model is well-trained on representative data.

---

## Q60. How does changing the classification threshold affect predictions?

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

## Q61. What is multinomial Logistic Regression?

Extends binary logistic regression to **K > 2 classes** (also called **Softmax Regression**).

$$P(y=k | x) = \frac{e^{w_k^T x}}{\sum_{j=1}^K e^{w_j^T x}}$$

The softmax function normalizes outputs so all class probabilities sum to 1. Used in neural network output layers for multi-class classification.

---

## Q62. What is one-vs-rest classification?

**OvR (One-vs-Rest)** trains K binary classifiers, one per class. Each classifier learns to separate class k from all others.

```python
from sklearn.linear_model import LogisticRegression
# multi_class='ovr' is one approach
model = LogisticRegression(multi_class='ovr')
```

For prediction, pick the class with the highest score. Simpler than multinomial but less theoretically elegant.

---

## Q63. How are Logistic Regression coefficients interpreted?

Coefficients represent the **change in log-odds** per unit increase in a feature:

$$\Delta \text{log-odds} = w_j \cdot \Delta x_j$$

More interpretable: **exponentiated coefficient** $e^{w_j}$ = **odds ratio**. If $e^{w_j} = 2$, then a 1-unit increase in $x_j$ doubles the odds of the positive class.

---

## Q64. How do you handle class imbalance?

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

## Q65. How does regularization work in Logistic Regression?

Regularization adds a penalty to the loss to prevent overfitting:

- **L2 (Ridge)**: $\mathcal{L} + \frac{1}{2C} \|w\|^2$ — shrinks all coefficients
- **L1 (Lasso)**: $\mathcal{L} + \frac{1}{C} \|w\|_1$ — can zero out coefficients (feature selection)

In scikit-learn, `C = 1/λ` (inverse regularization strength):
- Small C → strong regularization
- Large C → weak regularization

```python
model = LogisticRegression(C=0.1, penalty='l2')  # Strong L2 regularization
```

