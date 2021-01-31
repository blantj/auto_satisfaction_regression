# Auto Satisfaction Regression
## Introduction
I set out to construct a model in sklearn and then model the same data using Microsoft Azure’s automl tool in order to get a better understanding of the capabilities of auto machine learning tools. I utilized a Consumer Reports auto satisfaction dataset that modeled overall auto satisfaction score based on satisfaction scores for different aspects of the vehicle. The top performing automl model, Voting Ensemble, had an RMSE of .85 and an MAE of .65. This slightly underperformed the top performing model that was manually created in Sklearn, Support Vector Regression, which had an RMSE of .84 and MAE of .64.

## Obtain Data
For this project, I decided to use a simple dataset in order to first test automl under favorable circumstances. I leveraged csv form Consumer Reports owner satisfaction ratings by model I had previously scraped. My modeling goal was to perform regression in order to determine how owner satisfaction ratings for aspects of a vehicle, such as driving experience or comfort, influence their overall satisfaction rating for that vehicle. The scraped dataset included 231 data-points across 5 variables.

## Scrub Data

In order to scrub to the dataset, I first dropped the 60 datapoints that were missing four of the five variables. After dropping these points there were no more missing datapoints. I next built an Isolation Forest model that identified the five greatest outliers within the dataset. All of these datapoints were within the regular distribution of the datapoints, so I determined that there were no outlier datapoints that needed to be fixed. After scrubbing, I was left with 171 datapoints across 4 features. 

## Explore Data

In order to contextualize the subsequent model performance, I graphed the distribution of the Overall Owner Satisfaction Score dependent variable. The scores ranged from 1 to 5 with a mean of 3.5 and a standard deviation of 1.1. The distribution had a leftward skew around the median/mode of 4. I also plotted the relationship between each feature and the dependent variable, which confirmed a linear relationship and the usability of these features for linear regression models.

## Model Data

Before modeling, I first standardized the data using a standard scaler. All three models that I built, Linear Regression, Elastic Net Regression and Support Vector Regression modestly outperformed the baseline model RMSE of 1.14 and MAE of .98. The top performing model was Support Vector Regression with an RMSE of .84 and an MAE of .64. Combined these models took about 5 minutes to gridsearch and run.

For the automl modeling, I provisioned a single machine with standard performance to perform 20 minutes worth of machine learning across the 12 available regression models in azure and 4 forms of data scaling. Within the allotted time limit, automl constructed 21 models across 6 model types and 4 methods of scaling before constructing 2 final ensemble models. Had I provisioned additional computing power or time, automl could have constructed significantly more models.

## Analyze Results

The top performing automl model was a Voting Ensemble. This had an RMSE of .85 and an MAE of .65, which outperformed Linear Regression and Elastic Net Regression but under-performed Support Vector Regression by a bit. Microsoft Azure automl does not yet offer Support Vector Regression, so automl outperformed all comparable models that I built but failed to outperform my top performing model for which it did not build a model of the same type.

# Github Files
[Modeling.ipynb](https://github.com/blantj/auto_satisfaction_regression/blob/main/modeling.ipynb) :  Auto Satisfaction Regression Modeling

# Sources
Kaggle: https://www.consumerreports.org/cro/index.htm
