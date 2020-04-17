# Telco Customer Churn

![Churn Banner](https://miro.medium.com/max/1400/1*k0aH2ikjVKpXNOIDFKXdTg.png) 

Customer churn, also known as customer attrition, occurs when customers stopped using a company's product or service during a certain time frame. A telephone companies is interested in identifying segments of these customers because the price of acquisition for a new customer is greater than retaining an existing one.Therefore, they would like a churn prediction model to proactively engage the customers a risk of churning with special offers to prevent them from leaving.

---
## Table of Content
1. [ Data ](#data)
2. [ Basic Date Information ](#Information)
3. [ Data Cleansing ](#Cleansing)
4. [ Exploratory Data Analysis ](#Analysis)
5. [ Creating a Model ](#model)
6. [ Conclusion ](#Conclusion)

---
<a name="data"></a>
## 1. Data

The dataset is available on Kaggle: [Telco-Customer-Churn](https://www.kaggle.com/blastchar/telco-customer-churn)

The dataframe is composed of 7,043 rows each representing a customer and 21 features

#### Data Dictionary 

* customerID: customer ID
* gender: whether the customer is a male or a female
* SeniorCitizen: whether the customer is a senior citizen or not (1, 0)
* Partner: whether the customer has a partner or not (Yes, No)
* Dependents: whether the customer has dependents or not (Yes, No)
* tenure: number of months the customer has stayed with the company
* PhoneService: whether the customer has a phone service or not (Yes, No)
* MultipleLines: whether the customer has multiple lines or not (Yes, No, No phone service)
* InternetService: customer’s internet service provider (DSL, Fiber optic, No)
* OnlineSecurity: whether the customer has online security or not (Yes, No, No internet service)
* OnlineBackup: whether the customer has online backup or not (Yes, No, No internet service)
* DeviceProtection: whether the customer has device protection or not (Yes, No, No internet service)
* TechSupport: whether the customer has tech support or not (Yes, No, No internet service)
* StreamingTV: whether the customer has streaming TV or not (Yes, No, No internet service)
* StreamingMovies: whether the customer has streaming movies or not (Yes, No, No internet service)
* Contract: the contract term of the customer (Month-to-month, One year, Two year)
* PaperlessBilling: whether the customer has paperless billing or not (Yes, No)
* PaymentMethod: the customer’s payment method (Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic))
* MonthlyCharges: the amount charged to the customer monthly
* TotalCharges: the total amount charged to the customer
* Churn: whether the customer churned or not (Yes or No)

---
<a name="Information"></a>
## 2. Basic Date Information

This section will provide basic informtion about the data. 

![describe](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/describe.png)

In the table above, we can notice that we have no missing values, however, most of the features are categorical therefore we will have to manipulate them before running our model

---
<a name="Cleansing"></a>
## 3. Data Cleansing

There are 11 rows that have TotalCharges set to " ", which explain the reason why it is set as object. All of these customers are new customers that have not yet transacted with the company but are already subscribed therefore we converted the TotalCharges to zero.

Finally, we check that the dataset does not contain any duplicated rows or customer IDs.

![Duplicated](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Duplicated.png)

---
<a name="Analysis"></a>
## 4. Exploratory Data Analysis

#### Overview of the churn

![customerID](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/customerID.png)

27% of the customers in our dataset have churned.

### 4.1 Categorical Data

#### Gendre

![churn by Gender](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20Gender.png)
![Percentage of churn by Gender](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20Gender.png)

The split between male and female is almost excatly 50/50. This feature does not seem to have significance when it comes to predicting the churn.

#### Senior Citizen

![churn by SeniorCitizen](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20SeniorCitizen.png)
![Percentage of churn by SeniorCitizen](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20SeniorCitizen.png)

From the 7,043 customers in the dataset, senior citizen are 1,042, which represent 26% of the total customers. However, senior citizen seem more likely to churn as 42% have cancelled their subscription compare with 24% for the non senior citizen.

#### Partner

![churn by Partner](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20Partner.png)
![Percentage of churn by Partner](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20Partner.png)

There are roughly the same number of customers single and with partner. However, there is a noticeable difference in the churn as 20% of the customers with partners unsubscribe compared with 33% of the single customes.

#### Dependents

![churn by Dependents](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20Dependents.png)
![Percentage of churn by Dependents](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20Dependents.png)

30% of the customers in the dataset have dependants, 16% of these customers have churned. This represents almost half of the churn rate of the the customers that do not have dependants (31% churn).

#### Phone Service

![churn by PhoneService](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20PhoneService.png)
![Percentage of churn by PhoneService](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20PhoneService.png)

The customers subscribed to the phone service represents 90% of the dataset, however when looking at the percentage churn there is no significant differences between the two sets.

#### Multiple Lines

![churn by MultipleLines](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20MultipleLines.png)
![Percentage of churn by MultipleLines](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20MultipleLines.png)

There does no appear to be a difference in behaviour between customers with only one line and those that have none as both of these groups have a churn rate of 25%. However, the set of customers having multiple lines have a churn rate of 29%.

#### Internet Service

![churn by InternetService](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20InternetService.png)
![Percentage of churn by InternetService](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20InternetService.png)

There are noticeable differences in churn between the three differnt groups. Customers with the fiber optic have the biggest churn rate with 41%, Digital Subscriber Line (DSL) customers' churn rate is 19% and finally customers who do not have internet have a churn rate of 7%.

#### Online Security

![churn by OnlineSecurity](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20OnlineSecurity.png)
![Percentage of churn by OnlineSecurity](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20OnlineSecurity.png)

As showed the previous graph the customers that do not have internet as part of their subscription have a 7% churn rate as it is the same group of customers. Although this group represents the samllest set of customers, they seem to be the most loyal.

Customers without online security as part of their subscription have a churn rate of 42% compared with 15% for those that have the security service included.

#### Online Backup

![churn by OnlineBackup](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20OnlineBackup.png)
![Percentage of churn by OnlineBackup](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20OnlineBackup.png)

Customers without online backup represent 44% of the total customers while the ones with online backup represent 27% of the total customers (the rest being customers without internet service). The churn rate for customer without online backup is 40% compared with 22% for those that have an online backup which is 18 point percentage lower.

#### Device Protection

![churn by DeviceProtection](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20DeviceProtection.png)
![Percentage of churn by DeviceProtection](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20DeviceProtection.png)

Customers without a device protection represent 44% of the total customers while the ones with device protection represent 34% of the total customers (the rest being customers without internet service). The churn rate for customer without online backup is 39% compared with 23% for those that have an online backup which is 16 point percentage lower.

#### Tech Support

![churn by TechSupport](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20TechSupport.png)
![Percentage of churn by TechSupport](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20TechSupport.png)

Customers without a tech support represent almost half (49%) of the total customers while the ones with tech support represent 29% of the total customers (the rest being customers without internet service). The churn rate for customer without online backup is 41% compared with 15% for those that have an online backup which is 26 point percentage lower. There seems to be a significant difference in behaviour between customers with and without tech support.

#### Streaming TV

![churn by StreamingTV](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20StreamingTV.png)
![Percentage of churn by StreamingTV](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20StreamingTV.png)

Customers without a tv streaming service represent 40% of the total customers while the ones with tv streaming service represent 38% of the total customers (the rest being customers without internet service). The churn rate for these two groups is 33% and 30% respectively.There does not seems to be a significant difference in behaviour between customers with and without tv streaming service.

#### Streaming Movies

![churn by StreamingMovies](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20StreamingMovies.png)
![Percentage of churn by StreamingMovies](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20StreamingMovies.png)

Customers without a movies streaming service represent 40% of the total customers while the ones with movies streaming service represent 39% of the total customers (the rest being customers without internet service). The churn rate for these two groups is 33% and 30% respectively.There does not seems to be a significant difference in behaviour between customers with and without movies streaming service.

#### Contract

![churn by Contract](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20Contract.png)
![Percentage of churn by Contract](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20Contract.png)

Customers with month-to-month rolling contracts represents the majority of the customers, 55%, one year contracts represent 21% of the dataset and two years contract represent 24% of the total customers. The longer the customers contract last for the less likely they are to churn. Thus, rolling contracts have the highest churn rate with 43% compared with 11% for the one year contract and only 3% for the two years contract. Therefore, there is a significant difference in behaviour between customers depending on the period they are locked in their contract.

#### Paperless Billing

![Percentage of churn by PaperlessBilling](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20PaperlessBilling.png)
![Percentage of churn by PaperlessBilling](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20PaperlessBilling.png)

Paperless billing represents 59% of the total customers billing system but has a greater churn rate with 34% compared with 16% for custumers that have paper bill. There is a significant difference in behaviour between customers that are paperless compared with paper billing.

#### Payment Method

![churn by PaymentMethod](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20PaymentMethod.png)
![Percentage of churn by PaymentMethod](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20PaymentMethod.png)

* Electronic check is the most common form of payments with 33% of the total customers using this method. However it is also the methode that has the highest churn with 45%
* Mailed check represents 23% of the total customers method of payments and has a churn rate of 19%
* Bank transfer (automatic) represents 22% of the total customers method of payments and has a churn rate of 17%
* Credit card (automatic) represents 22% of the total customers method of payments and has a churn rate of 15%

There seems to be a difference in behaviour between customers depending the method of payment they prefer.

### 4.2 Numerical Data

#### Tenure

![Customers distribution by tenure](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Customers%20distribution%20by%20tenure.png)
![churn by tenure](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20tenure.png)
![Percentage of churn by tenure](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20tenure.png)

Customers have on average a tenure of 32 months, most of the customers stay between 9 and 55 months. The first month of subscription seems to be the high risk month with over 50% of the churn. It seems that the longer the customer stay subscribe the less likely they are to leave in the future.

#### Monthly Charges

![Customers distribution by MonthlyCharges](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Customers%20distribution%20by%20MonthlyCharges.png)

The average monthly charge is £64.76, most of the customers are paying between £35.50 and £89.85 a month.

![churn by MonthlyChargesGroups](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20MonthlyChargesGroups.png)
![Percentage of churn by MonthlyChargesGroups](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20MonthlyChargesGroups.png)

* Less than £35 represents 25% of the total customers monthly payments and has a churn rate of 11%
* 14% of the customers pay monthly between £35 and £55, their churn rate is 28%
* 12% of the customers pay monthly between £56 and £70, their churn rate is 22%
* 26% of the customers pay monthly between £71 and £90, their churn rate is 37%
* 23% of the customers pay monthly more than £90, their churn rate is 33%

There seems to be a positive relationship between the churn rate and the monthly charges

#### Total Charges

![Customers distribution by TotalCharges](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Customers%20distribution%20by%20TotalCharges.png)
![churn by TotalChargesGroups](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/churn%20by%20TotalChargesGroups.png)
![Percentage of churn by TotalChargesGroups](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Percentage%20of%20churn%20by%20TotalChargesGroups.png)

* 29% of the customers have their total charges under £500, their churn rate is 41%
* 13% of the customers have their total charges between £500 and £1000, their churn rate is 27%
* 18% of the customers have their total charges between £1001 and £2000, their churn rate is 21%
* 17% of the customers have their total charges between £2001 and £4000, their churn rate is 24%
* 23% of the customers have their total charges over £4000, their churn rate is 15%

There seems to be a positive relationship between the churn rate and the monthly charges

---
<a name="model"></a>
## 5. Creating a Model

### 5.1 Logistic Regression

We used a logistic regression to predict wether a customer is going churn or remain.

![accuracy](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/accuracy.png)

We achived 80% accuracy with the logistic regression. However, in order to assess of the performance of the classification model we used a confusion matrix.

![confusion matrix](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/confusion%20matrix.png)

Looking at the confusion matrix, we have 1,416 (1,156 + 260) correctly classified customers and 345 (123 + 222) incorrect predictions. 

![ROC curve](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/ROC%20curve.png)

The above graph shows that the logistic regression model stays far away for the ROC Curve, representing the random classifier.

### 5.2 Random Forest

We used the random forest algoritm in order to test if this would provide a better prediction

![Accuracy of random forest](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Accuracy%20of%20random%20forest.png)

We then created a graph to plot the level of importance of each of the features in predicting the customer churn.

![Feature Importance](https://github.com/mriffaud/Telco-Customer-Churn/blob/master/images/Feature%20Importance.png)

The top four features in predicting the customers churn are the type of contract, the online security, the tenure and the tech support.

---
<a name="Conclusion"></a>
## 6. Conclusion

The logistic performs better in predicting the customer churn with 80% accuracy. The confusion matrix shows that 222 customers were predicted to stay members when they have in fact churned, this mean these customers would not be contacted to receive incentive in order to retain them. This figure is the one the telephone company should focus on bringing as close as possible to zero.

We also have 123 customers classified as churning who they are not, this mean that the telephone company may spend money offering discounted price to customers that did not intend to leave.




