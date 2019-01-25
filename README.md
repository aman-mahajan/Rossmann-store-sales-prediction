# Rossmann-store-sales-prediction
A beginner's approach for [this](https://www.kaggle.com/c/rossmann-store-sales) problem.

## Problem: Rossmann Store Sales Prediction 
The objective is to predict the sales of various Rossmann stores for the next 6 weeks.

## Approach:
Even though it is a time series forecasting problem, basic timeseries forecasting methods like ARMA, ARIMA are not used because we have many features to consider, many of them being categorical.
Xgboost is used here for this problem of regression.
File Description: Code in rossmann.py and result in results.csv

### Data preparation: 
1.	Reading the files : train.csv, test.csv and store.csv.
2.	Merging the store.csv with train.csv and test.csv to aggregate all the training data into one.
3.	Building and cleaning features:
   *	Removing NaNs.
   *	Label encoding the categorical features like StoreType, Assortment, StateHoliday.
   *	Extracting day, month, year from the date.
   *	Creating feature “CompetitionOpen” which gives the number of months since a competition opened.
   *	Creating feature “PromoOpen” which gives the number of months promotion opened.
   *	Creating feature “IsPromoMonth” which indicates whether the sale is in promo month or not.

## Regression Model:
Xgboost(Extreme Gradient Boosting) is a type of gradient boosting machine that uses a more regularized model to control overfitting.
1.	Setting parameters of the xgb model: Objective would be reg:linear for linear regression. Booster is gbtree as we are using the gradient boosting trees for our model.
2.	Splitting the training data into training and validation.
3.	Taking log of the sales(ie the target variable y) to scale down the values since the regularization term in the loss function includes the l2 norm (square) of the weights of the leaves of the trees. Since the leaf weights are basically the target values, having big numbers would reduce the predictive power of the model.
4.	Training the model with RMSPE(root mean square percentage error) as the error (as it is used in the competition to calculate the score).
5.	 Predicting the test cases and sorting the result by Id to print the result in the output file results.csv for submission in Kaggle.

## Results:
#### RMSPE-training = 0.083653
#### RMSPE-validation= 0.096479
