---
title: Machine_Learning_day_03
date: 2018-08-19 09:18:52
tags: [Daily]
categories: [Machine Learning]
---

# Multiple Linear Regression
Multiple linear regression attempts to model the relationship between two or more features and a response by fitting a linear equation to observed data. The steps to perform multiple linear regression are almost similar to that of simple linear regerssion. The difference lies in the evaluation. You can use it to find out which factor has the highest impact on the predicted output and how different variables relate to the each other.

# Assumptions
For a successful regression analysis, it is essential to validate these assumptions.
1. Linearity: The relationship between dependent and independent variables should be Linear.
2. Homoscedasticity(constant varicance) of the errors should be maintained.
3. Multivariate Normality: Multiple regression assumes that the residuals are normally distributed.
4. Lack of Multicollinearity: It is assumed that there is little or no multicollinearity in the data. Multicollinearity occurs when features(or independent variables) are not independent of each other.


# Note
Having too many variables could potentially cause our model to become less accurate, especially if certain variables have no effect on the outcome or have a significant effect on other variables. There are various methods to select the appropriate variable like -
1. Forward Selection
2. Backward Elimination
3. Bi-directional Comparision

# Dummy Variables
Using categorical data in Multiple Regression Models is a powerful method to include non-numeric data types into a regression model.
Categorical data refers to data values which represent categories - data values with a fixed and unordered number of values, for instance, gender(male/female). In a regression model, these values can be reepresented by dummy variables - variables containing values such as 1 or 0 representing the presence or absence of the categorical value.

# Dummy variable Trap
The Dummy Variable trap is a scenario in which two or more variables are highly correlated; in simple terms, one variable can be predicted from the others. Intuitively, there is a duplicate category: if we dropped the male category it is inherently defined in the female category(zero female value indicate male, and vice-verse).
The solution to the dummy variable trap is to drop one of the categorical variables - if there are m number of categories, use `$m-1$` in the model, the value left out can be thought of as the reference value. `$y=b_{0} + b_{1}x_{1} + b_{2}x_{2} + b_{3}D_{1}$`

# Preprocess the data
- Import the Libraries.
- Import the DataSet.
- Check for Missing Data.
- Encode Categorical Data.
- Make Dummy Variables if necessary and avoid dummy variable trap.
- Feature Scaling will be taken care by the Library we will use for Simple Linear Regerssion Model.
- Fitting our model to the training set
This step is exactly the same as for simple linear regression.
To fit the dataset into the model we will use ==LinearRegression== class from ==sklearn.linear_model== library. Then we make an object regressor of LinearRegression Class. Now we will fit the regressor object into our dataset using ==fit()== method of LinearRegression Class.

# Predicting the test results
Now we will predict the observations from our test set. We will save the output in a vector `$Y_{pred}$`. To predict the result we use ==predict()== method of LinearRegression Class on the regressor we trained in the previous step.
