# Part I: Data Science Foundations

> **212 Interview Questions & Comprehensive Technical Solutions**  
> *Topics: Statistics, Probability, Hypothesis Testing, EDA, Feature Engineering & Preprocessing*  
> *Part of the [PIXEL CHAMP Master Question Bank](https://github.com/bsaclubmnnit-bot/ML-DS-QUESTIONS)*

---

## STAT-001: What are independent events?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are independent events` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-002: What are mutually exclusive events?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are mutually exclusive events` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-003: What are population and sample?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are population and sample` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-004: What are simple random sampling and stratified sampling?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are simple random sampling and stratified sampling` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-005: What is Bonferroni correction?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Bonferroni correction` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-006: What is Pearson correlation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Pearson correlation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-007: What is Simpson's paradox?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Simpson's paradox` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-008: What is Spearman correlation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Spearman correlation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-009: What is a Z-score?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Z-score` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-010: What is a confidence interval?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a confidence interval` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-011: What is a confidence level?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a confidence level` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-012: What is a confounding variable?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a confounding variable` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-013: What is a continuous random variable?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a continuous random variable` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-014: What is a discrete random variable?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a discrete random variable` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-015: What is a non-parametric test?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a non-parametric test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-016: What is a parameter?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a parameter` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-017: What is a percentile?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a percentile` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-018: What is a quantile?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a quantile` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-019: What is a random variable?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a random variable` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-020: What is a statistic?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a statistic` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-021: What is bootstrapping?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is bootstrapping` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-022: What is cluster sampling?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is cluster sampling` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-023: What is coefficient of variation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is coefficient of variation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-024: What is confounding?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is confounding` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-025: What is correlation coefficient range?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is correlation coefficient range` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-026: What is correlation matrix?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is correlation matrix` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-027: What is correlation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is correlation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-028: What is covariance matrix?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is covariance matrix` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-029: What is covariance?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is covariance` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-030: What is expected value?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is expected value` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-031: What is false discovery rate?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is false discovery rate` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-032: What is kurtosis?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is kurtosis` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-033: What is mean?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is mean` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-034: What is median?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is median` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-035: What is mode?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is mode` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-036: What is negative skewness?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is negative skewness` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-037: What is permutation testing?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is permutation testing` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-038: What is positive skewness?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is positive skewness` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-039: What is range?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is range` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-040: What is sampling bias?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is sampling bias` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-041: What is sampling?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is sampling` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-042: What is selection bias?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is selection bias` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-043: What is skewness?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is skewness` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-044: What is standard deviation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is standard deviation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-045: What is statistical power?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is statistical power` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-046: What is survivorship bias?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is survivorship bias` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-047: What is systematic sampling?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is systematic sampling` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-048: What is the Central Limit Theorem?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the Central Limit Theorem` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-049: What is the Empirical Rule?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the Empirical Rule` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-050: What is the Kruskal-Wallis test?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the Kruskal-Wallis test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-051: What is the Law of Large Numbers?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the Law of Large Numbers` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-052: What is the Mann-Whitney U test?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the Mann-Whitney U test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-053: What is the difference between a sample and population variance?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the difference between a sample and population variance` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-054: What is the difference between covariance and correlation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the difference between covariance and correlation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-055: What is the difference between descriptive and inferential statistics?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the difference between descriptive and inferential statistics` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-056: What is the difference between one-tailed and two-tailed tests?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the difference between one-tailed and two-tailed tests` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-057: What is the interquartile range?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the interquartile range` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-058: What is the multiple comparisons problem?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the multiple comparisons problem` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-059: What is variance of a random variable?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is variance of a random variable` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-060: What is weighted mean?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is weighted mean` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-061: Does correlation imply causation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Does correlation imply causation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-062: How do outliers affect mean and standard deviation?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do outliers affect mean and standard deviation` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-063: How do outliers affect median?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do outliers affect median` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-064: How do you detect outliers using IQR?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you detect outliers using IQR` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-065: How would you choose a statistical test for a real business problem?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you choose a statistical test for a real business problem` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-066: What assumptions are required for parametric tests?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What assumptions are required for parametric tests` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-067: When is median preferred over mean?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When is median preferred over mean` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-068: Why are squared deviations used in variance?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why are squared deviations used in variance` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-069: What is geometric mean?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What is geometric mean` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-070: What is harmonic mean?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What is harmonic mean` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-071: What is the Wilcoxon signed-rank test?

**Domain:** Topic 1: Statistics and Descriptive Statistics &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What is the Wilcoxon signed-rank test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-072: What are mean and variance of a Normal distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are mean and variance of a Normal distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-073: What is a Bernoulli distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Bernoulli distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-074: What is a Beta distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Beta distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-075: What is a Binomial distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Binomial distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-076: What is a Gamma distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Gamma distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-077: What is a Log-Normal distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Log-Normal distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-078: What is a Normal distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Normal distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-079: What is a Poisson distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Poisson distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-080: What is a cumulative distribution function?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a cumulative distribution function` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-081: What is a probability density function?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a probability density function` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-082: What is a probability mass function?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a probability mass function` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-083: What is a uniform distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a uniform distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-084: What is an Exponential distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an Exponential distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-085: What is conditional probability?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is conditional probability` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-086: What is probability?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is probability` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-087: What is sampling distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is sampling distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-088: What is the standard Normal distribution?

**Domain:** Topic 2: Probability and Probability Distributions &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the standard Normal distribution` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-089: What is ANOVA?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is ANOVA` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-090: What is a Type I error?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a Type I error` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-091: What is a null hypothesis?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a null hypothesis` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-092: What is a one-sample T-test?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a one-sample T-test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-093: What is a p-value?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a p-value` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-094: What is a paired T-test?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a paired T-test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-095: What is an alternative hypothesis?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an alternative hypothesis` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-096: What is an independent two-sample T-test?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an independent two-sample T-test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-097: What is hypothesis testing?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is hypothesis testing` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-098: What is multiple hypothesis testing?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is multiple hypothesis testing` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-099: What is significance level alpha?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is significance level alpha` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-100: What is statistical significance?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is statistical significance` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-101: What is statistical versus practical significance?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is statistical versus practical significance` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-102: What is the Chi-square test?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the Chi-square test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-103: What is the null hypothesis in ANOVA?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the null hypothesis in ANOVA` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-104: What assumptions does a T-test make?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What assumptions does a T-test make` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-105: When do you use a Chi-square goodness-of-fit test?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When do you use a Chi-square goodness-of-fit test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-106: When do you use a Chi-square test of independence?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When do you use a Chi-square test of independence` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-107: When do you use a Z-test?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When do you use a Z-test` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## STAT-108: When should ANOVA be used?

**Domain:** Topic 3: Hypothesis Testing and Statistical Inference &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When should ANOVA be used` is a fundamental principle in probability theory, descriptive statistics, and experimental design (A/B testing).

**Mathematical Formulation:**
- Under the probability framework, this concept governs distribution properties, expected values, and dispersion:
  $$\mathbb{E}[X] = \int x f(x) dx, \quad \text{Var}(X) = \mathbb{E}[(X - \mu)^2]$$
- Forms the mathematical foundation for sampling error estimation, standard error computation, and hypothesis testing.

**Python Implementation:**
```python
import numpy as np
from scipy import stats

# Empirical simulation and statistical calculation
np.random.seed(42)
sample_data = np.random.normal(loc=100, scale=15, size=1000)

mean = np.mean(sample_data)
std_err = stats.sem(sample_data)
ci_95 = stats.t.interval(0.95, len(sample_data)-1, loc=mean, scale=std_err)
print(f"Sample Mean: {mean:.2f}, 95% CI: {ci_95}")
```

**Interview Takeaway:**
Distinguish sample statistics from population parameters, specify distributional assumptions (normality, independence), and link statistical metrics directly to decision-making thresholds.

---

## EDA-001: How do you detect data leakage during EDA?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How do you detect data leakage during EDA` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-002: What are the first steps when receiving a new dataset?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are the first steps when receiving a new dataset` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-003: What is Exploratory Data Analysis?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Exploratory Data Analysis` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-004: What is a bar chart used for?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a bar chart used for` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-005: What is a box plot used for?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a box plot used for` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-006: What is a histogram used for?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a histogram used for` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-007: What is a scatter plot used for?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a scatter plot used for` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-008: What is a violin plot used for?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a violin plot used for` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-009: What is bivariate analysis?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is bivariate analysis` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-010: What is multivariate analysis?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is multivariate analysis` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-011: How do you analyze a target variable?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze a target variable` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-012: How do you analyze categorical variables?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze categorical variables` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-013: How do you analyze correlation?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze correlation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-014: How do you analyze missingness patterns?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze missingness patterns` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-015: How do you analyze numerical distributions?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze numerical distributions` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-016: How do you analyze relationships between two numerical variables?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze relationships between two numerical variables` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-017: How do you analyze time-based patterns?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you analyze time-based patterns` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-018: How do you avoid misleading visualizations?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you avoid misleading visualizations` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-019: How do you choose the right visualization?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you choose the right visualization` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-020: How do you communicate EDA findings to stakeholders?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you communicate EDA findings to stakeholders` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-021: How do you compare distributions across groups?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you compare distributions across groups` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-022: How do you convert EDA findings into feature engineering ideas?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you convert EDA findings into feature engineering ideas` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-023: How do you create an EDA summary report?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you create an EDA summary report` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-024: How do you detect anomalies?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you detect anomalies` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-025: How do you detect sampling bias during EDA?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you detect sampling bias during EDA` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-026: How do you detect skewness?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you detect skewness` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-027: How do you document data quality issues?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you document data quality issues` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-028: How do you identify class imbalance?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify class imbalance` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-029: How do you identify data types?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify data types` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-030: How do you identify missing values?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify missing values` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-031: How do you identify multicollinearity?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify multicollinearity` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-032: How do you identify outliers?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify outliers` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-033: How do you identify suspicious values?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify suspicious values` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-034: How do you identify trend and seasonality?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify trend and seasonality` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-035: How do you inspect dataset shape and schema?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you inspect dataset shape and schema` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-036: How do you perform univariate analysis?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you perform univariate analysis` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-037: How do you prioritize data cleaning tasks?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you prioritize data cleaning tasks` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-038: How do you validate business rules in data?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you validate business rules in data` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-039: How would you perform EDA before building a machine learning model?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you perform EDA before building a machine learning model` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-040: How would you perform EDA for a customer churn dataset?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you perform EDA for a customer churn dataset` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-041: How would you perform EDA for a sales dataset?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you perform EDA for a sales dataset` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-042: What visualizations help detect outliers?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What visualizations help detect outliers` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-043: Why is EDA important before modeling?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why is EDA important before modeling` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## EDA-044: What are limitations of a correlation matrix?

**Domain:** Topic 4: Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What are limitations of a correlation matrix` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-001: What are MCAR, MAR, and MNAR?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are MCAR, MAR, and MNAR` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-002: What are domain-specific features?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are domain-specific features` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-003: What are filter feature selection methods?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are filter feature selection methods` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-004: What are lag features?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are lag features` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-005: What are risks of target encoding?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are risks of target encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-006: What are rolling window features?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are rolling window features` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-007: What is Min-Max scaling?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Min-Max scaling` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-008: What is PCA?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is PCA` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-009: What is Recursive Feature Elimination?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Recursive Feature Elimination` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-010: What is Robust scaling?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Robust scaling` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-011: What is SelectKBest?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is SelectKBest` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-012: What is binning?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is binning` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-013: What is clipping?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is clipping` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-014: What is date and time feature engineering?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is date and time feature engineering` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-015: What is dimensionality reduction?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is dimensionality reduction` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-016: What is discretization?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is discretization` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-017: What is explained variance?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is explained variance` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-018: What is feature engineering?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature engineering` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-019: What is feature extraction?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature extraction` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-020: What is feature hashing?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature hashing` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-021: What is feature importance?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature importance` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-022: What is feature interaction?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature interaction` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-023: What is feature scaling?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature scaling` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-024: What is feature selection?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature selection` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-025: What is feature skewness?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature skewness` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-026: What is feature transformation?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is feature transformation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-027: What is frequency encoding?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is frequency encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-028: What is label encoding?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is label encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-029: What is log transformation?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is log transformation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-030: What is mutual information?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is mutual information` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-031: What is normalization?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is normalization` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-032: What is one-hot encoding?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is one-hot encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-033: What is ordinal encoding?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is ordinal encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-034: What is polynomial feature generation?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is polynomial feature generation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-035: What is standardization?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is standardization` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-036: What is target encoding?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is target encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-037: What is winsorization?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is winsorization` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-038: How can VIF help feature selection?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How can VIF help feature selection` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-039: How do you extract features from timestamps?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you extract features from timestamps` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-040: How do you identify redundant features?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you identify redundant features` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-041: How do you monitor feature drift?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you monitor feature drift` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-042: How do you validate a feature engineering pipeline?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you validate a feature engineering pipeline` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-043: How would you engineer features for a real business dataset?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you engineer features for a real business dataset` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-044: When is log transformation useful?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When is log transformation useful` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-045: When should Robust scaling be used?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When should Robust scaling be used` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-046: Which algorithms require feature scaling?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Which algorithms require feature scaling` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-047: Why is feature engineering important?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why is feature engineering important` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-048: What is Box-Cox transformation?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What is Box-Cox transformation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-049: What is Yeo-Johnson transformation?

**Domain:** Topic 5: Feature Engineering and Feature Selection &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What is Yeo-Johnson transformation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-050: What are missingness indicators?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are missingness indicators` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-051: What is KNN imputation?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is KNN imputation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-052: What is leakage-prone feature engineering?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is leakage-prone feature engineering` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-053: What is mean imputation?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is mean imputation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-054: What is median imputation?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is median imputation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-055: What is mode imputation?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is mode imputation` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-056: How do pipelines prevent preprocessing leakage?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do pipelines prevent preprocessing leakage` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-057: How do you handle missing numerical values?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle missing numerical values` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-058: How do you handle outliers during feature engineering?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle outliers during feature engineering` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-059: How do you prevent leakage during target encoding?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you prevent leakage during target encoding` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

## FE-060: Why should features be standardized before PCA?

**Domain:** Topic 6: Data Preprocessing and Data Leakage &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why should features be standardized before PCA` addresses a critical stage in the data preparation, exploratory analysis, and feature engineering lifecycle.

**Core Principles & Methodology:**
- **Signal Extraction:** Transforms raw, uncurated input columns into high-signal numerical representations that maximize downstream model performance.
- **Data Leakage Prevention:** All scalers, imputers, and categorical encoders must be fitted strictly on training folds and transformed onto test/validation folds.
- **Distribution Normalization:** Handles skewed distributions via power transforms (Box-Cox / Yeo-Johnson), encodes high-cardinality categories, and captures non-linear feature interactions.

**Production Pipeline Snippet:**
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.impute import SimpleImputer

# Leakage-free preprocessing pipeline
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
    ('encoder', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
])
```

**Interview Takeaway:**
Highlight data leakage risks, explain how to handle missing data mechanisms (MCAR, MAR, MNAR), and justify feature selection choices.

---

