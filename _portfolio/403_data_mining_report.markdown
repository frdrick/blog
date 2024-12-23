--- 
layout: page
title: Clustering and Classification
tags: python clustering classification dbscan optics data-mining
show_in_header: false
summary: A university project as a part of a Data Mining course  data-mining. I used the scikit-learn's implementations of the clustering algorithms DBSCAN and OPTICS to cluster some weather data from Basel, Switzerland.
image: ../assets/403_data_mining_report/k_means_3.jpeg
width: 55%
caption: 2-D projection of k-means with k = 3 using 1st & 2nd Principal components.
---

This was my first Python project and at felt like getting thrown in at the deep end. I am quite proud of how it turned out given my inexperience at the time. The task was split in two - one unsupervised and the other supervised. The unsupervised was a clustering problem on some weather data where we had no context on the time of observations. Therefore, we were roughly trying to discern which seasons different observations fell under. 

In particular implementing OPTICS was really difficult. I definitely spent much more time installing packages and pre-processing than tuning the different methods.  

![](/../assets/403_data_mining_report/optics.jpeg)

### Next time

Were I to do this project again now I would:

- Proof reading my report more thoroughly.
- Considering reviews of different clustering/classification algorithms more in when reading.
- Attempt to implement a classification algorithm on the base video feed data (we were provided with a pre-processed image too).

The full report is found here: [get pdf]({% link assets/403_data_mining_report/data_mining_report.pdf %})
