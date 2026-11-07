# Section 32: Common Production Mistakes

---

## Q287. (Section 1 - Regression & Classification Fundamentals) What common mistakes occur when applying this technique in production?

### 1. **Training-Serving Skew**
- The most critical and common production failure: the data pipeline used during training differs from the pipeline used in production.
- Example: Training data was scaled with `StandardScaler` but the production pipeline serves raw, unscaled inputs.
- **Fix:** Package the full preprocessing pipeline (using `sklearn.pipeline.Pipeline`) together with the model and deploy them as a single artifact.

### 2. **Ignoring Data Drift**
- Real-world data distributions change over time (economic shifts, seasonal patterns, user behavior changes). A model trained on 2022 data may degrade silently in 2024.
- **Fix:** Monitor input feature distributions in production using tools like Evidently AI, WhyLabs, or custom statistical tests. Retrain on a regular schedule or when drift is detected.

### 3. **Leaking Future Information into Training Data**
- Using features in training that wouldn't be available at prediction time (e.g., using "total annual spend" to predict a mid-year churn event).
- **Fix:** Carefully audit the temporal relationships in your features. Apply strict cutoff dates to training data.

### 4. **Not Versioning Models**
- Pushing a new model to production without tracking which version is live, making debugging and rollback impossible.
- **Fix:** Use MLflow, DVC, or Weights & Biases to version every model artifact, hyperparameters, and training dataset.

### 5. **No Fallback / Rollback Plan**
- Deploying a model without any strategy for when it underperforms.
- **Fix:** Keep the previous model version live as a fallback. Use A/B testing or canary deployments to validate new models before full rollout.

### 6. **Misalignment Between Model Metric and Business Metric**
- Optimizing for accuracy while the business cares about precision (e.g., false positives are costly).
- **Fix:** Align model evaluation metrics with the actual business cost function from the start. In classification, consider whether F1, precision, recall, or AUC is the right metric.

### 7. **Assuming Static Class Distributions**
- Training on a balanced dataset but deploying in a highly imbalanced real world (e.g., fraud is 0.1% of transactions, not 50%).
- **Fix:** Adjust decision thresholds, use class weights, and test with production-realistic data distributions.

---

## Q288. (Section 2 - Linear Regression) What common mistakes occur when applying this technique in production?

### 1. **Violating Linear Regression Assumptions Without Checking**
- Deploying a linear regression without verifying its core assumptions:
  - Linearity (relationship is actually linear)
  - Homoscedasticity (constant variance of errors)
  - Independence of errors
  - Normality of residuals
- **Fix:** Plot residuals vs. fitted values, run Durbin-Watson tests, and check Q-Q plots during model validation.

### 2. **Not Scaling Features**
- Linear regression with features on very different scales (e.g., income in thousands vs. age in years) leads to numerically unstable coefficient estimates.
- **Fix:** Apply `StandardScaler` or `MinMaxScaler` and include the scaler in the deployment pipeline.

### 3. **Multicollinearity in Production Features**
- Two or more input features that are highly correlated (e.g., "income" and "monthly spending") inflate coefficient variance and make the model unstable when feature distributions shift slightly.
- **Fix:** Check Variance Inflation Factor (VIF) during training. Drop or combine correlated features.

### 4. **Extrapolating Beyond Training Data Range**
- Linear regression will blindly extrapolate — if trained on house prices from $100K–$500K, it will confidently (and wrongly) predict for $2M homes.
- **Fix:** Add input validation in your production API to reject predictions for inputs outside the training range. Log and flag out-of-range requests.

### 5. **Forgetting Outlier Sensitivity**
- OLS linear regression is sensitive to outliers. A single bad data point in a live stream can skew predictions significantly.
- **Fix:** Implement input validation and anomaly detection on incoming data. Consider robust regression alternatives (Huber loss) for noisy environments.

### 6. **Not Monitoring Prediction Distributions**
- Silent degradation: the model still runs but predictions drift from ground truth over time.
- **Fix:** Track the distribution of predicted values and residuals in production dashboards. Alert when they deviate beyond thresholds.

### 7. **Ignoring Feature Engineering Drift**
- A derived feature (e.g., "days since last purchase") calculated at training time may be computed differently in the production ETL pipeline.
- **Fix:** Unit-test every feature engineering step and ensure identical computation logic in both training and serving pipelines.

---

## Q289. (Section 3 - Ridge and Lasso Regression) What common mistakes occur when applying this technique in production?

### 1. **Not Persisting the Tuned Alpha Value**
- Finding the optimal regularization strength (alpha) via cross-validation during experimentation but hardcoding a different value in production.
- **Fix:** Log the alpha value in your experiment tracker (MLflow, W&B) and automate its injection into the production config.

### 2. **Forgetting to Scale Features Before Regularization**
- Ridge and Lasso penalize large coefficients. If features are on different scales, the penalty is applied unfairly — large-scale features get disproportionately penalized.
- **Fix:** **Always** apply feature scaling (e.g., `StandardScaler`) before Ridge/Lasso. Include it in the `Pipeline` object.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('model', Ridge(alpha=1.0))
])
```

### 3. **Re-tuning Alpha Without Fresh Data**
- Re-running `GridSearchCV` for alpha on stale data and getting a different optimal value — then deploying that without re-validating the full pipeline.
- **Fix:** Treat alpha tuning as part of the full retraining workflow. Always retune on the most recent training data.

### 4. **Lasso Dropping Important Features Silently**
- Lasso can zero out coefficients, effectively removing features. In production, this is fine — unless the zeroed features later become important (due to data drift) and the model never learns from them.
- **Fix:** Monitor feature importance over time. Trigger model retraining when new feature patterns emerge.

### 5. **Applying Ridge When Lasso Is Needed (or Vice Versa)**
- Ridge retains all features (shrinks coefficients). Lasso drops features. Using Ridge when you need feature selection leads to a more complex, less interpretable model than necessary.
- **Fix:** Use cross-validated comparison (or ElasticNet) to select the right regularizer for your problem.

### 6. **Not Validating on Held-Out Test Set After Cross-Validation**
- Cross-validation tunes alpha well but can still overfit to the training distribution. Reporting CV score as final performance is optimistic.
- **Fix:** Always have a completely untouched test set that is never used during model selection — only for final evaluation.

---

## Q290. (Section 4 - Logistic Regression) What common mistakes occur when applying this technique in production?

### 1. **Using Default 0.5 Threshold for All Cases**
- The default decision threshold of 0.5 is almost never optimal in real business scenarios, especially with imbalanced classes.
- **Fix:** Tune the classification threshold using Precision-Recall curves based on the business cost of false positives vs. false negatives.

```python
from sklearn.metrics import precision_recall_curve
precision, recall, thresholds = precision_recall_curve(y_true, y_prob)
# Choose threshold that meets business precision/recall requirements
```

### 2. **Assuming Features Are Linearly Separable**
- Logistic regression assumes a linear decision boundary. In complex real-world problems, this assumption fails, leading to poor accuracy.
- **Fix:** Check model performance on validation data. If it underperforms, add polynomial features, interaction terms, or switch to a more flexible model.

### 3. **Not Handling Class Imbalance**
- Training on imbalanced data (e.g., 99% non-fraud, 1% fraud) causes the model to predict the majority class for almost everything.
- **Fix:** Use `class_weight='balanced'`, SMOTE oversampling, or adjust prediction threshold.

### 4. **Multicollinearity Among Input Features**
- Highly correlated features cause unstable and uninterpretable coefficient estimates.
- **Fix:** Check correlation matrix and VIF. Remove or combine correlated features.

### 5. **Not Calibrating Probabilities**
- The probability scores from logistic regression may be poorly calibrated — a 70% predicted probability may not actually correspond to 70% real-world occurrence rate.
- **Fix:** Apply `CalibratedClassifierCV` with isotonic or Platt scaling, especially when probability scores are used in downstream business decisions.

### 6. **Ignoring Concept Drift**
- The relationship between features and the target can change (e.g., what predicts churn in 2022 may differ in 2024 due to market changes).
- **Fix:** Monitor model performance metrics (AUC, precision, recall) continuously in production. Set up automated alerts and retraining triggers.

### 7. **Not Logging Prediction Confidence Scores**
- Deploying a logistic regression that outputs only hard labels (0/1) rather than probability scores, discarding valuable uncertainty information.
- **Fix:** Always log and store predicted probabilities. They enable A/B test analysis, model monitoring, and threshold tuning post-deployment.

---

## Q291. (Section 5 - Regression Practical Implementation) What common mistakes occur when applying this technique in production?

### 1. **Reproducing Feature Engineering Differently in Production**
- The most common practical failure: features are engineered differently in the training notebook vs. the production ETL/API.
- **Fix:** Centralize feature engineering logic in a shared module or feature store. Unit-test it rigorously.

### 2. **Not Handling Missing Values in Live Data**
- Training was done on a cleaned dataset. Production data arrives with nulls, which the model was never designed to handle.
- **Fix:** Include imputation as part of the deployed `Pipeline`. Log instances of missing data and alert if missingness rate increases significantly.

### 3. **Not Saving the Full Pipeline (Only the Model)**
- Saving only the trained model object (`model.pkl`) without the preprocessing steps — then having to manually reconstruct them in production.
- **Fix:** Save the complete `sklearn.pipeline.Pipeline` object. This ensures identical preprocessing at serving time.

### 4. **Not Setting a Random Seed**
- Running the same training script produces slightly different models each time, making results non-reproducible and debugging difficult.
- **Fix:** Set `random_state` in all stochastic components. Log the random seed as part of experiment metadata.

### 5. **Overly Optimistic Evaluation (Data Leakage)**
- Including data from the future or from the test set in any step of preprocessing (e.g., fitting a scaler on the full dataset before splitting).
- **Fix:** Always split train/test **first**, then fit all preprocessing only on training data and transform test/production data.

### 6. **Not Testing Model Inference Latency**
- A model that runs fine offline may be too slow for a real-time API with SLA requirements.
- **Fix:** Benchmark inference time during development. For low-latency needs, consider model compression, simpler models, or pre-computation of features.

### 7. **Hard-coding File Paths or Credentials**
- Training scripts reference absolute local paths or embedded credentials that break in CI/CD and production environments.
- **Fix:** Use environment variables and configuration files. Never hard-code paths or secrets.

---

## Q292. (Section 6 - Ridge and Lasso Practical Implementation) What common mistakes occur when applying this technique in production?

### 1. **Not Automating Alpha Re-tuning on Retraining**
- Initial alpha was tuned carefully. When the model is retrained months later on new data, the alpha is not re-tuned — it's copy-pasted from the original run.
- **Fix:** Make `GridSearchCV` or `RidgeCV`/`LassoCV` a standard step in your automated retraining pipeline.

```python
from sklearn.linear_model import RidgeCV
model = RidgeCV(alphas=[0.01, 0.1, 1.0, 10.0], cv=5)
model.fit(X_train, y_train)
print(f"Best alpha: {model.alpha_}")
```

### 2. **Mixing Scaled and Unscaled Data in the Pipeline**
- Fit the scaler on training data, but accidentally transform new production data with fresh scaler parameters (re-fitting on production data).
- **Fix:** Fit the scaler **once** during training, pickle it alongside the model, and use only `transform()` (never `fit_transform()`) on production data.

### 3. **Not Logging Which Features Lasso Zeroed Out**
- Lasso may eliminate features. If this isn't logged, the production pipeline may still compute (and pay the cost of) those features unnecessarily.
- **Fix:** Log `model.coef_` after training to identify zeroed-out features. Optionally remove them from the data pipeline to save compute costs.

### 4. **Using Cross-Validation Score as Final Test Score**
- Reporting the CV score as model performance on unseen data, leading to overconfident stakeholder expectations.
- **Fix:** Always evaluate the final model on a completely held-out test set that was never used during model selection or training.

### 5. **Not Monitoring Coefficient Stability Over Time**
- As data distributions shift, the model coefficients change significantly on retraining — an early warning sign of concept drift that is often ignored.
- **Fix:** Log and track model coefficients across retraining runs. Alert if they change dramatically between versions.

### 6. **Deploying Without Baseline Comparison**
- The regularized model is deployed without comparing it to the baseline (e.g., simple linear regression or business rules). There's no way to quantify the value it adds.
- **Fix:** Always establish a clearly defined baseline model and compare both offline metrics and business KPIs between baseline and new model.

---

## Q293. (Section 7 - Naive Bayes) What common mistakes occur when applying this technique in production?

### 1. **Zero Probability Problem (Missing Smoothing)**
- If a word/feature appears in the test data but never appeared in training, the likelihood becomes zero, crashing the entire probability calculation.
- **Fix:** Always apply Laplace (additive) smoothing. In scikit-learn, this is the `alpha` parameter in `MultinomialNB` (default = 1.0, which is Laplace smoothing). Never set it to 0.

```python
from sklearn.naive_bayes import MultinomialNB
model = MultinomialNB(alpha=1.0)  # Laplace smoothing — keep this!
```

### 2. **Violating the Independence Assumption Silently**
- Naive Bayes assumes all features are independent. In practice, features are often correlated (e.g., word co-occurrences in text). The model still runs but may produce poorly calibrated probabilities.
- **Fix:** Be aware of this limitation. If probability calibration matters (not just ranking), apply `CalibratedClassifierCV`.

### 3. **Feeding Negative Values to MultinomialNB**
- `MultinomialNB` requires non-negative count data. Passing TF-IDF scores (which can be non-negative but float) or raw negative values causes errors or silently wrong results.
- **Fix:** Use `GaussianNB` for continuous features, `MultinomialNB` for count/frequency data, and `BernoulliNB` for binary features.

### 4. **Not Updating the Model on New Vocabulary**
- A text classification model trained on last year's data may never have seen new product names, slang, or terminology that appears in current data — leading to silent degradation.
- **Fix:** Implement periodic retraining and track out-of-vocabulary (OOV) token rates in production.

### 5. **Trusting Overconfident Probability Outputs**
- Naive Bayes is known to produce extreme probabilities (very close to 0 or 1) due to the independence assumption. Using these raw probabilities for business decisions can be misleading.
- **Fix:** Calibrate probabilities with Platt scaling or isotonic regression before using them in decision logic.

### 6. **Ignoring Data Imbalance**
- Training on imbalanced classes without adjusting priors leads the model to be systematically biased toward the majority class.
- **Fix:** Adjust class priors using `class_prior` parameter or balance the training data.

---

## Q294. (Section 8 - KNN) What common mistakes occur when applying this technique in production?

### 1. **Storing the Entire Training Set in Production Memory**
- KNN is a lazy learner — it stores all training data and computes distances at prediction time. With millions of training samples, this is a memory and latency disaster in production.
- **Fix:** Use approximate nearest neighbor (ANN) libraries like **FAISS**, **Annoy**, or **ScaNN** for large-scale deployment. Or choose a model that learns a compact representation.

### 2. **Not Scaling Features**
- KNN relies on distance calculations. Without scaling, features with large numerical ranges (e.g., income: 50,000) dominate over small-scale features (e.g., age: 35), making the distance measure meaningless.
- **Fix:** **Always** apply `StandardScaler` or `MinMaxScaler` before KNN. Include it in the production pipeline.

### 3. **Choosing K Without Cross-Validation**
- Using K=5 by default without tuning it to the actual dataset characteristics, leading to underfitting (large K) or overfitting (small K).
- **Fix:** Use `GridSearchCV` or `cross_val_score` to find the optimal K on your specific dataset.

### 4. **High Prediction Latency in Real-Time Systems**
- Even with scaled data, KNN's O(n) search time per prediction makes it too slow for real-time APIs with high traffic.
- **Fix:** Pre-index the training data using KD-trees (scikit-learn's default) or ball-trees. For very high traffic, switch to a model with constant-time inference (e.g., Random Forest).

### 5. **Curse of Dimensionality**
- KNN degrades sharply as the number of features increases — in high-dimensional space, all points become equally distant, making nearest-neighbor search meaningless.
- **Fix:** Apply dimensionality reduction (PCA, t-SNE, UMAP) before using KNN. Limit features to the most informative ones.

### 6. **Not Handling New/Unseen Feature Values**
- If a new category appears in production that wasn't in training, the encoded feature vector will be wrong.
- **Fix:** Add robust encoding (with unknown-category handling) and input validation at the API layer.

### 7. **No Model Artifact to Deploy**
- Since KNN stores training data rather than learning a compact model, teams sometimes forget that they need to version and deploy the **entire training dataset** as the model artifact.
- **Fix:** Package the fitted `KNeighborsClassifier` (which stores the training data internally) as a pickle. Treat it like any other model artifact.

---

## Q295. (Section 9 - Decision Tree Classification) What common mistakes occur when applying this technique in production?

### 1. **Deploying an Overfitted, Unpruned Tree**
- Without depth limits, decision trees grow extremely deep and memorize training data. They look perfect in training but fail completely on new data.
- **Fix:** Always set `max_depth`, `min_samples_split`, and `min_samples_leaf`. Tune these via cross-validation.

```python
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier(max_depth=5, min_samples_leaf=20, random_state=42)
```

### 2. **Not Monitoring for Feature Distribution Shifts**
- Decision trees create hard-coded splits (e.g., "if age > 35"). If the age distribution of incoming users shifts significantly, the tree's splits become incorrect without retraining.
- **Fix:** Monitor input feature distributions monthly. Retrain when splits become stale.

### 3. **Treating the Tree Structure as Permanent**
- Business logic teams sometimes hard-code the decision tree's rules into manual workflows. When the model is retrained, these hard-coded rules become outdated.
- **Fix:** Always serve predictions through the model API — never manually extract and hard-code the tree's rules.

### 4. **Ignoring Class Imbalance**
- An imbalanced dataset causes the tree to default to always predicting the majority class for leaf nodes.
- **Fix:** Use `class_weight='balanced'` and evaluate with F1/AUC rather than raw accuracy.

### 5. **Over-relying on Training Accuracy**
- Decision trees can reach 100% training accuracy by overfitting. Teams sometimes mistake this for a good model.
- **Fix:** Always evaluate on a held-out test set. Use cross-validation. A good model has similar training and test performance.

### 6. **Not Versioning the Tree Structure**
- After retraining, the new tree may have completely different splits even on the same data due to randomness in split selection. Not version-controlling makes debugging hard.
- **Fix:** Log model artifacts, feature importances, and tree structure for every training run.

### 7. **Using Default Impurity Measure Without Consideration**
- The default `gini` impurity is fine for most cases, but for highly imbalanced problems or specific business objectives, `entropy` or custom split criteria may be better.
- **Fix:** Compare Gini vs. entropy experimentally and choose based on validation performance.

---

## Q296. (Section 10 - Decision Tree Regression) What common mistakes occur when applying this technique in production?

### 1. **Predicting Out-of-Range Values Incorrectly (Extrapolation Failure)**
- Decision tree regression cannot extrapolate beyond the range of training target values. It will predict the average of the nearest leaf — which may be far from correct for values outside the training range.
- **Fix:** Add hard input validation in the production API to detect out-of-range requests. Log and flag them. Consider augmenting with a linear model for extrapolation.

### 2. **Overfitting Due to No Depth Control**
- Deep trees memorize training noise, producing high-variance predictions on new data.
- **Fix:** Tune `max_depth`, `min_samples_leaf`, and `ccp_alpha` (cost-complexity pruning) via cross-validation.

### 3. **High Prediction Variance on Boundary Inputs**
- For regression problems, small changes in input values can cause large jumps in predictions at tree decision boundaries.
- **Fix:** If smooth predictions are required, consider ensemble methods (Random Forest, Gradient Boosting) which average many trees and produce smoother prediction surfaces.

### 4. **Not Accounting for Target Variable Distribution**
- If the target variable (e.g., house prices) is heavily skewed, the tree will struggle because it predicts mean values per leaf.
- **Fix:** Apply log transformation to the target, train on log-scale, and reverse the transformation at prediction time.

### 5. **Feature Importance Misinterpretation**
- Decision tree feature importances measure "how often a feature was used in splits" — not true causal importance. In production, teams sometimes use this to make business decisions that are incorrect.
- **Fix:** Use SHAP values for more reliable feature attribution. Cross-validate feature importances across multiple models.

### 6. **Not Handling New Categories in Categorical Features**
- If a new category appears in a categorical feature in production that wasn't seen during training, the model pipeline may crash or produce garbage output.
- **Fix:** Implement robust encoding with explicit handling for unseen categories (e.g., map to a default value or "other" category).

---

## Q297. (Section 11 - Ensemble Learning, Bagging and Boosting) What common mistakes occur when applying this technique in production?

### 1. **Not Accounting for Increased Inference Latency**
- Ensemble models (especially with 500+ estimators) are much slower to serve than a single model. Teams often benchmark training time but forget prediction latency.
- **Fix:** Profile inference time during development. Consider reducing `n_estimators` if latency is a constraint. Use parallel prediction (`n_jobs=-1`) where possible.

### 2. **Memory Bloat in Production**
- A bagging ensemble with 100 large base models can easily consume gigabytes of RAM, causing issues in memory-constrained production environments.
- **Fix:** Profile model size before deployment. Use `compress=9` when saving with joblib. Consider model distillation.

### 3. **Boosting Models Sensitive to Noisy Labels**
- Boosting focuses on misclassified samples — if those misclassifications are due to noisy/incorrect labels, boosting will overfit to the noise.
- **Fix:** Clean training data carefully before boosting. Use early stopping to prevent over-amplification of noise.

### 4. **Forgetting Early Stopping in Boosting**
- Running too many boosting rounds leads to overfitting in production. Without early stopping, the model may have been perfectly tuned on training data but degrades on new data.
- **Fix:** Always use validation-based early stopping and log the optimal number of rounds.

### 5. **Not Monitoring Individual Model Diversity Over Time**
- As data drifts, some base models in the ensemble may degrade more than others. Without monitoring, the ensemble degrades silently.
- **Fix:** If possible, track the contribution and disagreement rate of individual ensemble members over time.

### 6. **Deploying Without Comparing to Single-Model Baseline**
- Ensemble models are more complex and harder to maintain. If they don't significantly outperform a simpler model, the added complexity isn't worth it.
- **Fix:** Always document the performance gain vs. the complexity cost. Justify ensemble use with clear metrics.

---

## Q298. (Section 12 - Random Forest) What common mistakes occur when applying this technique in production?

### 1. **Not Tuning n_estimators and max_features**
- Using default values (`n_estimators=100`, `max_features='sqrt'`) without validation. Too few trees → high variance. Default `max_features` may not be optimal.
- **Fix:** Use `RandomizedSearchCV` to tune key hyperparameters: `n_estimators`, `max_depth`, `max_features`, `min_samples_leaf`.

### 2. **Model File Too Large for Deployment**
- A Random Forest with 500 deep trees can easily exceed 1–2 GB as a pickle file, making it impractical for low-resource deployment environments.
- **Fix:** Reduce `max_depth`, reduce `n_estimators`, or use `joblib.dump(model, path, compress=3)`. Evaluate if XGBoost's more compact format is preferable.

### 3. **Misusing Feature Importances for Business Decisions**
- Random Forest's impurity-based feature importances are biased toward high-cardinality features (e.g., user IDs, postal codes). Teams sometimes act on these misleading importances.
- **Fix:** Use permutation importance or SHAP values instead of the built-in `feature_importances_`.

```python
from sklearn.inspection import permutation_importance
result = permutation_importance(model, X_test, y_test, n_repeats=10)
```

### 4. **Not Handling Class Imbalance**
- Random Forest's default behavior gives equal weight to all samples. On imbalanced datasets, it becomes biased toward the majority class.
- **Fix:** Use `class_weight='balanced'` or `class_weight='balanced_subsample'`. Evaluate with AUC-ROC and F1.

### 5. **Slow Retraining Pipeline**
- Retraining a large Random Forest on millions of samples can take hours. If not planned, this blocks the retraining cadence needed to combat data drift.
- **Fix:** Profile retraining time. Consider incremental learning strategies, data sampling for fast retraining experiments, and efficient compute (parallel cores, distributed training).

### 6. **Not Setting random_state**
- Without a fixed random seed, two identical training runs produce different models — making debugging, comparison, and reproducibility impossible.
- **Fix:** Always set `random_state` in the classifier and in train/test splits.

### 7. **Treating Random Forest as a Black Box**
- Deploying without any explainability layer makes it impossible to audit in regulated industries or debug individual predictions.
- **Fix:** Integrate SHAP for local and global explainability. Log SHAP values for sampled predictions in production.

---

## Q299. (Section 13 - AdaBoost and Gradient Boosting) What common mistakes occur when applying this technique in production?

### 1. **Not Using Early Stopping in Gradient Boosting**
- Gradient Boosting can have thousands of rounds. Without early stopping, the model overfits, performs poorly in production, and wastes compute.
- **Fix:** Always monitor a validation set and stop training when validation loss stops improving.

```python
from sklearn.ensemble import GradientBoostingClassifier
model = GradientBoostingClassifier(n_estimators=500, validation_fraction=0.1,
                                    n_iter_no_change=10, random_state=42)
```

### 2. **AdaBoost Collapsing on Noisy Labels**
- AdaBoost aggressively upweights misclassified samples. If those samples are mislabeled, it amplifies the noise rather than the signal.
- **Fix:** Validate data quality before training. Consider Gradient Boosting (which is more robust to noise) over AdaBoost in noisy environments.

### 3. **Not Tuning Learning Rate in Conjunction with n_estimators**
- Using a high learning rate with many estimators leads to overfitting. Lowering learning rate requires more estimators — these must be tuned together.
- **Fix:** Use `learning_rate` × `n_estimators` as a joint hyperparameter. Lower learning rate generally yields better generalization if compute allows.

### 4. **Gradient Boosting Is Sequential — High Prediction Latency**
- Unlike Random Forest, trees in gradient boosting are built sequentially, and all must be traversed at prediction time. With 1000 trees, this can be slow.
- **Fix:** Reduce `n_estimators` via early stopping. Use histogram-based implementations (HistGradientBoosting, LightGBM, XGBoost) which are faster.

### 5. **Not Monitoring for Concept Drift**
- Gradient Boosting models encode the patterns of training data into many tree splits. As the world changes, these splits become outdated — but the model silently continues predicting.
- **Fix:** Monitor key performance metrics (AUC, F1, RMSE) in production dashboards. Set automated alerts for metric degradation.

### 6. **Assuming Gradient Boosting Always Wins**
- Teams sometimes default to Gradient Boosting for every problem even when a simpler model (logistic regression, Ridge) would suffice and be much easier to maintain.
- **Fix:** Always compare against a baseline. Reserve ensemble methods for problems where the accuracy gain justifies the complexity.

### 7. **Failing to Serialize the Model with Consistent Library Versions**
- A model saved with scikit-learn 1.1 may not load correctly with scikit-learn 1.3 due to API changes.
- **Fix:** Pin library versions in `requirements.txt`. Test loading the model artifact in a clean environment as part of CI/CD.

---

## Q300. (Section 14 - XGBoost Classification) What common mistakes occur when applying this technique in production?

### 1. **Not Using Early Stopping**
- Training XGBoost for a fixed number of rounds without monitoring a validation set leads to overfitting and unnecessarily large models.
- **Fix:** Always supply an `eval_set` and use `early_stopping_rounds`.

```python
model = xgb.XGBClassifier(n_estimators=1000, learning_rate=0.05,
                            early_stopping_rounds=50, eval_metric='logloss')
model.fit(X_train, y_train, eval_set=[(X_val, y_val)], verbose=False)
print(f"Best iteration: {model.best_iteration}")
```

### 2. **Not Handling Class Imbalance with scale_pos_weight**
- XGBoost on imbalanced binary classification data predicts the majority class by default.
- **Fix:** Set `scale_pos_weight = count(negative) / count(positive)` to rebalance.

```python
scale = (y_train == 0).sum() / (y_train == 1).sum()
model = xgb.XGBClassifier(scale_pos_weight=scale)
```

### 3. **Training/Serving Feature Mismatch**
- XGBoost is strict about feature names and order. If the production feature set differs in any way from training, predictions will be silently wrong or throw errors.
- **Fix:** Enforce feature ordering via a fixed schema. Validate feature names and dtypes at the API boundary.

### 4. **Not Pinning XGBoost Version**
- XGBoost serialization format changes across major versions. A model saved in v1.6 may not load in v2.0.
- **Fix:** Pin `xgboost==x.y.z` in `requirements.txt`. Test model loading across environments as part of CI/CD.

### 5. **Using Default Hyperparameters on Complex Problems**
- XGBoost's defaults are reasonable starting points, but on complex business problems, leaving `max_depth=6`, `learning_rate=0.3` untuned often leaves significant performance on the table.
- **Fix:** Use `RandomizedSearchCV` or Optuna/Hyperopt for Bayesian hyperparameter optimization.

```python
import optuna
def objective(trial):
    params = {
        'max_depth': trial.suggest_int('max_depth', 3, 10),
        'learning_rate': trial.suggest_float('learning_rate', 0.01, 0.3),
        'subsample': trial.suggest_float('subsample', 0.6, 1.0),
        'colsample_bytree': trial.suggest_float('colsample_bytree', 0.6, 1.0),
    }
    # ... cross-validate and return score
```

### 6. **Ignoring Prediction Threshold**
- Using the default 0.5 threshold for classification when the business has asymmetric misclassification costs (e.g., missing a fraud case is 10x more costly than a false alarm).
- **Fix:** Tune the threshold on a validation set using Precision-Recall curves aligned to business costs.

### 7. **Not Monitoring Model Performance Post-Deployment**
- XGBoost models can silently degrade as input data distributions shift. Without monitoring, teams discover degradation only when business metrics suffer.
- **Fix:** Log prediction distributions, input feature statistics, and classification metrics daily. Use tools like Evidently AI, Arize, or Grafana-based dashboards. Set automated retraining triggers.

### 8. **Treating Feature Importances as Ground Truth**
- XGBoost's built-in feature importances (`weight`, `gain`, `cover`) can be inconsistent and misleading — especially for correlated features.
- **Fix:** Use SHAP values for reliable, consistent feature attribution.

```python
import shap
explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_test)
shap.summary_plot(shap_values, X_test)
```
