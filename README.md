# Machine Learning Ideas, Tips and Tricks

  This markdown contains useful information concerning machine learning, deep learning and statistics.

## Dealing with outliers in linear models and neural networks

* ### Outlier clipping

  One of ways of dealing with outliers is clipping, using e.g. 1st and 99th percentile of the data
  
  Example:
  
  ```python 
  # Define boundaries
  LOWERBOUND, UPPERBOUND = np.percentile(x, [1, 99])
  
  # Clip the data
  x = np.clip(x, LOWERBOUND, UPPERBOUND)
  ```
  
  Python implementation ![here](https://github.com/AlxndrMlk/dataScienceHelpers/blob/master/percent_clipper.py)
  
  
  
* ### Rank transformation

  ```python
  from scipy.stats import rankdata
  x = rankdata(x)
  ```
  
  Documentaition ![here](https://docs.scipy.org/doc/scipy-0.16.0/reference/generated/scipy.stats.rankdata.html)
  
  
  
* ### Non-linear transformations (useful for ANNs)
  
  ```python
  # Log transformation
  x = np.log(1 + x)
  ```
  
  ```python
  # Power < 1 transformation
  x = np.sqrt(x + 2/3)
  ```
  
## Feature generation

  Gradient boosting is a powerful model but it has a hard time approximating multiplication and division. Adding multiplied / divided features is a powerful trick even for boosting.
  
  
