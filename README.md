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
