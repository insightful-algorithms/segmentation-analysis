# Segmentation Analysis
This is an Segmentation Analysis that using K-Means clustering algorithms to understand the purchasing behaviour of the customers of E-Shop Pro

![image](https://www.c5i.ai/wp-content/uploads/Approach-to-Segmentation-Analysis1-2.png)

After the Heat Map of the quantity table dataframe, I performed the following tasks
1. Aggregated the data for each customer by calculating TotalPrice for each transaction line (Quantity * UnitPrice).
2. Grouped the data by CustomerID to combine all transactions belonging to the same customer.
3. Aggregated relevant metrics:
    - Sum of quantities purchased (TotalQuantity),
    - Sum of total prices (TotalSpent),
    - Count of unique invoices (TotalInvoices).
4. Renamed these aggregated columns to be clearer and more descriptive.
5. Produced a customer-level DataFrame (customer_df) that can be used for further analysis or clustering. This DataFrame now has one row per customer with the main features capturing their overall purchasing behavior.
6. The next step was to prepare the numerical features for clustering by putting them in a comparable scale and getting the shape of the dataframe by carrying out the following steps:
    - Extracted the three chosen features (TotalQuantity, TotalInvoices, TotalSpent) from the customer_df DataFrame to form a feature matrix X.
    - Standardized each feature to have zero mean and unit variance by using StandardScaler. This is a critical step for many distance-based or gradient-based algorithms—such as K-Meansensure no single feature dominates due to its scale.
    - Stored the transformed data in X_scaled and confirmed its dimensions.
7. The next step implement the Elbow Method to help find an optimal number of clusters for K-Means. The code recorded the WCSS (within-cluster sum of squares) for each fit. Then ploted WCSS vs. k to  visually detect the elbow point—where adding more clusters no longer significantly reduces the total variance within each cluster. This elbow is a common heuristic for choosing a good value of k in K-Means clustering.
8. The next thing I did was to chose 5 clusters because of the elbow joint from the previous step to the scaled customer data, assigning each customer to one of 5 clusters. The result is stored in the Cluster column of customer_df. This showed which cluster each customer belonged to.
9. The next step was to profile each cluster by grouping customers by their assigned Cluster.
10. The next step was to import the PCA class from sklearn.decomposition and initialize it with n_components=2, so as to reduce the dataset to two principal components. Then I called pca.fit_transform(X_scaled) on the standardized dataset (X_scaled), which performed a Principal Component Analysis and returned a two-dimensional representation of each data point in X_pca. Subsequently, I created a scatter plot of these two principal components on the x- and y-axes (PC1 and PC2).  Finally, the user added a colorbar to reflect the cluster assignments and displayed the plot. Then I visualized the distribution of the K-Means clusters in a two-dimensional space, making it easier to observe how different customers in the dataset might cluster together when reduced to just two principal components.
