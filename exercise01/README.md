_Exercise assignment for the course [Unsupervised and Reinforcement Learning (AAI-URL)](https://inf-git.fh-rosenheim.de/aai-url/hsro-aai-url-github-io) in the [Bachelor of AAI](https://www.th-rosenheim.de/en/technology/computer-science-mathematics/applied-artificial-intelligence-bachelors-degree) at [Rosenheim University of Applied Sciences](http://www.th-rosenheim.de)_

# Assigment 01 - Python, Elbow method, and Hierarchical Clustering

> **As usual: The solution is availabe in branch "musterloesung"!**

## Task 1 - Elbow method and Silhouette score

To apply the K-means clustering algorithm, let's load the Palmer Penguins dataset, choose the columns that will be clustered, and use some libs to plot a scatterplot with color-coded clusters.

Download the dataset from here: https://gist.github.com/slopp/ce3b90b9168f2f921784de84fa445651

Let's import some libraries and load the Penguins dataset, trimming it to the chosen columns and dropping rows with missing data (there were only 2):

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

df = pd.read_csv('penguins.csv')
print(df.shape)

df = df[['bill_length_mm', 'flipper_length_mm']]
df = df.dropna(axis=0)
```

Write some code to identify k using the Elbow method and Silhouette score from the lecture.

NOTE: You can simply pass df to KMeans as values!

## Task 2 - Hierarchical Clustering on paper

Use single and complete link agglomerative clustering to group the data described by the following distance matrix. Show the dendrograms!

![Alt text](image.png)

## Task 3 - Hierarchical Clustering in Python

Let’s take a look at a concrete example of how we could go about labeling data using **hierarchical agglomerative clustering**.

In this tutorial, we use the csv file containing a list of customers with their gender, age, annual income, and spending score. Use the mall customers' data from here: https://inf-git.fh-rosenheim.de/aai-url/01_exercise/-/blob/main/data.csv

Also, use the following imports:

```python
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
from sklearn.cluster import AgglomerativeClustering
from scipy.cluster.hierarchy import dendrogram, linkage
```

a) Load data

Load the data from the file by using the pandas `read_csv` method and use only columns 3 and 4 by using this expression

```python
X = dataset.iloc[:, [3, 4]].values
```

b) Find k

Try to find k by using either the Elbow method or the Silhouette score

c) Compare linkage

Create clusters using Agglomerative Clustering and k from b for various linkages: 'ward', 'complete', 'average', and 'single'.

Compare the results. Which one is the best?