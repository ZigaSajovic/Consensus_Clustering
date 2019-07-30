# Consensus clustering
An implementation of Consensus clustering in Python

This repository contains a Python implementation of *consensus clustering*, following the paper [Consensus Clustering: A Resampling-Based Method for Class Discovery and Visualization of Gene Expression Microarray Data](https://link.springer.com/article/10.1023%2FA%3A1023949509487).

## ConsensusCluster

The class containing the implementation.

### Attributes

  * cluster : the class to perform the clustering (like [KMEANS](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html) from sklearn)
      * NOTE: the class is to be instantiated with parameter `n_clusters`,
        and possess a `fit_predict` method, which is invoked on data.
  * L : smallest number of clusters to try
  * K : largest number of clusters to try
  * H : number of resamplings for each number of clusters
  * resample_proportion : percentage to sample
  * Mk : consensus matrices for each k (shape =(K,data.shape[0],data.shape[0]))
      * NOTE: every consensus matrix is retained, like specified in the paper
  * Ak : area under CDF for each number of clusters
      * (see paper: section 3.3.1. Consensus distribution.)
  * deltaK : changes in areas under CDF
      * (see paper: section 3.3.1. Consensus distribution.)
  * bestK : number of clusters that was found to be best

### Methods
  
  #### ConsensusCluster.\_\_init\_\_

    Parameters:
        * cluster : the class to perform the clustering (like KMEANS from sklearn)
          * NOTE: the class is to be instantiated with parameter `n_clusters`,
            and possess a `fit_predict` method, which is invoked on data.
        * L : smallest number of clusters to try
        * K : largest number of clusters to try
        * H : number of resamplings for each number of clusters
        * resample_proportion : percentage to sample

  #### ConsensusCluster.fit

  Fits all attributes of the class to data

    Parameters:
        * data : data.shape == (n_examples,n_features) 
        * verbose : should print or not

  #### ConsensusCluster.predict

  Predicts the clustering on the consensus matrix, for best found number of cluster

    Returns:
        * Cluster labels for each example

  #### ConsensusCluster.predict_data

  Predicts the clustering on the data, for best found number of cluster

    Parameters:
        * data : data.shape == (n_examples,n_features)

    Returns:
        * Cluster labels for each example 
