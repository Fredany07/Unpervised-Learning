# Unpervised-Learning
# This repo consist of all the algorithm you need to know about unpervised learning 
Hierarchical Agglomerative Clustering (HAC) — Wine Dataset Project

Overview

This project demonstrates the full workflow of Hierarchical Agglomerative
Clustering using scipy (for the dendrogram/linkage) and scikit-learn
(for the final clustering + evaluation), applied to the built-in Wine
dataset (178 samples, 13 chemical features, 3 real cultivar classes).

Workflow implemented


Load & scale data — StandardScaler (HAC is distance-based, so
scaling every feature matters a lot).
Build linkage matrix — scipy.cluster.hierarchy.linkage() with
Ward's method (minimizes within-cluster variance growth at each merge).
Plot dendrogram — visualize merge order and distances, used to help
pick the number of clusters.
Fit AgglomerativeClustering — sklearn.cluster.AgglomerativeClustering
with linkage="ward" and n_clusters=3.
Evaluate

Silhouette score (cluster cohesion/separation, no labels needed)
Adjusted Rand Index (agreement with the true cultivar labels, since
we happen to have them for validation)
Silhouette score scanned across k=2..7 to show how you'd pick k on
an unlabeled dataset



Visualize — PCA-projected 2D scatter plots comparing HAC clusters
side-by-side with the true classes.


Files


hac_clustering.py — the full runnable pipeline
dendrogram.png — dendrogram of the last 30 merges
clusters_vs_truth.png — PCA plots: predicted clusters vs. ground truth
requirements.txt — dependencies


Run it

bashpip install -r requirements.txt
python hac_clustering.py

Results (this run)

MetricValuek (clusters chosen)3Silhouette score0.277Adjusted Rand Index vs true labels0.790

An ARI of 0.79 means the unsupervised clustering recovered the real wine
cultivar groups quite well, purely from chemical measurements — no labels
were used during clustering.

How to choose k in a real (unlabeled) project

Since you normally don't have ground-truth labels, use one of:


Dendrogram inspection — cut where the vertical gap between
successive merges is largest (biggest "jump" in distance).
Silhouette scan — try a range of k values and pick the one that
maximizes the silhouette score (see the printed table in the script
output).
