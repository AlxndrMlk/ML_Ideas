# Machine Learning Ideas, Tips and Tricks


## Dealing with outliers in liner models

* Outlier clipping

  One of ways of dealing with outliers is clipping, using e.g. 1st and 99th percentile of the data
  ```LOWERBOUND, UPPERBOUND = np.percentile(x, [1, 99])
x = np.clip(x, LOWERBOUND, UPPERBOUND)```
