# Machine Learning Ideas, Tips and Tricks

  This markdown contains useful information concerning machine learning, deep learning and statistics.
  
  
## Dealing with outliers 

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
  
## Feature generation and extraction

* ### Use mulitplications and divisions  

  Gradient boosting is a powerful model but it has a hard time approximating multiplication and division. Adding multiplied / divided features is a powerful trick even for boosting.
  
* ### Prices: use fractional prices

  If we have a price, we can build an additional feature `fractional_price` - this feature can inform model about customer's price perception
  
  | Price         | Fractional price |
  | -------------:|-----------------:|
  | 2.49          | 0.49      |
  | 5.00          | 0.00      |  
  | 19.99         | 0.99      |   
  
* ### Text: using char n-grams
  
  Sometimes having char level n-grams can be cheaper than having all unique words from the dataset. Char n-grams can also help with handling previously unseen words (e.g. rare forms of words present in the training data).
  
* ### Text: word2vec vs Bag of Words

  Both methods pretty often lead to different results. Using both can be beneficial.
  
## Feature encoding

* ### Encoding categorical features

  * Alphabetical order: [R, B, Z] -> [2, 1, 3] (default in `sklearn.preprocessin.LabelEncoder`) (**tree-based methods**)

  * Order of appearance: [R, B, Z] -> [1, 2, 3] (default in `Pandas.factorize`) (**tree-based methods**)
  
  * Frequency of appearance: [R, B, Z] -> [.3, .47, .23] (can also be useful in **linear models**)
  
  ```python
  # Encode the feature - which is a fancy name of getting the feature's frequencies:
  encoding = data['Feature'].value_counts() / len(data.Feature)
  
  # Map your encoding to the feature:
  data['encoded'] = data.Feature.map(encoding)
  
  # Done :)
  ```
  
  * One-hot encoding (**linear, kNN, ANN**)
  
  * Interactions of categorical features 
  can also be useful for **linear** and **kNN**.
  
* ### Encoding ordinal features for linear models

  * *Polynomial contrasts* - use your original, quadratic and cubic predictors in the model to generalize monotonicity to non-linear monotonicities as well. Ispired by this ![thread](https://stats.stackexchange.com/questions/195246/how-to-handle-ordinal-categorical-variable-as-independent-variable) 
  
## EDA

* ### Explore fetures groups 

  * Based on **means**
  ```python
  df.mean().sort_values().plot(style='.')
  ```

