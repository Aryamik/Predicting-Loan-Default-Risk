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

![Correlation Matrix](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Correlation%20Matrix.PNG)

*Figure 1: Correlation Matrix of all Numerical Variables*

Based on the correlation matrix generated above, none of the numerical variables seem to be highly correlated to each other. 

## Training the Classification Models
### Logistic Regression (Stepwise)

![Logistic Regression](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Logistic%20Regression.PNG)

*Figure 2: Logistic Regression Model*

Using 'Credit Application Result' as the target variable, 'Account Balance', 'Purpose', 'Payment Status of Previous Credit', 'Length of Current Employment', 'Installment per Cent' and 'Credit Amount' are the most significant predictive variables.

### Decision Tree

![Decision Tree](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Decision%20Tree.PNG)

*Figure 3: Decision Tree*

![Summary of Decision Tree](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Decision%20Tree%20Summary.PNG)

*Figure 4: Summary of Decision Tree*

Using 'Credit Application Result' as the target variable, 'Account Balance', 'Value Savings Stocks' and 'Duration of Credit Month' are the top 3 most important variables.

### Forest Model

![Forest Model](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Forest%20Model.PNG)

*Figure 5: Forest Model*

![Forest Model](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Variable%20Importance%20Plot.PNG)

*Figure 6: Variable Importance Plot*

Using 'Credit Application Result' as the target variable, 'Credit Amount', 'Age Years' and 'Duration of Credit Month' are the 3 most important variables

### Boosted Model

![Forest Model](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Boosted%20Model.PNG)

*Figure 7: Boosted Model*

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Variable%20Importance%20Plot%20for%20Forest%20Model.PNG)  ![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Variable%20Importance%20Plot.PNG)

*Figure 8: Boosted Model Summary*

Using Credit Application Result as the target variable, Credit Amount, Account Balance and Duration of Credit Month are the 3 most important variables.

## Model Comparison

![Model Comparison](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Model%20Comparison%20Report.PNG)

*Figure 9: Model Comparison*

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Confusion%20Matrices.PNG)

*Figure 10: Confusion Matrices*

Based on the model comparison report above, the overall accuracy for
* Logistic Stepwise model is 76%
* Decision Tree is 74.67%
* Forest Model is 80%
* Boosted Model is 78.67% 

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Gain%20Chart.PNG)

*Figure 11: Gain Chart*

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Lift%20Curve.PNG)

*Figure 12: Lift Curve*

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Precision%20and%20Recall%20Curve.PNG)

*Figure 13: Precision and Recall Curve*

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/ROC%20Curve.PNG)

*Figure 14: ROC Curve*


Forest model should be chosen as it offers the highest accuracy of 80% against validation set.
The Forest model reaches the positive prediction value at the fastest rate. This is crucial in avoiding lending money to customers with high probability of defaulting while ensuring opportunities are not overlooked by not loaning to creditworthy customers.


We will then use this Forest Model to identify the number of creditworthy customers in the ‘Customers to Score’ dataset. 

## Results
Ultimately we get a total of 405 customers out of 500 who are creditworthy after accounting for other variables. 

## Alteryx Workflows

![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Prediciting%20Default%20Risk%20Alteryx%20Workflow.PNG)

*Figure 15: Predicting Default Risk Workflow*


![](https://raw.githubusercontent.com/Aryamik/Predicting-Loan-Default-Risk/master/Images/Scoring%20Customers%20Alteryx%20Workflow.PNG)

*Figure 16: Scoring Customers Workflow*

