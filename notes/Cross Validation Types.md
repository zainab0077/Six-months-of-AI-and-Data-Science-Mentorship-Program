

**Types of Cross-Validation (CV) Explained with Iris Dataset Examples**
====================================================================

Cross-Validation (CV) is a technique used to evaluate the performance of a machine learning model by training and testing it on multiple subsets of the data. This helps to prevent overfitting and provides a more accurate estimate of the model's performance on unseen data.

### 1. **K-Fold Cross-Validation**

**Definition:** K-Fold CV involves splitting the data into k subsets or "folds". The model is trained on k-1 folds and tested on the remaining fold. This process is repeated k times, with each fold serving as the test set once.

**Example (Iris Dataset):**
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import KFold
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Load iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Define k-fold CV with k=5
kf = KFold(n_splits=5, shuffle=True, random_state=42)

# Initialize accuracy scores
accuracies = []

# Iterate over k-folds
for train_index, test_index in kf.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    # Train logistic regression model on current fold
    model = LogisticRegression()
    model.fit(X_train, y_train)
    
    # Predict on test fold and calculate accuracy
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    accuracies.append(accuracy)

# Print average accuracy over k-folds
print("Average Accuracy:", sum(accuracies) / len(accuracies))
```
### 2. **Stratified K-Fold Cross-Validation**

**Definition:** Stratified K-Fold CV is a variant of K-Fold CV that preserves the class distribution in each fold. This is particularly useful when dealing with imbalanced datasets.

**Example (Iris Dataset):**
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import StratifiedKFold
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Load iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Define stratified k-fold CV with k=5
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

# Initialize accuracy scores
accuracies = []

# Iterate over k-folds
for train_index, test_index in skf.split(X, y):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    # Train logistic regression model on current fold
    model = LogisticRegression()
    model.fit(X_train, y_train)
    
    # Predict on test fold and calculate accuracy
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    accuracies.append(accuracy)

# Print average accuracy over k-folds
print("Average Accuracy:", sum(accuracies) / len(accuracies))
```
### 3. **Leave-One-Out Cross-Validation (LOOCV)**

**Definition:** LOOCV involves training the model on all data points except one, and then testing it on that single data point. This process is repeated for all data points.

**Example (Iris Dataset):**
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import LeaveOneOut
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Load iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Define LOOCV
loo = LeaveOneOut()

# Initialize accuracy scores
accuracies = []

# Iterate over data points
for train_index, test_index in loo.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    # Train logistic regression model on current data point
    model = LogisticRegression()
    model.fit(X_train, y_train)
    
    # Predict on test data point and calculate accuracy
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    accuracies.append(accuracy)

# Print average accuracy over data points
print("Average Accuracy:", sum(accuracies) / len(accuracies))
```

### **4. Train-Test Split**

**Definition:** Train-Test Split involves splitting the data into two subsets: a training set and a test set. The model is trained on the training set and evaluated on the test set.

**Example (Iris Dataset):**
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Load iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train logistic regression model on training set
model = LogisticRegression()
model.fit(X_train, y_train)

# Predict on test set and calculate accuracy
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print("Accuracy:", accuracy)
```