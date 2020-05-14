# Predicting Loan Default Risk
Default risk, also called default probability, is the likelihood that a borrower fails to make full and timely payments of principal and interest, according to the terms of the debt security involved. Together with loss severity, default risk is one of the two components of credit risk. These days, when building credit risk models, one of the most important activities performed by banks is to predict the probability of default (PD). When we look at credit scores, such as FICO for customers, they typically imply a certain probability of default. This is an important factor considered by lenders while approving or disapproving your loan. Banks employ a variety of binary and non-binary classification models such as logistic regression, decision trees, forest models and boosted models to predict the probability of default. 

In this project, I will use a series of classification models in Alteryx to figure out the best model to evaluate the creditworthiness of 500 new applicants

## Exploratory Data Analysis (EDA)
After loading the 'Credit Data Training' dataset, as a first step, we will perform an exploratory data analysis (EDA) to identify any missing data and low variability fields using Field Summary Tool. 

As a first step, we will perform an exploratory data analysis (EDA) to identify any missing data and low variability fields using Field Summary Tool. 
‘Foreign Worker’, ‘Guarantors’, and ‘No of Dependents’ show low variability where more than 80% of the data skewed towards one data. These variables should be removed in order not to skew our analysis results.

‘Duration in Current Address’ has around 69% missing data and should be removed. While ‘Age Years’ has 2% missing data, it would be appropriate to impute the missing data with the median age. Here Median age is used instead of mean as the data is skewed to the left as shown below. Additionally, ‘Occupation’ and ‘Concurrent Credits’ both have one value
In addition, Concurrent Credits and Occupation has one value while 

Finally, ‘Telephone’ should also be removed as it is irrelevant in predicting default risk of customers.

Next we will perform an association analysis on the numerical variables and ensure that there are no variables which are highly correlated with each other ( a correlation of higher than 0.7).

Based on the confusion matrix generate above, none of the numerical variables are highly correlated to each other. 

## Training the Classification Models
### Logistic Regression (Stepwise)



Using 'Credit Application Result' as the target variable, 'Account Balance', 'Purpose', 'Payment Status of Previous Credit', 'Length of Current Employment', 'Installment per Cent' and 'Credit Amount' are the most significant predictive variables.

### Decision Tree



Using 'Credit Application Result' as the target variable, 'Account Balance', 'Value Savings Stocks' and 'Duration of Credit Month' are the top 3 most important variables.

### Forest Model


Using 'Credit Application Result' as the target variable, 'Credit Amount', 'Age Years' and 'Duration of Credit Month' are the 3 most important variables

### Boosted Model


Using Credit Application Result as the target variable, Credit Amount, Account Balance and Duration of Credit Month are the 3 most important variables.

## Model Comparison


Based on the model comparison report above, the overall accuracy for
* Logistic Stepwise model is 76%
* Decision Tree is 74.67%
* Forest Model is 80%
* Boosted Model is 78.67% 

Forest model should be chosen as it offers the highest accuracy of 80% against validation set.
The Forest model reaches the positive prediction value at the fastest rate. This is crucial in avoiding lending money to customers with high probability of defaulting while ensuring opportunities are not overlooked by not loaning to creditworthy customers.


We will then use this Forest Model to identify the number of creditworthy customers in the ‘Customers to Score’ dataset. 

## Results
Ultimately we get a total of 405 customers out of 500 who are creditworthy after accounting for other variables. 

