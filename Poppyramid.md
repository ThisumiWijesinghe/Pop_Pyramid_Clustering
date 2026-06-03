# Population Pyramid Analysis using Spectral Clustering and PCA

## Overview

This project analyzes global population pyramids using **Spectral Clustering** and **Principal Component Analysis (PCA)**.

The dataset contains:

* Population data for multiple countries
* 21 age groups
* Multiple years (1950–2100)
* Male, female, and total population counts

The main goal of the project is to:

1. Group countries with similar population structures
2. Identify demographic patterns over time
3. Visualize similarities and transitions in population pyramids
4. Reduce high-dimensional demographic data into 2D visual representations using PCA

---

# Project Objectives

* Analyze demographic similarities between countries
* Cluster countries based on age distributions
* Track how demographic structures change over time
* Find the optimal number of clusters using eigengap analysis
* Visualize clusters using PCA
* Compare population pyramid shapes between clusters

---

# Dataset Information

The dataset file used:

```python
age_data_1.csv
```

Main columns:

| Column    | Description       |
| --------- | ----------------- |
| Time      | Year              |
| Location  | Country name      |
| AgeGrp    | Age group         |
| PopTotal  | Total population  |
| PopMale   | Male population   |
| PopFemale | Female population |

Each country contains population values for 21 age groups.

---

# Why Spectral Clustering?

Traditional clustering methods like K-Means assume clusters are:

* Spherical
* Linearly separable
* Similar in size

However, population pyramids are complex demographic distributions.
Countries can have:

* Aging populations
* Youth-heavy populations
* Transitional structures
* Irregular demographic patterns

These patterns are not always linearly separable.

Therefore, **Spectral Clustering** was selected because it:

* Works well with non-linear structures
* Uses graph-based similarity
* Captures complex relationships
* Produces better demographic grouping

---

# Spectral Clustering Methodology

## Step 1 — Load Data

The dataset is filtered for a selected year.

Example:

```python
YEAR = 2020
```

---

## Step 2 — Pivot Population Pyramid

The data is converted into a matrix:

| Country   | Age Group Features |
| --------- | ------------------ |
| Sri Lanka | 21 age values      |
| Japan     | 21 age values      |
| India     | 21 age values      |

Each country becomes a feature vector with 21 dimensions.

---

## Step 3 — Normalize Population Pyramids

Normalization converts raw populations into proportions.

Code used:

```python
X_norm = normalize(X, norm="l1")
```

### Why normalization is important

Countries have very different total populations.

Example:

* India population is much larger than Sri Lanka
* Without normalization, clustering would mainly depend on country size

L1 normalization ensures:

[
\sum_{i=1}^{21} x_i = 1
]

This means the clustering focuses on:

* Shape of the population pyramid
* Age distribution structure
* Demographic pattern

instead of total population size.

---

# k-Nearest Neighbor (kNN) Graph

A graph is created using:

```python
kneighbors_graph()
```

Each country connects to its nearest demographic neighbors.

Parameter used:

```python
N_NEIGHBORS = 12
```

### Why kNN graph?

The graph represents similarity relationships between countries.

Countries with similar population structures become connected.

This creates an affinity matrix:

[
W
]

where:

[
W_{ij} = 1
]

if countries (i) and (j) are neighbors.

---

# Affinity Matrix

The affinity matrix stores similarities between countries.

Symmetric matrix construction:

```python
W = 0.5 * (W + W.T)
```

This ensures:

[
W = W^T
]

which is required for spectral graph analysis.

---

# Degree Matrix

The degree matrix contains the number of connections for each country.

Formula:

[
D_{ii} = \sum_j W_{ij}
]

where:

* (D) = degree matrix
* (W) = affinity matrix

---

# Graph Laplacian

The normalized graph Laplacian is computed as:

genui{"math_block_widget_always_prefetch_v2":{"content":"L = I - D^{-1/2} W D^{-1/2}"}}

Implemented using:

```python
L = np.eye(W.shape[0]) - D_inv_sqrt @ W @ D_inv_sqrt
```

### Why Laplacian?

The Laplacian captures:

* Graph connectivity
* Community structure
* Cluster boundaries

Countries within the same demographic group produce similar spectral properties.

---

# Eigenvalues and Eigengap Analysis

The eigenvalues of the Laplacian are computed.

Formula:

[
L v = \lambda v
]

where:

* (L) = Laplacian matrix
* (v) = eigenvector
* (\lambda) = eigenvalue

The eigengap method is used to estimate the optimal number of clusters.

### Eigengap Principle

A large gap between consecutive eigenvalues indicates cluster separation.

Example:

| Eigenvalue | Value |
| ---------- | ----- |
| λ1         | 0.01  |
| λ2         | 0.03  |
| λ3         | 0.05  |
| λ4         | 0.62  |

Large gap between λ3 and λ4 suggests:

```python
k = 3
```

This was used to:

* Find optimal cluster counts
* Analyze demographic evolution over time

---

# Spectral Clustering Execution

The clustering model:

```python
SpectralClustering()
```

Main parameters:

| Parameter              | Purpose                |
| ---------------------- | ---------------------- |
| n_clusters             | Number of clusters     |
| affinity='precomputed' | Uses similarity matrix |
| assign_labels='kmeans' | Final label assignment |
| random_state=42        | Reproducibility        |

---

# Temporal Analysis (1950–2100)

The project also performs clustering across multiple years.

Example:

```python
START_YEAR = 1950
END_YEAR = 2100
YEAR_STEP = 5
```

This helps analyze:

* Demographic transitions
* Population aging
* Fertility decline
* Long-term population changes

The model recalculates clusters for each year.

---

# PCA (Principal Component Analysis)

## Why PCA?

The dataset contains 21 dimensions.

Visualization in 21D is impossible.

PCA reduces dimensions while preserving most variance.

The project uses:

```python
PCA(n_components=2)
```

to convert data into:

* PC1 (Principal Component 1)
* PC2 (Principal Component 2)

---

# PCA Methodology

## Step 1 — Input Matrix

The normalized matrix:

[
X_{norm}
]

is used as PCA input.

---

## Step 2 — Covariance Structure

PCA identifies directions with maximum variance.

Covariance matrix:

[
C = \frac{1}{n-1} X^T X
]

---

## Step 3 — Eigen Decomposition

PCA computes eigenvectors and eigenvalues.

* Eigenvectors → principal components
* Eigenvalues → variance explained

---

# Principal Components

PCA transforms the data:

[
Z = XW
]

where:

* (X) = original data
* (W) = principal component vectors
* (Z) = transformed low-dimensional data

---

# Explained Variance

The explained variance ratio shows how much information is preserved.

Code used:

```python
explained = pca.explained_variance_ratio_.sum()
```

Higher explained variance means:

* Better dimensional reduction
* Better structure preservation

---

# PCA Visualization

Countries are plotted in 2D space.

Countries close together indicate:

* Similar demographic structures
* Similar population pyramids

Cluster colors represent spectral clustering labels.

This allows visual validation of clusters.

---

# Population Pyramid Cluster Analysis

The project also visualizes:

* Average male population pyramids
* Average female population pyramids
* Cluster-wise demographic structures

This helps identify:

* Youth-heavy countries
* Aging populations
* Stable populations
* Transitional demographics

---

# Key Techniques Used

| Technique           | Purpose                                        |
| ------------------- | ---------------------------------------------- |
| Data Pivoting       | Convert country-age structure into matrix form |
| L1 Normalization    | Remove total population bias                   |
| kNN Graph           | Build similarity network                       |
| Affinity Matrix     | Represent country relationships                |
| Graph Laplacian     | Capture graph structure                        |
| Eigengap Analysis   | Determine optimal clusters                     |
| Spectral Clustering | Group similar countries                        |
| PCA                 | Dimensionality reduction and visualization     |

---

# Libraries Used

```python
pandas
numpy
matplotlib
scikit-learn
```

Main sklearn modules:

```python
SpectralClustering
PCA
normalize
kneighbors_graph
```

---

# Results and Observations

The clustering revealed multiple demographic patterns:

### Common cluster types

* Aging populations
* Youth-dominated populations
* Transitional populations
* Balanced demographic structures

### Observations over time

* Many countries move from youth-heavy to aging structures
* Developed countries tend to form aging clusters
* Developing countries often remain youth-dominant
* Demographic transitions become visible through PCA movement

---

# Advantages of the Approach

## Spectral Clustering Advantages

* Handles non-linear data
* Works well with graph structures
* Better for complex demographic patterns
* Captures local similarities

## PCA Advantages

* Reduces dimensionality
* Preserves major variance
* Enables visualization
* Simplifies analysis

---

# Limitations

* Spectral clustering can be computationally expensive
* Results depend on kNN parameter selection
* PCA may lose some information during reduction
* Cluster interpretation can sometimes be subjective

---



# Conclusion

This project successfully applied:

* Spectral Clustering
* Graph theory concepts
* Eigengap analysis
* PCA visualization

to analyze global population pyramid structures.

The methodology effectively grouped countries with similar demographic characteristics and visualized long-term demographic transitions from 1950–2100.

The combination of Spectral Clustering and PCA provided:

* Meaningful demographic grouping
* Clear visual interpretation
* Strong representation of complex population structures
