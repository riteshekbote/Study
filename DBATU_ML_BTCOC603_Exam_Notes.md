# DBATU Machine Learning (BTCOC603) — Exam-Ready Notes

---

# IMPORTANT NUMERICALS

## 1. Confusion Matrix Numerical

Suppose a model predicts for 100 patients whether they have a disease:
TP = 40, TN = 30, FP = 10, FN = 20

**Calculations:**
- Accuracy = (TP+TN)/(TP+TN+FP+FN) = (40+30)/100 = **70%**
- Precision = TP/(TP+FP) = 40/(40+10) = **80%**
- Recall = TP/(TP+FN) = 40/(40+20) = **66.7%**
- Specificity = TN/(TN+FP) = 30/(30+10) = **75%**
- F1-Score = 2×(Precision×Recall)/(Precision+Recall) = 2×(0.80×0.667)/(0.80+0.667) = **72.7%**

---

## 2. Information Gain (Decision Tree — ID3) Numerical

Dataset "Play Tennis": Total = 14 examples, 9 = Yes, 5 = No

**Step 1 — Entropy of full dataset:**
Entropy(S) = −(9/14)log₂(9/14) − (5/14)log₂(5/14) = **0.940**

**Step 2 — Split on attribute "Outlook":**

| Outlook | Total | Yes | No | Entropy |
|---|---|---|---|---|
| Sunny | 5 | 2 | 3 | 0.971 |
| Overcast | 4 | 4 | 0 | 0 |
| Rainy | 5 | 3 | 2 | 0.971 |

**Step 3 — Weighted Entropy after split:**
= (5/14)(0.971) + (4/14)(0) + (5/14)(0.971) = **0.693**

**Step 4 — Information Gain:**
IG(Outlook) = Entropy(S) − Weighted Entropy = 0.940 − 0.693 = **0.247**

This process is repeated for all other attributes (Temperature, Humidity, Wind). The attribute with the **highest Information Gain** is selected as the root node.

---

## 3. K-Means Clustering Numerical

Points: A(2,2), B(2,4), C(6,6), D(6,4), E(1,3), F(7,5)
K = 2. Initial centroids chosen: C1 = A(2,2), C2 = D(6,4)

**Iteration 1 — compute Euclidean distance of each point to C1 and C2:**

| Point | Dist to C1 | Dist to C2 | Assigned Cluster |
|---|---|---|---|
| A(2,2) | 0 | 4.47 | Cluster 1 |
| B(2,4) | 2.00 | 4.00 | Cluster 1 |
| C(6,6) | 5.66 | 2.00 | Cluster 2 |
| D(6,4) | 4.47 | 0 | Cluster 2 |
| E(1,3) | 1.41 | 5.10 | Cluster 1 |
| F(7,5) | 5.83 | 1.41 | Cluster 2 |

Cluster 1 = {A, B, E} → New Centroid C1 = ((2+2+1)/3, (2+4+3)/3) = **(1.67, 3.00)**
Cluster 2 = {C, D, F} → New Centroid C2 = ((6+6+7)/3, (6+4+5)/3) = **(6.33, 5.00)**

**Iteration 2 — recompute distances using new centroids:**

| Point | Dist to C1 | Dist to C2 | Assigned Cluster |
|---|---|---|---|
| A(2,2) | 1.05 | 5.27 | Cluster 1 |
| B(2,4) | 1.05 | 4.44 | Cluster 1 |
| C(6,6) | 5.27 | 1.05 | Cluster 2 |
| D(6,4) | 4.44 | 1.05 | Cluster 2 |
| E(1,3) | 0.67 | 5.69 | Cluster 1 |
| F(7,5) | 5.69 | 0.67 | Cluster 2 |

Clusters remain the same as Iteration 1 → **centroids are stable → algorithm converges.**

**Final Result:**
- Cluster 1 = {A, B, E}, Centroid = (1.67, 3.00)
- Cluster 2 = {C, D, F}, Centroid = (6.33, 5.00)

---

## 4. KNN (K-Nearest Neighbour) Numerical

Training data:

| Point | X1 | X2 | Class |
|---|---|---|---|
| P1 | 1 | 2 | A |
| P2 | 2 | 3 | A |
| P3 | 3 | 3 | B |
| P4 | 6 | 5 | B |
| P5 | 7 | 8 | B |

Test point Q = (3, 4). Take **K = 3**.

**Step 1 — Compute Euclidean distance from Q to each training point:**
- d(Q,P1) = √((3−1)²+(4−2)²) = √8 = **2.83**
- d(Q,P2) = √((3−2)²+(4−3)²) = √2 = **1.41**
- d(Q,P3) = √((3−3)²+(4−3)²) = √1 = **1.00**
- d(Q,P4) = √((3−6)²+(4−5)²) = √10 = **3.16**
- d(Q,P5) = √((3−7)²+(4−8)²) = √32 = **5.66**

**Step 2 — Sort distances (ascending) and pick K=3 nearest neighbours:**
1. P3 (1.00) → Class B
2. P2 (1.41) → Class A
3. P1 (2.83) → Class A

**Step 3 — Majority Voting:**
Class A = 2 votes, Class B = 1 vote → **Predicted Class = A**

---
---

# UNIT 1 — Basics of Machine Learning

## Types of Machine Learning
- **Supervised Learning:** Trained on labeled data (input–output pairs known). Learns a mapping function from input (X) to output (Y). Sub-types: Classification (categorical output), Regression (continuous output). Examples: Linear Regression, Logistic Regression, Decision Tree, SVM, Naïve Bayes.
- **Unsupervised Learning:** Trained on unlabeled data; finds hidden patterns/structure. Sub-types: Clustering (K-Means), Association Rule Mining. No predefined output.
- **Reinforcement Learning:** An agent interacts with an environment, takes actions, and learns via rewards/penalties to maximize cumulative reward over time. Example: Game-playing AI, robotics.

## Applications of Machine Learning
Healthcare (disease diagnosis), Finance (fraud detection, credit scoring), E-commerce (recommendation systems), NLP (chatbots, speech recognition), Computer Vision (face recognition, self-driving cars), Marketing (customer segmentation).

## Machine Learning Process
1. Data Collection
2. Data Preprocessing (cleaning, handling missing values, normalization)
3. Splitting dataset (Train/Test)
4. Model Selection
5. Training the Model
6. Evaluation
7. Hyperparameter Tuning
8. Deployment

## Confusion Matrix

|  | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actual Positive** | True Positive (TP) | False Negative (FN) |
| **Actual Negative** | False Positive (FP) | True Negative (TN) |

- **TP:** Correctly predicted positive.
- **TN:** Correctly predicted negative.
- **FP:** Incorrectly predicted positive (Type I Error).
- **FN:** Incorrectly predicted negative (Type II Error).

## Performance Evaluation Metrics
- **Accuracy** = (TP+TN) / (TP+TN+FP+FN) — overall correctness.
- **Precision** = TP / (TP+FP) — how many predicted positives were actually positive; important when FP cost is high.
- **Recall (Sensitivity)** = TP / (TP+FN) — how many actual positives were correctly found; important when FN cost is high.
- **Specificity** = TN / (TN+FP) — how many actual negatives were correctly identified.
- **F1-Score** = 2×(Precision×Recall)/(Precision+Recall) — harmonic mean, balances Precision & Recall.

*(See Numerical section above for a worked example.)*

## Bias vs Variance
- **Bias:** Error from oversimplified assumptions; high bias → model fails to capture pattern → **Underfitting**. High bias, low variance.
- **Variance:** Error from sensitivity to small fluctuations/noise in training data; high variance → model memorizes noise → **Overfitting**. Low bias, high variance.
- **Tradeoff:** Decreasing bias increases variance and vice versa. Goal: minimize Total Error = Bias² + Variance + Irreducible Error, for best generalization.

**Underfitting:** Model too simple; poor performance on both training and test data.
**Overfitting:** Model too complex; excellent on training data, poor on test data.

**Methods to reduce Overfitting:**
1. Cross-Validation
2. Regularization (L1/L2)
3. Pruning (in Decision Trees)
4. Increasing training data
5. Early Stopping
6. Dropout (Neural Networks)
7. Feature Selection
8. Ensemble Methods (Bagging/Boosting)

## Training / Validation / Test Set
- **Training Set:** Used to train/fit the model.
- **Validation Set:** Used during training to tune hyperparameters and check for overfitting.
- **Test Set:** Completely unseen data used only for final performance evaluation.
- Typical split: 60:20:20 or 70:15:15.

## Cross Validation (K-Fold)
1. Divide dataset into K equal folds.
2. Train on K−1 folds, test on the remaining 1 fold.
3. Repeat K times, each time with a different fold as test set.
4. Average the K results → final performance estimate.

**Advantages:** More reliable performance estimate, efficient use of limited data.
**Limitations:** Computationally expensive, not ideal for time-series data.

---
---

# UNIT 2 — Classification & Optimization

## Naïve Bayes Classifier
Probabilistic classifier based on **Bayes' Theorem**, assumes features are conditionally independent given the class (hence "naïve").

**Bayes' Theorem:** P(A|B) = [P(B|A) × P(A)] / P(B)

**Working:**
1. Calculate prior probability of each class.
2. Calculate likelihood of each feature given each class.
3. Compute posterior probability for each class using Bayes' theorem.
4. Assign the class with highest posterior probability.

**Types:** Gaussian NB (continuous data), Multinomial NB (text/count data), Bernoulli NB (binary data).

**Advantages:** Fast, simple, works well with high-dimensional data (e.g., text/spam classification), needs less training data.
**Limitations:** Independence assumption rarely holds; Zero Frequency Problem (solved by Laplace smoothing).

## Logistic Regression
Supervised algorithm for **binary classification** (despite the name "regression").

**Sigmoid Function:** σ(z) = 1/(1+e^(−z)), maps any real value into range (0,1). If σ(z) ≥ 0.5 → class 1, else class 0.

**Cost Function (Log Loss / Cross-Entropy):**
J(θ) = −(1/m) Σ [yᵢ·log(h(xᵢ)) + (1−yᵢ)·log(1−h(xᵢ))]
Used instead of MSE because MSE + sigmoid gives a non-convex cost function; Log Loss is convex, ensuring gradient descent converges properly.

**Assumptions:** Binary/categorical dependent variable, little multicollinearity, linear relationship between predictors and log-odds, large sample size, independent observations.

**Advantages:** Simple, interpretable, outputs probabilities, works well for linearly separable classes.
**Limitations:** Assumes linear decision boundary (log-odds), sensitive to outliers, poor with non-linearly separable data.

## Gradient Descent
Optimization algorithm to minimize cost function by iteratively updating parameters:
θ = θ − α × ∂J(θ)/∂θ

- **Batch Gradient Descent:** Uses entire dataset per update — accurate but slow.
- **Stochastic Gradient Descent (SGD):** Uses one random example per update — fast but noisy/zigzag path.
- **Mini-Batch Gradient Descent:** Uses small batches (e.g., 32/64 samples) — balance of speed and stability; most widely used.

## Regularization (L1 vs L2)
Adds a penalty term to the cost function to prevent overfitting by discouraging large weights.

- **L1 (Lasso):** J(θ) = MSE + λΣ|θᵢ| — can shrink weights to exactly zero → automatic feature selection → sparse model.
- **L2 (Ridge):** J(θ) = MSE + λΣθᵢ² — shrinks weights close to zero but never exactly zero → retains all features → dense model.

| Basis | L1 (Lasso) | L2 (Ridge) |
|---|---|---|
| Penalty | Sum of absolute weights | Sum of squared weights |
| Feature Selection | Yes | No |
| Outlier Robustness | More robust | Less robust |
| Model | Sparse | Dense |

---
---

# UNIT 3 — Neural Networks

## Perceptron
Simplest neural network — single neuron, used for binary classification of **linearly separable** data.

**Formula:** y = f(Σwᵢxᵢ + b)

**Working:** Compute weighted sum → apply activation (step function) → compare with actual output → update weights: wᵢ = wᵢ + α(y_actual − y_predicted)xᵢ → repeat until convergence.

**Advantages:** Simple, fast for linear problems.
**Limitations:** Cannot solve non-linear problems (e.g., XOR).

## Multilayer Perceptron (MLP) / ANN
Overcomes Perceptron's limitation using multiple layers:
- **Input Layer** — receives features
- **Hidden Layer(s)** — extract patterns via weights, bias, activation functions
- **Output Layer** — final prediction
Data flows forward only (feedforward network); solves non-linear problems.

## Backpropagation Algorithm
Supervised training algorithm for multilayer neural networks; minimizes error through iterative weight updates.

**Steps:**
1. **Forward Pass:** Input flows through layers, each neuron computes weighted sum + activation, produces output.
2. **Error Calculation:** Compare predicted vs actual output using a loss function (MSE/Cross-Entropy).
3. **Backward Pass:** Error is propagated backward using the chain rule to compute gradients w.r.t. each weight.
4. **Weight Update:** w = w − α × (∂E/∂w), repeated over many epochs until error is minimized.

**Advantages:** Efficiently trains deep networks.
**Limitations:** Can get stuck in local minima; needs large data & computation.

## Convolutional Neural Network (CNN)
Deep learning architecture for image data.

**Layers:**
1. Input Layer — raw image
2. Convolution Layer — filters extract features (edges, textures) → feature maps
3. ReLU Layer — adds non-linearity
4. Pooling Layer — down-samples, reduces computation (e.g., Max Pooling)
5. Flatten Layer — converts 2D feature maps to 1D vector
6. Fully Connected Layer — combines features
7. Output Layer — final class probabilities (Softmax)

**Applications:** Image classification, face recognition, object detection, medical imaging.

## Activation Functions

| Function | Range/Formula | Use Case |
|---|---|---|
| Sigmoid | 0 to 1 | Binary classification (output layer) |
| Tanh | −1 to +1 | Hidden layers, zero-centered |
| ReLU | f(x)=max(0,x) | Most common in hidden layers |
| Softmax | Probabilities summing to 1 | Multi-class classification (output layer) |

---
---

# UNIT 4 — Learning Theory & Ensemble Methods

## Support Vector Machine (SVM)
Finds the **optimal hyperplane** that separates classes with **maximum margin**.
- **Hyperplane:** decision boundary (w·x+b=0).
- **Margin:** distance between hyperplane and nearest points; SVM maximizes this.
- **Support Vectors:** data points closest to the hyperplane; define its position.
- **Kernel Trick:** maps non-linearly separable data into higher-dimensional space to make it linearly separable, without explicit computation. Common kernels: Linear, Polynomial, RBF/Gaussian, Sigmoid.

**Advantages:** Effective in high dimensions, memory efficient, versatile via kernels.
**Limitations:** Slow on large datasets, sensitive to noise/overlap, hard to tune kernel/parameters.

## Decision Tree (ID3 Algorithm)
Tree-structured model: Root Node, Internal Nodes (attribute tests), Branches (outcomes), Leaf Nodes (class labels).

**Entropy:** Entropy(S) = −Σpᵢlog₂(pᵢ) — measures impurity (0 = pure, 1 = max impure).

**Information Gain:** IG(S,A) = Entropy(S) − Σ[(|Sᵥ|/|S|)×Entropy(Sᵥ)] — reduction in entropy from splitting on attribute A.

**ID3 Steps:** Compute entropy of dataset → compute IG for each attribute → select attribute with highest IG as node → split → repeat recursively until pure nodes or no attributes left.

*(See Numerical section above for worked example.)*

**Overfitting in Decision Trees:** Deep trees memorize training data noise, causing poor generalization.

**Pruning:** Technique to reduce overfitting by removing branches that have little importance/predictive power.
- **Pre-pruning:** Stop tree growth early (e.g., max depth limit).
- **Post-pruning:** Grow full tree first, then remove weak branches afterward.

**Advantages:** Easy to interpret, handles numerical & categorical data, little preprocessing needed.
**Limitations:** Prone to overfitting, unstable (small data change → different tree), biased toward attributes with more levels.

## PAC (Probably Approximately Correct) Learning
Theoretical framework defining how much data is needed for an algorithm to be, with high probability, approximately correct.
- **ε (epsilon):** acceptable error rate.
- **δ (delta):** allowed probability of failure.
- **Confidence:** 1−δ.
A concept class is PAC-learnable if an algorithm can output a hypothesis with error ≤ ε with probability ≥ 1−δ using a polynomial number of samples.

## Ensemble Learning
Combines multiple base models to produce a more accurate, robust prediction than any single model. Types: Bagging, Boosting, Stacking.

## Bagging vs Boosting

**Bagging (Bootstrap Aggregating):** Models trained in **parallel** on random bootstrap samples; final result via majority vote/averaging. Reduces **variance**. Example: Random Forest.

**Boosting:** Models trained **sequentially**, each correcting previous errors by giving misclassified points higher weight; final result is a weighted combination. Reduces **bias**. Example: AdaBoost, Gradient Boosting, XGBoost.

| Basis | Bagging | Boosting |
|---|---|---|
| Training | Parallel, independent | Sequential, dependent |
| Goal | Reduce variance | Reduce bias |
| Sampling | Random with replacement | Weighted on prior errors |
| Example | Random Forest | AdaBoost |

## Random Forest
Ensemble (Bagging-based) algorithm building multiple Decision Trees on random data/feature subsets; final prediction via majority voting (classification) or averaging (regression).

**Steps:** Bootstrap sample the data → build a tree per sample (random feature subset per split) → combine all tree outputs via majority vote.

**Advantages:** High accuracy, reduces overfitting vs single tree, handles missing data, robust to noise.
**Limitations:** Less interpretable (black-box), computationally expensive, slower prediction.

---
---

# UNIT 5 — Clustering & Dimensionality Reduction

## K-Nearest Neighbour (KNN)
Instance-based (lazy learning) supervised algorithm. Classifies a new point based on the majority class among its **K nearest neighbours** (by distance, usually Euclidean).

**Steps:** Choose K → compute distance from query point to all training points → select K nearest → majority vote (classification) or average (regression).

**Advantages:** Simple, no training phase, effective for small datasets.
**Limitations:** Computationally expensive for large datasets, sensitive to irrelevant/unscaled features, choice of K matters, poor with imbalanced data.

*(See Numerical section above for worked example.)*

## K-Means Clustering
Unsupervised algorithm partitioning data into **K clusters**, where each point belongs to the cluster with the nearest mean (centroid).

**Steps:**
1. Choose number of clusters K.
2. Randomly initialize K centroids.
3. Assign each point to nearest centroid.
4. Recalculate centroids as mean of assigned points.
5. Repeat steps 3–4 until centroids stabilize (convergence).

**Advantages:** Simple, fast, scales well.
**Limitations:** Must specify K in advance, sensitive to initial centroids, struggles with non-spherical clusters/outliers.

*(See Numerical section above for worked example.)*

## Hierarchical Clustering
Builds a tree-like hierarchy of clusters (**dendrogram**), no need to predefine K.

- **Agglomerative (Bottom-Up):** Each point starts as its own cluster; closest clusters merge repeatedly until one cluster remains.
- **Divisive (Top-Down):** Starts with one cluster; splits repeatedly until each point is its own cluster.

**Dendrogram:** Tree diagram showing the sequence of merges/splits; cutting it at a chosen height gives the desired number of clusters.

**Advantages:** No need to predefine K, interpretable dendrogram.
**Limitations:** Computationally expensive for large data, sensitive to noise/outliers.

## Principal Component Analysis (PCA)
Dimensionality reduction technique transforming correlated features into fewer uncorrelated **Principal Components**, retaining maximum variance.

**Steps:**
1. Standardize the dataset.
2. Compute covariance matrix.
3. Calculate eigenvalues & eigenvectors.
4. Sort eigenvectors by eigenvalues (descending) — top ones are Principal Components.
5. Project data onto top-k components.

**Advantages:** Reduces computation, removes multicollinearity, aids visualization, reduces overfitting.
**Limitations:** Reduced interpretability, sensitive to feature scaling.

## Curse of Dimensionality
Problems arising from datasets with very high number of features:
- Data becomes sparse; distance metrics lose meaning.
- Slower training, higher memory usage.
- Increased overfitting risk.
**Solution:** Dimensionality Reduction (PCA / Feature Selection).

## Dimensionality Reduction
- **Feature Selection:** Choosing the most relevant original features, discarding irrelevant/redundant ones.
- **Feature Extraction:** Transforming original features into a new, smaller set capturing most variance (e.g., PCA, LDA).

---
---

*End of Notes — Good luck for the exam! Draw the suggested diagrams wherever mentioned; examiners award extra marks for correct diagrams.*
