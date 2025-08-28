# Population Pyramid Clustering

##  Overview
This project clusters countries based on their population pyramids (age-group distribution).  
I used 2021 UN population data and applied multiple clustering techniques to compare results.

## 🔧 Steps Done
1. **Data Preprocessing**
   - Loaded `age_data.csv`.
   - Selected columns: `Location`, `Time`, `AgeGrpStart`, `PopTotal`.
   - Filtered for **year = 2021**.
   - Kept only recognized countries.
   - Pivoted dataset → rows = countries, columns = age groups, values = population.
   - Normalized to population proportions.

2. **Scaling**
   - Standardized values using `StandardScaler`.

3. **Clustering Methods**
   - **KMeans (k=4)**
   - **DBSCAN (eps=0.8, min_samples=7)**
   - **Spectral Clustering** (optimal cluster number chosen using eigengap heuristic).
   - **Agglomerative Clustering (Ward linkage, k=4)**

4. **Evaluation Metrics**
   - **Silhouette Score** (higher = better separation).
   - **Davies-Bouldin Index (DBI)** (lower = better).
   - **Calinski-Harabasz Index (CHI)** (higher = better).

5. **Visualization**
   - PCA projection (2D scatter plots).
   - Average population pyramids for each cluster.

6. **Outputs**
   - `all_clustering_results.csv` → contains each country’s cluster labels from all four methods.

---

##  Results (Sample Metrics)

- **KMeans** → Silhouette=0.417, DBI=0.688, CHI=157.0  
- **DBSCAN** → Silhouette=0.570, DBI=0.452, CHI=121.9  
- **Spectral** → Silhouette=0.422, DBI=0.812, CHI=135.1  
- **Agglomerative** → Silhouette=0.347, DBI=0.750, CHI=120.3  

---

##  Next Steps
- Compare the **interpretation of clusters** (young populations, ageing populations, etc.).
- Decide on the best clustering method to highlight in the report/presentation.
- Possibly refine DBSCAN parameters to see if better grouping emerges.
