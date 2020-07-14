# Fraud detection for GE Aviation

## Project Overview 
Founded by Thomas Edison, GE has a long history of involving in patent conflicts since the famous “Current war” with Westinghouse, thus it has been GE’s tradition to protect the Intellectual Property. The cost of a single IP leakage can be as high as $10million. Currently the company has rule based system with a special team of 10 analysts to monitor the IP leakage risks manually and classify the alerts as high or low risk. It has been very heavy work since they have to check nearly 100,000 incidents per year, thus the aim of our project is to build a more robust ML models for protection of IP and Fraud Detection that can save the analyst from heavy work while not miss any high risk incidents.

The rules are activated dependent on the activities and threshold of the cumulative heat score for an employee which fires an alert( atomic and heat).These are afterwards analyzed by the team of analyst and classified as TP/DE, TP/HIGH, TP/LOW or FP. 

## Goals

In the analysis, I have focused on three types of alerts: Atomic alerts TP high, TP notable(high and low risk alerts) and Heat Alerts(high and low); I would design the models for predicting each of these types that reduce the analysts manual work as much as possible whilst minimize the chance of missing any high risky alerts. 

## Approach

1. To get an overview, first I separated the data in 4 sets (atomic, heat daily, heat monthly, heat weekly) and then performed the Exploratory Data Analysis and Unsupervised Learning using k means to find out the significant factors that would impact the accuracy of current system.
2. Based on my findings I then chose Logistic regression, Naïve Bayes,Random Forest and XGBoost to perform the predictive analysis. 
3. Improved the recall and reduced the number of False Positives by varying the model probability threshold.
4. Finally, constructed a budget constrain analysis to find the best threshold value to minimize the cost of missing risky alerts(FN) and the labor cost of analysts(FP).

## Insights
1. Ensemble methods with probability threshold at .01 were able to detect 99% of the risky alerts correctly while reducing the Analyst efforts (False Positive count) by 53% and is cost-effective.

2. From the model Feature importance and tenure bar chart we can state that tenure is an important feature and employees with tenure greater than 40 years (near retirement) are susceptible to suspicious activities.

3. From the clustering output, we can see that the Employee details like GE_hire_date, Job_Function, Function_Name, Person_status, and Country, are playing a major role in classifying High-Risk alerts and hence the employee information should be merged with the current system. Moreover, HRU is another important factor and maybe we should look into None category and assign it a Higher Risk Unit.

**Value Proposition**

There are 10 analysts in the IP detective team and they have to review manually about 100,000 incidents per year, that is about 270 cases per day, in addition to the current labor cost $1M (10 x 100k), since it is the human work cannot be 100% perfect, missing TP highs do exist: according to my calculation, half of the TP high were discovered by re-checking the incidents, so the first time accuracy for TP high is only 50%, let’s assume that after 2 or 3 rounds of re-checking and reclassification, still 10% of the TP high were missed: that is incidents missed (in 2018: around 500 TP high were discovered). So, the expecting cost of current system is $51 million

**Financial Analysis and Cost model**
1. The missing TP highs(False Negative) from my predictive models at probablity threshold .01 are about 22 alerts that would be missed, so for this part the potential cost would be about $22 million; 
2. The labor cost for reviewing false negative and false positive alerts. The model has generated 89813 incidents as False positived which needs to be reviewed bt the analyst which is 50% less than the current count 190404 of incidents being reviwed by the analyst.

So, the total cost of my ML based model is around $22 millions plus the labor cost reduced by 50%.

**Comparison with the existing model**
Existing System | Proposed Model
--------------- | --------------
Rule Based Static System | Dynamic system based on the Ensemble Machine Learning algorithm
Produced lot of False Positive, adding to the work of Analyst | Reduced the Count of FP by 53%, saving a lot of time for the Analyst.
Doesn’t Consider Employee Details and adding more data is complex task. | Can be easily retrained by adding more data and features.
Analyst manually must check all the alerts, thus susceptible to human error. | Automated process for classifying alerts, less prone to errors.

