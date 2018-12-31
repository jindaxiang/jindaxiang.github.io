---
title: Machine_Learning_day_02
date: 2018-08-16 09:18:52
tags: [Daily]
categories: [Machine Learning]
---

# Step 1: Importing the required Libraries
These Two are essential libraries which we will import every time.
NumPy is a Library which contains Mathematical functions.
Pandas is the library used to import and manage the data sets.
# Step 2: Importing the Data Set
Data sets are generally available in .csv format. A CSV file stores tabular data in plain text. Each line of the file is a data record. We use the ==read_csv== mehtod of the pandas library to read a local CSV file as a dataframe. Then we make separate Matrix and Vector of the independent and dependent variables from the dataframe.
# Step 3: Handling the Missing Data
The data we get is rarely homogeneous. Data can be missing due to various reasons and needs to be handled so that it does not reduce the performance of our machine learning model. We can replace the missing data by the Mean or Median of the entire column. We use ==Imputer== class of ==sklearn.preprocessing== for this task.
# Step 4: Encoding Categorical Data
Categorical data are variables that contain label values rather than numeric vlaues. The number of possible values is often limited to a fixed set. Example values such as "Yes" and "No" can not be used in mathematical equations of the model so we need to encode these variables into numbers. To achieve this we import ==LabelEncoder== class from ==sklearn.preprocessing== library
# Step 5: Splitting the dataset into test set and training set
We make two partitions of dataset one for training the model called training set and other for testing the performance of the trained model called test set. The split is generally 80/20. We import ==train\_test\_split()== method of ==sklearn.crossvalidation== library.
# Step 6: Feature Scaling
Most of the machine learning algorithms use the Euclidean distance between two data points in their computations, features highly varying in magnitudes, units and range pose problems. High magnitudes features will weigh more in the distance calculations than featurs with low magnitudes. Done by Feature standardization or Z-score normalizaion. ==StandardScalar== of ==sklearn.preprocessing== is imported.