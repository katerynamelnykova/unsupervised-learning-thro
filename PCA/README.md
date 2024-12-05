_Exercise assignment for the course [Unsupervised and Reinforcement Learning (AAI-URL)](https://inf-git.fh-rosenheim.de/aai-url/hsro-aai-url-github-io) in the [Bachelor of AAI](https://www.th-rosenheim.de/en/technology/computer-science-mathematics/applied-artificial-intelligence-bachelors-degree) at [Rosenheim University of Applied Sciences](http://www.th-rosenheim.de)_

# Assigment 05 - Principal Component Analysis

> As usual: The solution is available in branch "musterloesung"!

## Task 1: Principal Component Analysis

PCA is a linear transformation that finds the “principal components”, or directions of greatest variance, in a data set. It can be used for dimension reduction among other things. 

In this task, we’re applying PCA to a simple 2-dimensional data set to see how it works. 


a) Let’s start by loading and visualizing the data set.

```python
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt 
from scipy.io import loadmat

data = loadmat('data.mat') 
X = data['X']

# todo visualize as scatter plot
```

>Note: `mat`is a MatLba file format and the scipy package can read that file!

b) Normalize and center the data and then find eigenvalues and eigenvectors.


c) Project data to PCA1 and plot.

d) Compare the result with 'sklearn.decomposition.PCA'

## Task 3: Some LinA fun :-)

In this task, we visualize how a linear operation encoded by a 2D matrix transforms a vector space. 

We use vector space to visualize the stretching and rotation of data points.

As an example, consider the matrix following matrix:

```math
A=\left( \begin{array}{rr}
2 & -1 \\ 
1 & 1 \\
\end{array}\right)
```
We can get a visual feel for this transformation by looking at a regular grid of points before and after the transformation

![image.png](./image.png)

![image-1.png](./image-1.png)


To enable this, follow the strategy:

- Create a rectangular array of points in x-y space.

- Map grid coordinates to colors that uniquely identify each point by using this funtion
```python
def colorizer(x, y):
    """
    Map x-y coordinates to a rgb color
    """
    r = min(1, 1-y/3)
    g = min(1, 1+y/3)
    b = 1/4 + x/16
    return (r, g, b)
```

- Generate a series of intermediate transforms that will “smoothly” transition from the original grid to the transformed grid. Please feel inspired by this function:
```python
def stepwise_transform(a, points, nsteps=24):
    '''
    Generate a series of intermediate transform for the matrix multiplication
      np.dot(a, points) # matrix multiplication
    starting with the identity matrix, where
      a: 2-by-2 matrix
      points: 2-by-n array of coordinates in x-y space 
    returns a (nsteps + 1)x2xn array
    '''
    # create empty array of the right size
    transgrid = np.zeros((nsteps+1,) + np.shape(points))
    for j in range(nsteps+1):
        intermediate = np.eye(2) + j/nsteps*(a - np.eye(2)) # compute intermediate matrix
        transgrid[j] = np.dot(intermediate, points) # apply intermediate matrix transformation
    return transgrid

```

- Apply it to a rotation matrix, shear matrix, permutation matrix and projection

  - rotation: 
  ```python  
  theta = np.pi/3 # 60 degree clockwise rotation
  a = np.column_stack([[np.cos(theta), np.sin(theta)], [-np.sin(theta), np.cos(theta)]])
  ```

  - shear:
  ```python
  a = np.column_stack([[1, 0], [2, 1]])
  ```

  - permutation:
  ```python
  a = np.column_stack([[0, 1], [1, 0]])
  ```
  
  - projection:
  ```python
  a = np.column_stack([[1, 0], [0, 0]])
  ```

- (optional) Plot each of the intermediate transforms and save them as individual images.
- (optional) Stitch images into a gif

![stepwise-transform.gif](./stepwise-transform.gif)


