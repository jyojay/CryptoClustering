# CryptoClustering
##### Unsupervised Learning project on Crypto data

In this challenge knowledge of Python and unsupervised learning was used to predict if cryptocurrencies are affected by 24-hour or 7-day price changes.

## Table of Contents

- [Repository Folders and Contents](#Repository-Folders-and-Contents)
- [Details](#Details)
  
## Repository Folders and Contents
- Resources:
  - crypto_market_data.csv
    
- Output:
  - Elbow curve PCA.png
  - Elbow curve.png
  - Scatter plot PCA.png
  - Scatter plot.png
  
- Crypto_Clustering.ipynb

## Details
### Tools/Libraries Imported:
- pandas
- hvplot.pandas
- KMeans from sklearn.cluster
- PCA from sklearn.decomposition
- StandardScaler from sklearn.preprocessing

### Prepare the Data
Data was normalised using StandardScaler to produce below result </br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/77014533-10bb-4b7c-a277-a5f259fb11fb)

### Find the Best Value for k Using the Original Scaled Data
Using Kmeans technique for the scaled data, an elbow curve was plotted to determine the best value of k </br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/ef4d8422-8b11-43db-ac76-250a8c45569f) </br>
Based on this Elbow Curve, **k=4** looked like the best value.

### Cluster Cryptocurrencies with K-means Using the Original Scaled Data
Using number of clusters = 4 which seemed to be the best value of k, model was initialised and fit followed by predicting clusters.
The resulting array of cluster values was as below </br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/a0ab89b6-61c4-4b8e-a00a-11313239bb1a) </br>

A scatter plot was plotted with x="price_change_percentage_24h", y="price_change_percentage_7d" colour coded by labels found using k-means and adding the crypto name in the `hover_cols` </br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/42517c54-1339-40e2-9211-0e5to 1b48e2389) </br>

### Optimise Clusters with Principal Component Analysis.
Using `n_components=3` created a PCA model instance then used `fit_transform` to reduce to three principal components. Retrieved the explained variance to determine how much information could be attributed to each principal component </br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/673f1b1f-76ac-4f89-9c51-1449ed164256) <\br>
Total explained variance of the 3 principal components was found to be 0.89317787 or **89%** <\br>
Created a new dataframe with PCA data <\br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/cee59daf-92f4-43a5-9197-a433f06cdfc0) <\br>

### Find the Best Value for k Using the PCA Data
Inertia was computed for eac possible value of k using PCA data and an elbow curve was drawn as below <\br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/7545212e-c1a7-4f6c-9d0a-a611d262e6a9) <\br>
**The best value of k was found to be 4 using PCA data** same as the value found using original scaled data <\br>

### Cluster Cryptocurrencies with K-means Using the PCA Data
Using number of clusters = 4 based onthe best k value, model was initialised and fit followed by predicting clusters.
The resulting array of cluster values was as below </br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/e3cb6277-0f40-4904-8747-ee659e0c3ffd) <\br>
![image](https://github.com/jyojay/CryptoClustering/assets/132628129/7a42a552-bd56-4f97-a7ee-30f4a80914f3) <\br>
A scatter plot was plotted with x="PC1", y="PC2" colour coded by labels found using k-means and adding the crypto name in the `hover_cols` </br>

### Visualise and Compare the Results
`(original_data_plot + pca_data_plot).cols(1)` and `(original_data_scatter + pca_data_scatter).cols(1)` were used to create composite plots one on top of the other to compare results from original scaled data and PCA data of both Elbow curve and scatter plot
Looking at the elbow curves the k value can more distinctly be identified using fewer features(PCA). Comparing the scatter plots also the one with fewer features shouwed more clear segmentation between all the clusters. In case of the plot using all features, various axes would need to probably be tried to see a clearer distinction in segmentation of clusters even though it appears that cluster analysis using the DataFrame with all of the features yielded same results as PCA analysis.






