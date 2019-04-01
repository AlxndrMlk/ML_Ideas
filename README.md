# Machine Learning Ideas, Tips and Tricks

  This markdown contains useful information concerning machine learning, deep learning and statistics.

## Dealing with outliers in linear models

* Outlier clipping

  One of ways of dealing with outliers is clipping, using e.g. 1st and 99th percentile of the data
  
  Example:
  
  ```python 
  # Define boundaries
  LOWERBOUND, UPPERBOUND = np.percentile(x, [1, 99])
  
  # Clip the data
  x = np.clip(x, LOWERBOUND, UPPERBOUND)
  ```
