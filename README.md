# Project: Hepatitis C Virus (HCV) Dataset Clustering Analysis

This project performs a clustering analysis on the Hepatitis C Virus (HCV) dataset (`hcvdat0.csv`). The primary objective is to identify inherent groupings within the data using the DBSCAN clustering algorithm, chosen for its ability to handle datasets with outliers and imbalanced classes.

---

## Dataset

The analysis utilizes the `hcvdat0.csv` dataset, which contains medical and demographic data related to Hepatitis C. Initial observations from the notebook indicate that the dataset is imbalanced and contains outliers.

---

## Methodology

The analysis follows these key steps:

1.  **Data Loading and Initial Exploration:**
    * The dataset is loaded using pandas.
    * Descriptive statistics (`df.describe()`) are generated to understand the data distribution.
    * The presence of missing values is checked (`df.isna().sum()`, `df.isnull().sum()`).

2.  **Data Preprocessing:**
    * Missing values are handled by removing rows with any NaN values (`df.dropna(axis=0, inplace=True)`).
    * Categorical features ("Category", "Sex") are converted into numerical representations using `LabelEncoder`.

3.  **Exploratory Data Analysis (EDA):**
    * Histograms (`df.hist()`) are generated for all numerical features to visualize their distributions.
    * The distribution of the "Category" feature is visualized using a bar plot.
    * Box plots (`df.plot(kind="box", subplots=True, layout=(4,4))`) are created to identify the spread and potential outliers for each numerical feature.
    * A correlation matrix (`df.corr()`) is computed and visualized to understand relationships between features.

4.  **Feature Scaling:**
    * Independent variables (excluding 'Category' and 'Unnamed: 0') are scaled using `StandardScaler` to normalize the data and mitigate the impact of outliers on the clustering algorithm.

5.  **Clustering with DBSCAN:**
    * The DBSCAN (Density-Based Spatial Clustering of Applications with Noise) algorithm is selected.
    * **Parameter Tuning (`eps`):**
        * The Silhouette Score is calculated for a range of `eps` values (0.1 to 1.9 with a step of 0.1) to identify an optimal value. The `min_samples` parameter is set to 5.
        * A k-distance plot is generated (using `NearestNeighbors` with k=5) to further aid in the selection of an appropriate `eps` value by observing the "elbow" point in the curve of distances to the k-nearest neighbors.
    * The final DBSCAN model is run with the determined optimal `eps` value and `min_samples=5`.
    * Cluster labels are assigned to the cleaned dataframe.

6.  **Cluster Analysis & Visualization:**
    * The number of identified clusters and the count of data points in each cluster (including noise points labeled as -1) are reported.
    * Principal Component Analysis (PCA) is used to reduce the dimensionality of the scaled data to 2 components for visualization purposes.
    * The identified clusters are plotted using a scatter plot of the first two principal components.
    * Local Outlier Factor (LOF) is applied to calculate the average LOF density for each identified cluster, providing an insight into the density of the clusters.

---

## Results

* The optimal `eps` value for DBSCAN, as determined by the Silhouette Score analysis, was found to be **1.9**.
* The DBSCAN algorithm identified **2 distinct clusters** and a set of outliers (noise points).
    * Cluster 0: 291 samples
    * Cluster 1: 203 samples
    * Outliers (-1): 95 samples
* The LOF density analysis provided average density scores for each cluster:
    * Cluster 0: LOF Density Média = -1.0000
    * Cluster 1: LOF Density Média = -0.9901
* The PCA plot visually represents the separation of these clusters in a 2-dimensional space.

---

## Files in This Repository

* `Clusterização.ipynb`: The Jupyter Notebook containing the Python code for the analysis.
* `hcvdat0.csv`: The dataset used for this project.
* `README.md`: This file, providing an overview of the project.

---

## How to Run

1.  Ensure you have Python installed.
2.  Install the necessary libraries:
    ```bash
    pip install pandas matplotlib scikit-learn numpy
    ```
3.  Download the `Clusterização.ipynb` notebook and the `hcvdat0.csv` dataset into the same directory.
4.  Open and run the Jupyter Notebook using an environment like Jupyter Lab or Google Colab.

---
