# Wellness Tourism Package: Development of strategies to identify and expand customer base
Developed a model to identify potential customers who will buy tourism packages and insights for optimizing market strategies

#### Skills used for this project: EDA, data preprocessing, customer profiling, random frest, XGBoost, Hyperparameter tuning using GridSearchCV, business recommendations

## Introduction
The 'Visit with us' company has a new product called "Wellness Tourism Package". The package will offer a path to the customer to increase their well-being by giving the ability to kick-start a healthy lifestyle, or enhance their current lifestyle, or assist in maintaining their current healthy lifestyle. The current aim is to expand the customer base by building a viable business model that includes the new product as a path forward.

Background: The company offered 5 tourism packages earlier: Basic, Standard, Deluxe, Super Deluxe, King. The marketing campaign contacted customers at random with no prior analysis. This resulted in 18% of customers buying the packages, however, the marketing cost was high.

## Objective
- Identifying potential customers who are likely to purchase the Wellness Tourism Package.
- Generating insights into the characteristics of the customers that would optimize the marketing team's strategies.

## EDA Excerpts: 
![image](https://user-images.githubusercontent.com/83994337/164950795-3966b9c9-4d16-478c-afc8-05265a79bdbb.png)
The range for MonthlyIncome is quite large - from 0 to 100,000. The peak is around 20,000 to 30,000. We can see a few outliers for the remaining graphs - these will be dealt with in the preprocessing section. For TypeofContact, Passport, OwnCar - the medians for whether the customers preferred a typeofContact or had a passport or Owned a car based on their monthlyIncome are not significantly different. For ProdTaken, on the basis of monthlyIncome, there is a slight difference in median. If we look at Designation, we can see that the median monthlyIncome is different between the Manager designation versus a VP type designation.

![image](https://user-images.githubusercontent.com/83994337/164950815-d308bbdc-f2f9-4471-9957-02ed5237c6b0.png)
- The NumberOfChildrenVisiting is strongly correlated with NumberOfPersonVisiting (0.61). This is likely due to the numbers of children visiting being included in the numbers of persons visiting. However, multicolinearity is not an issue as such for classification problems as it is for linear regression problems.
- There is moderate correlation between Age and MonthlyIncome (0.46) - meaning that customers who had higher monthly incomes belonged to a higher age group as well.
- There is some weak correlation between NumberOfChildrenVisiting and NumberOfFollowups, and between NumberOfPersonsVisiting and NumberOfFollowups as well (0.29 and 0.33). Also some weak correlation (0.26) between Passport and ProdTaken variables.

![image](https://user-images.githubusercontent.com/83994337/164950846-02b746df-cbee-4a5e-ba16-4416ed711555.png)

On the testing set, for accuracy - the model that gave the best accuracy was random forest estimator. However, accuracy is not the most important measure of performance as explained in the beginning of the model building section. For recall, the best model was bagging estimator, and the next best was random forest estimator. For precision, the weighted random forest classifier was the best performing model. For F1, the random forest estimator (the hypertuned) gave the best F1 score.
However, for the current problem of predicting which customer will buy a travel package, the recall and F1 are more important scores as compared to precision and accuracy. This is because we want to reduce the false positivies as much as possible. Thus, analyzing the above table - we can say that the random forest estimator (the hypertuned model) peformed best for the above testing set (80.7% F1, 71% recall).

![image](https://user-images.githubusercontent.com/83994337/164950861-7730fa0c-dfbc-45b2-8bea-591da4a67744.png)

Between the boosting models, the XGBoost gave the best train-test accuracy performance. For recall, the XGBoost tuned gave the best recall on the testing set (81%). For precision, the best model was XGBoost (88%), and for F1, the best model was XGBoost as well on the testing set (88%). Our most important measures are recall and F1 - so from boosting - the models that had a reasonable performance was the tuned XGBoost.
Between the bagging section and boosting section, the random forest estimator (recall = 71.3%, precision = 92.9%, F1 = 80.77% on testing set) compares well to the XGBoost tuned (recall = 81%, precision = 72%, F1 = 72%).
Overall, for an imbalanced data set - where only 18% of the data had ProdTaken = 1, influenced the models on how well they performed on recall and precision and F1.
If we consider recall to be most important measure, then XGBoost tuned gave a high metric for recall (81%). If both recall and F1 are considered to be most important measure, then the tuned random forest performed better since it had an F1 of 80.77%.

##Insights and recommendations
- Majority of the customer base is highly interested in tourism packages - given that 70.4% made a self enquiry about travel packages on their own. This indicates that if the right sort of travel package is offered to these customers, the likelihood that they will purchase a travel package is good.
- 82% of the customers who did a self enquiry and 78% of the customers who were contacted by the company did not purchase a tourism package. This indicates that either the packages did not appeal to the customers or they could not afford the travel packages.
- While Deluxe was the package that was pitched the most to customers, the Basic package was the one that was purchased most of the time. This indicates that there is a mismatch between what is being offered to the customer and what they actually want/or can afford.
- The model predictions gave importance to monthly income and age and duration of pitch - hence, the marketing team can target customers based on their income (higher income bracket should be targeted more often) and age (younger customers for basic package). In addition, the duration of pitch can also influence whether the customer will ultimately buy the package or not, so the marketing department should strategize on how to engage the customer for an optimum duration while pitching the package product to them.
- Overall, the potential to market a wellness tourism package is present - especially since the customer base is mostly manager designation or above (which involves long hours and stress, so a wellness package may seem attractive). However, since the customers prefer 3 star properties, and domestic locations, as well are in the younger age bracket - the wellness packages should incorporate these features into the product.
