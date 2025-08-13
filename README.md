# Population Pyramid Clustering

This project clusters countries based on their population pyramids using K-Means, DBSCAN, and Spectral Clustering.

### Key Updates
- Uses one CSV file(age_data.csv)
- Filters data to only year 2021
- Uses exactly 21 age group variables per country (PopTotal values)
- Includes 3 clustering methods  :K-Means,DBSCAN and Spectral Clustering 
- PCA variance explained plot added to assess dimensionality reduction 
-Saves seperate CSVs for each clustering methods
- Spectral Clustering automatically determines optimal number of clusters using the eigengap heuristic
- Generates text files listing countries under each cluster for all 3 methods 
- All preprocessing,clustering and Visualization steps in one script

## Population Pyramid Summary
A population pyramid shows the age and gender distribution of a population. Its shape reveals demographic trends, such as whether a country has a young, balanced, or aging population. This helps in planning for healthcare, education, and workforce needs, and is useful for comparing populations across countries or over time.

## Dataset
- Source: `age_data.csv`
- Year Used: 2021
- Features: 21 age groups per country (PopTotal values)
- Each row represents a country’s population distribution for one year.

## Methods Used
- **K-Means**: Groups countries into broad,clearly defined clusters (4 clusters used here)
- **DBSCAN**: Identifies dense clusters and outliers , parameters(eps,min_samples) tuned to get meaningful results.
- **Spectral Clustering**: Captures complex boundaries between demographic groups and automatically selects the optimal number of clusters using the eigengap heuristic.

# Methodology
1.Data Preprocessing
- Filtered the dataset to year 2021 only 
-Pivoted so rows = countries,columns=age groups(21 variables),values=total population 
- Normalized values to represent population proportions rather than total size 

2.Dimentionality Reduction(PCA)
- Reduced 21 variables to 2 principal components for visualization 
- Plotted variance explained to show how much information is retained.

3.Clustering:
- K-Means : Predefined 4 clusters to group countries with similar demographic patterns.
- DBSCAN: Unsupervised density-based method to detect natural clusters and outliers without a fixed no of clusters .
- Spectral Clustering: Graph-based approach to detect non-linear cluster shapes and optimal number of clusters is selected using the eigengap heuristic.

4.Export & Visualization:
- PCA scatter plots for each clustering method 
- Average pop pyramid bar plots for each cluster
- CSV files mapping each country to its cluster for all 3 methods in one file.(all_clustering_results.csv)
- Text files listing countries under each cluster for K-Means,DBSCAN and Spectral clustering.


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
    * Place the `age_data.csv` file in the same directory as the Python script (`pop_pyramid_task3.py`).
    * Run the script from your terminal:
    ```bash
    python pop_pyramid_task3.py
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
* `dbscan_countries.csv`: Country to DBSCAN cluster mapping(including -1 for outliers)
* `spectral_countries.csv`:
Country to spectral clustering cluster mapping 
* `all_clustering_results.csv`: Consolidated CSV of cluster assignments for all 3 methods .
* `_cluster_countries.txt`:Text files listing countries in each cluster for all 3 methods 


# Insights
- Cluster0 : countries with younger populations
- Cluster1 : Countries with balanced age distribution
- Cluster2 : Countries with aging populations
- Cluster3 : Mixed demographic patterns
- DBSCAN is better for finding unusual profiles , while K-Means is easier for broad interpretation.
-Spectral Clustering with eigengap heuristic automatically identifies the optimal number of clusters,capturing complex demographic patterns

By examining the plots and the output files, one can gain insights into the different patterns of population structures that exist across the globe.