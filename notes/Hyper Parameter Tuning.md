**Hyperparameter Tuning**
=========================

**Definition**
---------------

Hyperparameter tuning is the process of selecting the optimal hyperparameters for a machine learning model to achieve the best performance on a given dataset. Hyperparameters are parameters that are set before training a model, as opposed to model parameters, which are learned during training.

**Types of Hyperparameter Tuning**
---------------------------------

### 1. **Grid Search**

Grid search is a simple and exhaustive method that involves trying all possible combinations of hyperparameters within a specified range.

```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'learning_rate': [0.1, 0.01, 0.001],
    'max_depth': [3, 5, 10],
    'n_estimators': [10, 50, 100]
}

grid_search = GridSearchCV(estimator=model, param_grid=param_grid, cv=5)
grid_search.fit(X_train, y_train)
```

### 2. **Random Search**

Random search is a more efficient method that involves randomly sampling hyperparameters from a specified distribution.

```python
from sklearn.model_selection import RandomizedSearchCV

param_distributions = {
    'learning_rate': [0.1, 0.01, 0.001],
    'max_depth': [3, 5, 10],
    'n_estimators': [10, 50, 100]
}

random_search = RandomizedSearchCV(estimator=model, param_distributions=param_distributions, cv=5, n_iter=10)
random_search.fit(X_train, y_train)
```

### 3. **Bayesian Optimization**

Bayesian optimization is a more advanced method that uses a probabilistic approach to search for the optimal hyperparameters.

```python
from skopt import gp_minimize
from skopt.space import Real, Categorical, Integer

search_space = [
    Real(0.001, 1.0, name='learning_rate'),
    Categorical([3, 5, 10], name='max_depth'),
    Integer(10, 100, name='n_estimators')
]

def optimize_hyperparameters(params):
    model.set_params(**params)
    model.fit(X_train, y_train)
    return model.score(X_val, y_val)

result = gp_minimize(optimize_hyperparameters, search_space, n_calls=10)
```

### 4. **Gradient-Based Optimization**

Gradient-based optimization methods, such as gradient descent, can also be used for hyperparameter tuning.

```python
import torch

def optimize_hyperparameters(params):
    model.set_params(**params)
    model.fit(X_train, y_train)
    loss = model.loss(X_val, y_val)
    return loss

params = torch.tensor([0.1, 3, 10], requires_grad=True)
optimizer = torch.optim.Adam([params], lr=0.01)

for epoch in range(10):
    loss = optimize_hyperparameters(params)
    loss.backward()
    optimizer.step()
    optimizer.zero_grad()
```

Note: The above code snippets are just examples and may need to be modified to fit your specific use case.