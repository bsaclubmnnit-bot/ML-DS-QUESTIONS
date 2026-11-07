# Section 7: Naive Bayes

---

## Q90. What is Naive Bayes?

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

## Q91. Why is it called "naive"?

It is called **naive** because it makes a simplifying assumption that is rarely true in real data:

> All features are **conditionally independent** of each other given the class label.

**Example:** In spam detection, the words "free" and "money" are treated as independent given the email is spam — but in reality, they often appear together.

- This assumption simplifies computation dramatically
- Despite being "wrong," the classifier still performs well because it only needs to rank classes (relative probabilities), not compute exact probabilities

---

## Q92. What conditional independence assumption does it make?

Given the class label `y`, all features `x₁, x₂, ..., xₙ` are assumed to be **mutually independent**:

$$P(x_1, x_2, \ldots, x_n \mid y) = \prod_{i=1}^{n} P(x_i \mid y)$$

This means:
- Knowing `x₁` gives no additional information about `x₂` once we know `y`
- Joint probability decomposes into a product of marginals
- This reduces parameter estimation from exponential to linear in the number of features

---

## Q93. What is Bayes' Theorem?

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

## Q94. What are prior, likelihood, and posterior probabilities?

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

## Q95. What is Gaussian Naive Bayes?

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

## Q96. What is Multinomial Naive Bayes?

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

## Q97. What is Bernoulli Naive Bayes?

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

## Q98. When is Multinomial Naive Bayes useful?

Multinomial NB is most useful when:

- **Text classification**: Spam filtering, news categorization, sentiment analysis
- **Count-based features**: Word frequencies, term counts
- **Document classification** with Bag-of-Words representations
- When features represent the **number of times** something occurs (non-negative integers)
- When you need a **fast baseline** for NLP tasks

> It is often the **go-to baseline** for text classification tasks because it's fast, interpretable, and handles high-dimensional sparse data efficiently.

---

## Q99. What is the Zero-Frequency Problem?

The **zero-frequency problem** occurs when a feature value never appears with a particular class in the training data, making `P(xᵢ | y) = 0`.

**Problem:** Since we multiply probabilities, a single zero makes the entire posterior probability **zero**, regardless of all other evidence:

$$P(y \mid X) \propto P(y) \prod_i P(x_i \mid y) = 0 \text{ if any } P(x_i \mid y) = 0$$

**Example:** If the word "cryptocurrency" never appeared in training spam emails, a test email containing it would never be classified as spam.

---

## Q100. What is Laplace Smoothing?

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

## Q101. What are Naive Bayes Limitations?

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
