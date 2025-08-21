# Predicting Medical Costs with Linear Regression

## Background + Goal

Medical insurance companies provide coverage to customers based on their predicted yearly medical costs. For example, people under the age of 30 typically have lower insurance costs than people over the age of 60 because they seek less medical care throughout the year. Insurance companies can evaluate an individual's annual insurance premium based on many factors like age, sex, and smoking habits. 

The goal of this project is to build a linear regression model that predicts an individual’s yearly medical costs based on their background information. A successful model should explain at least 70% of the variability in annual expenses. Such a model could be used by ACME Inc. to estimate monthly premium charges for new customers.

## Can annual expenditure be predicted by a customer's age? (Simple Linear Model)

![image](https://github.com/catherinealeal/DP-MedicalInsurance/blob/main/images/SLMPlot.png)

With actual values in green and predicted values in purple, it is clear to see that a simple linear model using age as the predictor performs poorly in predicting individuals' annual medical costs. 

![image](https://github.com/catherinealeal/DP-MedicalInsurance/blob/main/images/res1.png)

If regressing on age was enough to capture the variability in annual expenses, the residuals would be evenly distributed around 0. However, the residuals are positively skewed, indicating the requirement for a more complex model. 

R-Squared of Simple Linear Model =  0.0894

**No, annual expenditure cannot be predicted by an individual's age alone.** With an R-squared of just 0.089, I can confidently conclude that age is not sufficient for predicting annual expenses. The model explains very little of the variability in medical costs and performs almost as poorly as the mean. 

## Are all 6 customer features sufficient for predicting yearly medical costs? (Multiple Linear Model)

![image](https://github.com/catherinealeal/DP-MedicalInsurance/blob/main/images/MLMPlot.png)

Again, actual values are in green and predicted values in purple. It is evident by this plot that incorporating all 6 features into the model greatly improved it's predictive power. The model seems to have captured much more variability in the data and much les resembles a simple mean prediction. 

![image](https://github.com/catherinealeal/DP-MedicalInsurance/blob/main/images/res2.png)

This residual plot looks much more promising, with values fairly evenly distributed around 0 with no clear pattern. 

R-Squared of Full Multiple Linear Model = 0.7498

**Using all 6 features in the regression model successfully explains more than 70% of the variability in annual medical costs.** In fact, the full multiple linear model explains almost 75% of the variability in expenses. Although this model is sufficient, I want to test the trade-off between model complexity and model fit to ensure ACME Inc. employs the optimal model for their company and customers. 

## Are all the predictors signifigantly contributing to the model? (Lasso Regression)

Lasso regression is a form of penalized regression used for variable selection because it adds an L1 penalty (the absolute value of the coefficients) to the loss function.
This penalty encourages sparsity, meaning it pushes the coefficients of less important variables all the way to zero. As a result, Lasso not only helps prevent overfitting but also performs automatic feature selection.

Since the coefficient for the feature 'sex' went to 0, I can conclude that it does not contribute signifigantly to the model and remove it as a predictor. 

**Missing one feature, the reduced model is slightly less complex than the original but still explains almost 75% of the variability in expenses.**

## Conclusion

- The final regression model is: $AnnualMedicalExpenses = 257.9*Age + 320.9*BMI + 476.9*NumChildren + 23799.6*Smoker - 98.0*Region - 11929.9$ where:
    - Smoker: 0 for no, 1 for yes
    - Region: 0 for northeast, 1 for southeast, 2 for southwest, 3 for northwest
- The expected monthly premium can be computed as: MonthlyPremium = AnnualMedicalExpenses / 12
- This model allows ACME Inc. to quickly estimate medical costs and assign premiums for new customers based on only two pieces of information: age and smoking status.
- Because the model explains more than 70% of the variation in annual expenses, ACME Inc. and their customers can be confident that the premiums are fair, data-driven, and reasonably accurate.

#### View the full project [here](https://github.com/catherinealeal/DP-MedicalInsurance/blob/main/InsuranceCostPrediction.ipynb)
