# Population Pyramid Clustering

This project clusters countries based on their population pyramids using K-Means, DBSCAN, and Spectral Clustering.

## Population Pyramid Summary
A population pyramid shows the age and gender distribution of a population. Its shape reveals demographic trends, such as whether a country has a young, balanced, or aging population. This helps in planning for healthcare, education, and workforce needs, and is useful for comparing populations across countries or over time.

## Dataset
- Source: `age_data.csv`
- Year Used: 2021
- Features: 21 age groups per country (PopTotal values)
- Each row represents a country’s population distribution for one year.

## Methods Used
- **K-Means**: Clear, broad categories.
- **DBSCAN**: Finds unusual demographic patterns.
- **Spectral Clustering**: Groups with complex boundaries.

## How to Run
```bash
pip install pandas scikit-learn matplotlib seaborn
python clustering_script.py


# Clustering Countries by Population Pyramids

## Project Overview

This project uses unsupervised machine learning to cluster countries based on their population pyramid structures for the year 2021. The goal is to identify groups of countries with similar demographic profiles. The analysis is performed using three different clustering algorithms: K-Means, DBSCAN, and Spectral Clustering.

## Dataset

The dataset used is `age_data.csv`, which contains population data broken down by 21 age groups for various countries. This analysis specifically filters the data for the year 2021.

The data has the following relevant columns:
* `Location`: The country name.
* `Time`: The year of the data.
* `AgeGrpStart`: The starting age of the age group.
* `PopTotal`: The total population in that age group.

## Methodology

The analysis follows these steps:

1.  **Data Preprocessing:**
    * The data is filtered to include only records from the year 2021.
    * The dataset is pivoted to create a matrix where rows are countries and columns are age groups, with the values being the population for each age group.
    * The population values for each country are normalized to represent the proportion of the population in each age group. This ensures that countries are compared based on the shape of their population distribution, not their total population size.

2.  **Dimensionality Reduction (PCA):**
    * Principal Component Analysis (PCA) is used to reduce the 21 dimensions (age groups) to 2 principal components. This is done primarily for visualizing the clusters on a 2D scatter plot.

3.  **Clustering Algorithms:**
    * **K-Means Clustering:** The countries are grouped into 4 clusters.
    * **DBSCAN:** A density-based clustering algorithm is applied to identify clusters without a predefined number. It also identifies outlier countries as "noise".
    * **Spectral Clustering:** A graph-based clustering method is used to group countries into 4 clusters.

## How to Run the Script

1.  **Prerequisites:** Make sure you have Python installed, along with the following libraries:
    * pandas
    * scikit-learn
    * matplotlib
    * seaborn

    You can install them using pip:
    ```bash
    pip install pandas scikit-learn matplotlib seaborn
    ```

2.  **Execution:**
    * Place the `age_data.csv` file in the same directory as the Python script (`pop_pyramid_task.py`).
    * Run the script from your terminal:
    ```bash
    python pop_pyramid_task.py
    ```

## Results and Outputs

The script will generate the following outputs:

### Visualizations

Several plots will be generated and displayed for each clustering algorithm, allowing for a comparative analysis:

* **PCA Variance Explained Plot:** Shows the percentage of variance captured by the principal components.
* **Cluster Scatter Plots:** For each algorithm, a 2D scatter plot of the clusters based on the first two principal components.
* **Average Population Pyramid Plots:** For each cluster found by each algorithm, a bar chart showing the average population distribution. These plots are key to understanding the demographic characteristics of each cluster.

### Output Files

The script will also save the clustering results to CSV files:

* `kmeans_countries.csv`: A file containing each country and its assigned K-Means cluster.
* `clustered_countries.csv`: This file is overwritten in script. In its final state, it will contain the K-Means cluster for each country.

By examining the plots and the output files, one can gain insights into the different patterns of population structures that exist across the globe.