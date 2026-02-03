🌍 Global Demographic Evolution (1950–2100)
AI-Powered Clustering of World Population Pyramids

This project analyzes the demographic transition of under 200 countries across a 150-year period (1950–2100) using unsupervised machine learning.
Rather than relying on single indicators such as fertility or median age, countries are clustered based on the entire shape of their population pyramids, capturing holistic demographic structure and evolution.

🚀 Project Overview

Population pyramids encode the combined effects of fertility, mortality, and migration.
This research leverages Spectral Clustering and Hierarchical Clustering to identify global demographic patterns and classify countries into structural demographic archetypes.

Each country is represented by 21 age groups, normalized to population shares, allowing comparisons across countries of vastly different population sizes.

🛠️ Technical Workflow
1️⃣ Data Preprocessing

UN population data (1950–2100)

21 age groups per country

Normalization using L1 norm (population shares instead of raw counts)

2️⃣ Dimensionality Reduction

Principal Component Analysis (PCA)

Retains ≈95% of variance

Used to denoise high-dimensional age distributions (not only for visualization)

3️⃣ Clustering Models

Spectral Clustering

k-Nearest Neighbor (kNN) affinity graph

Eigenvalue gap method for optimal cluster selection

Hierarchical Clustering

Ward’s linkage

Reveals nested demographic similarity structures

4️⃣ Model Evaluation

Eigengap heuristic

Silhouette score comparison

Cluster stability across years

5️⃣ Visualization

🌐 World choropleth maps (cluster assignments)

👥 Back-to-back population pyramids

⏳ Long-term demographic trajectory analysis (1950–2100)

📊 Demographic Stages Identified

Based on clustering results, countries broadly align with the following demographic archetypes:

Expansive (High Growth)
Wide base, high fertility, youthful population

Stationary (Transitional)
Large working-age cohorts, declining fertility

Constrictive (Aging)
Narrow base, population ageing, low fertility

These stages correspond closely to the Demographic Transition Model (DTM) but are identified data-driven, without predefined thresholds.

📌 Research Contribution

This work addresses key gaps in existing demographic studies:

Moves beyond single-indicator analysis (fertility, mortality alone)

Applies unsupervised learning to full age distributions

Introduces a dual-layered clustering framework:

Static morphology (population structure at a given year)

Dynamic evolution (pathways through the DTM over decades)

This approach enables policy-relevant benchmarking that accounts for both current demographic conditions and historical momentum.

💻 Installation & Usage
# Clone the repository
git clone https://github.com/your-username/demographic-clustering.git

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn geopandas plotly


Run clustering scripts year-wise or across trajectories to reproduce figures and maps.

📈 Outputs

Clustered country lists (CSV)

World maps colored by demographic archetype

Comparative population pyramid panels

Eigenvalue spectra and eigengap plots

📚 Data Source

United Nations World Population Prospects (WPP)(Filtered Age data file)

✍️ Author

W. A. Thisumi Nimsani
BSc (Hons) Computer Science with Artificial Intelligence
NIBM Sri Lanka

🧠 Suggested Extensions

Temporal spectral clustering on full trajectories

Integration with health or economic indicators

Forecast-aware clustering using projected pyramids