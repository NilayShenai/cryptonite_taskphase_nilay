
# Nilay TaskPhase

## Overview
**AI TASKPHASE**

## Contents
1. **Linear Regression**
2. **Logistic Regression**
3. **K-Nearest Neighbors (KNN)**
4. **Decision Trees**
5. **Random Forest**
6. **Support Vector Machine (SVM)**
7. **K-Means Clustering**
8. **Hierarchical Clustering**
9. **Neural Networks**
10. **Dimensionality Reduction (PCA)**

## Getting Started
LIBS USED:
- Python (>=3.7)
- Required libraries: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `scipy`

## Example Implementations

### 1. Linear Regression
```python
from sklearn.linear_model import LinearRegression
import numpy as np

X = np.array([[1], [2], [3], [4], [5]])
y = np.array([3, 6, 9, 12, 15])

model = LinearRegression()
model.fit(X, y)
print("Predicted:", model.predict([[6]]))
```

### 2. Logistic Regression
```python
from sklearn.linear_model import LogisticRegression

X = [[1], [2], [3], [4], [5]]
y = [0, 0, 1, 1, 1]

model = LogisticRegression()
model.fit(X, y)
print("Predicted:", model.predict([[2.5]]))
```

### 3. K-Nearest Neighbors (KNN)
```python
from sklearn.neighbors import KNeighborsClassifier

X = [[1], [2], [3], [6], [7], [8]]
y = [0, 0, 0, 1, 1, 1]

model = KNeighborsClassifier(n_neighbors=3)
model.fit(X, y)
print("Predicted:", model.predict([[5]]))
```

### 4. Decision Trees
```python
from sklearn.tree import DecisionTreeClassifier

X = [[1], [2], [3], [6], [7], [8]]
y = [0, 0, 0, 1, 1, 1]

model = DecisionTreeClassifier()
model.fit(X, y)
print("Predicted:", model.predict([[4]]))
```

### 5. Random Forest
```python
from sklearn.ensemble import RandomForestClassifier

X = [[1], [2], [3], [6], [7], [8]]
y = [0, 0, 0, 1, 1, 1]

model = RandomForestClassifier(n_estimators=10)
model.fit(X, y)
print("Predicted:", model.predict([[5]]))
```

### 6. Support Vector Machine (SVM)
```python
from sklearn.svm import SVC

X = [[1], [2], [3], [6], [7], [8]]
y = [0, 0, 0, 1, 1, 1]

model = SVC(kernel='linear')
model.fit(X, y)
print("Predicted:", model.predict([[5]]))
```

### 7. K-Means Clustering
```python
from sklearn.cluster import KMeans
import numpy as np

X = np.array([[1, 2], [1, 4], [1, 0], [4, 2], [4, 4], [4, 0]])

model = KMeans(n_clusters=2)
model.fit(X)
print("Cluster Centers:", model.cluster_centers_)
```


