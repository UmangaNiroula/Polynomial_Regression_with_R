# Elevator Pitch

This analysis focuses on understanding customer shopping behaviors from nearly 100,000 invoices across Istanbul shopping malls between 2021 and 2023. Using detailed customer data—including age, gender, purchase categories, payment methods, and spending patterns—we employed polynomial regression to model the relationship between these factors and sales outcomes, such as quantity sold.

Key insights emerged from time-series trends and distribution analyses, highlighting which age groups and categories dominate shopping mall transactions and how seasonal shifts influence purchase quantities and prices. Through correlation and scatter plots, we examined the strength of relationships between age, price, category, payment methods, and quantity. The results guided us to create and compare five regression models, each rigorously evaluated using metrics like Residual Sum of Squares (RSS), log-likelihood, AIC, and BIC.

Model 3 outperformed others, achieving the best fit without overcomplicating predictions. With further training and confidence interval estimation, this model has shown promise in accurately predicting sales trends. The analysis underscores actionable insights for shopping mall marketing strategies and inventory planning by aligning customer demographics and purchasing preferences.

### Language Used : R Programming Language

# Modeling Shopping Mall Dales Data using Polynomial Regression

1. Introduction

This report provides an overview of a customer shopping dataset, that is obtained from different shopping malls of Istanbul from year 2021 to 2023. The data includes information on nearly 100,000 invoices from various customers which is represented by the following figure
1. Further, there are various customer details included such as gender and age, which makes the understanding of shopping based on gender and age more understandable. Likewise, the dataset provided shows what customers are buying (category), how much they're buying (quantity) and how much they're spending (price). It will also examine how customers are paying (payment method) and when (invoice _date) and where (shopping_mall) they are making their purchases.

![2](https://github.com/user-attachments/assets/6ccf6586-b6a0-4154-8ca1-d0ab5526b855)

Moreover, the following figure is a summary of the dataset, as shown by the figure, we the length, class, and mode for the non-numerical columns such as “invoice_no”, “customer_id”, “category”, ”payment_method”, and many more. Similarly, there are numerical colums such as “age”, “quantity”, and “price” where the min, 1st quartile, median, mean, 3rd quartile, and max value can be seen (Thakur, 2024).

![3](https://github.com/user-attachments/assets/9a8ec0db-5f87-49cf-b7e9-533e87854380)

For further analysis, each of the columns were thoroughly checked for any missing value, the output is shown in the following figure 3. This is a very crucial process as it hinders with the process of analysis. If certain data are missing then the conclusion of the analysis will not be accurate. Hence, to make sure the accuracy of the analysis is top notch, we check for any anomaly in the dataset.

![4](https://github.com/user-attachments/assets/af0798d6-fe97-4bfa-8b9e-80f199b6344b)

Additionally, to check if the dataset consists of a standard value, we also check for the unique value in each of the columns, as shown in following figure 4. This will only select the unique value form the column, which we can understand that the values are standard across the dataset, which makes the process of analysis error free.

![5](https://github.com/user-attachments/assets/6572736e-20b7-4f6b-b6ff-95699c032d0f)

2. Preliminary Data Analysis
   
2.1. Time Series Plots

Time series plots are used to show the trend of various variables over time, in the following figure 5 and 6, the trends of age, category, price, payment method, and total quantity is used to show what kind of trends were observed with the time frame of invoice data.

In the following figure 5, we can see that none of the graph shows a strong upward or downwards trends. For example, for the age, it shows that during the first half of the invoice date, an age group above 50 shopped from mall, where are near to the end the age group has doped below 50. This information shows what kind of audience the shopping malls need to target (Montgomery et al, 2015).

Likewise, for category the first half contained very a smaller number of categories shopped where are near to the end more of those categories are being brought in a larger volume. Hence, this data shows the shopping mall to put more emphasis on the categories are they are selling more than ever.
Furthermore, talking about the price, it has not seen a dramatical upwards and downwards trends are others, which makes sense as prices are usually high during the initial phase of a particular year. Further, as the demand and supply slowly start to catch up, the price is adjusted and kept constant throughout the year, which can clearly be seen from the following figure 5 (Chatfield, 2016).

![6](https://github.com/user-attachments/assets/d796c184-de6b-41ae-b1b0-4eceb971adce)

The following figure 6 is another time-series plot showcasing total quantity of products sold by various shopping malls throughout 2021.0 to 2023.0. From 2021, the total quantity was 11000 plus when then seems to reach the highest in between 2021.5 and 2022.0. Further, except this sharp increase the graph shows a steadiness.

![7](https://github.com/user-attachments/assets/a7862976-603b-4240-9d81-d5fdb470021f)

2.2. Distribution for each Sales Data
The black curve line represents the density estimation of each variable in figure 7, 8, 9, 10, and 11. This curve line is used to represent how likely different variable (price, payment method, age, category, and quantity) values are within the dataset. Further, the curve is created using a statistical technique called Kernel Density Estimation. Likewise, each of the light blue bars represent the actual value of the variable which is divided into intervals that shows the frequency of the data point falling within an interval. Additionally, there are red lines along the x-axis which represents a rug plot, that provides a more descriptive view of distribution of each variable. It shows the cluster or the gaps between the variables (Hyndman et al, 2018). 

Moreover, in the following figure 7, the curve is higher in the left side of the x-axis, which is also true of the bar and the rug plot underneath the bar in red color. This suggests a possible skewness in the price distribution, meaning there are more data points with lower price compared to high price

![8](https://github.com/user-attachments/assets/c367c98d-6c62-4a0f-8649-4f0649713ea2)

Furthermore, from the following figure 8, we can see the density of the payment method, as shown in figure 4 there are three different types of payment methods: credit card, debit, and cash. As shown by the following figure, cash is the most used payment method, where the density is greater than 2.0. Similarly, following cash, credit cards are the next favorite payment type.

![9](https://github.com/user-attachments/assets/c8036475-ec81-44bc-87f9-9567d894df1b)

As shown in the following figure 9, we can see that customers form the age group 20 to 75 are the most active once. This figure appears to be right-skewed meaning there are more younger people than older ones. Similarly, the peak of the curve is somewhere between 20- 30 years old, showcasing that these are the age group that has frequently appeared in the dataset.

![10](https://github.com/user-attachments/assets/0d03fefd-9aae-4403-924f-23a2995a25cf)

The following figure 10 demonstrates the density of eight different categories that the customer shop in shopping mall. As shown, we can see that density is higher in clothing, hence a lot of customers go to the shopping malls for clothes; on the other hand, technology 12 and souvenir are the least bought items from the shopping mall. By this we can see the trend of customer preference in shopping malls.

![11](https://github.com/user-attachments/assets/0c39bc62-507a-49aa-acd6-b5a61f821742)

Likewise, the following figure is another density plot for quantity, from where we can see that the maximum number of quantities is 5 and minimum is 1. Further, from the looks of the graph, there are not much different between the customers that shop 1upto 5 items of product.

![12](https://github.com/user-attachments/assets/4ef45087-8c28-468d-b81a-367b90af95f9)

2.3. Correlation and Scatter Plots

This section is dedicated in showing the correlation of the input customer data with the output predicted sales quantity. For the customer data age, price, category, and payment method have been considered. Here we check the strength and direction of two variable turn by turn (Box et al, 2015). The following figure 12, shows the correlation between age and quantity, as shown by the figure it doesn’t explicitly describes a trend as there are horizontal blue lines which is the data points, meaning it shows the number of products brought by each customer of different age. Further the red line shows that it is the most common range “3” for various age groups to buy.

![13](https://github.com/user-attachments/assets/723290af-6728-4800-b00e-734bf10d1bc9)

Furthermore, there is a positive correlation between price and quantity in the following figure 13. This means that when the quantity increases the price also increase, which is what normally happens. However, under certain situation this might not be the criteria as there might be factors influencing both the variables. For example, if the product is new and trendy product then the price will be high regardless of the quantity. Another correlation graph can be seen in following figure 14 between category which is the x-axis and quantity, y-axis. There are all together 8 different category type as shown in the following graph. Further the blue dot represents the data point for each of the category type whereas the red line shows the average of each category brought which is 3.

![14](https://github.com/user-attachments/assets/b0971f3e-d8ab-4f8f-b3be-8d001e1dfa48)

Another correlation graph can be seen in following figure 14 between category which is the x-axis and quantity, y-axis. There are all together 8 different category type as shown in the following graph. Further the blue dot represents the data point for each of the category type whereas the red line shows the average of each category brought which is 3. The following figure 15 is another scatter plot graph showing the correlation between payment method and quantity, as shown in the following figure the blue dot represents the data point for each of the category type whereas the red line shows the average of each category brought which is 3.

![15](https://github.com/user-attachments/assets/15c4960b-ce71-4ea2-8d2c-e12d041c7e79)

3. Regression Modeling the Relationship Between Sales Data
   
3.1. Estimating Theta Hat Value

In this section of the report, random variable or estimator, often denoted as "θ," helps us understand various aspects of a distribution when we lack actual values. Further the value of "θ," can be multiple, as a result, to find the best fit model we can utilize least squares method. Least square method helps us to identify a line that is best fit as well as showcasing the relation between the independent and the dependent variables (Brooks et al, 1998). Hence, to find the least square we will use the following formula:

![16](https://github.com/user-attachments/assets/f0cd5eae-e4da-4190-ab74-3b78980d09e0)

Further, to find the least square, we first we arrange an input data and combine it with a constant, that are also called predictor variables. In this case we have used "age", "category", "price", and "payment method" as the predictor variables and "quantity" as the response variable. Doing so we obtained the following output which is shown by figure 16. From the following figure 16, we can identify the value of "θhat" for model 1 to be as follows:

![17](https://github.com/user-attachments/assets/cda919b5-b635-4990-9627-28a31b7d89fe)

Likewise, the following figure 17 is the output for value of "θhat" for model 2, which is:

![16value](https://github.com/user-attachments/assets/11528835-fa88-4305-9707-36a30c95b30f)

Furthermore, the following figure 18 is the output for value of "θhat" for model 3, which is:

![18](https://github.com/user-attachments/assets/fd517a0c-196d-4f89-a2fb-9cef45137d7b)

Similarly, the following figure 19 is the output for value of "θhat" for model 4, which is:

![19](https://github.com/user-attachments/assets/c7cb3e01-05e6-469c-b374-3d2eec76bb6b)

Finally, the following figure 20 is the output for value of "θhat" for model 5, which is:

![20](https://github.com/user-attachments/assets/866f4b27-073b-4640-ab53-ac9e5320c52d)

3.2. Computing Model Residual Sum of Squared Errors (RSS)

In this section, we check for the model’s RSS value which shows us how closely our estimates align with the real data. RSS is measured by the squared and mean difference between actual values and estimated values, which is the accuracy of the above mentioned 5 models. In the above-mentioned formula ‘i’ is the lower limit whose value is 1, ‘n’ is total number of data point. Likewise, ‘X i’ is the value that contains all possible input values, and ‘θ hat’ is the value obtained from the previous point for each of the five models. Further, following figure 21 shows the RSS value for each of the model (McElreath, 2015).

![21](https://github.com/user-attachments/assets/6d9e3a8e-9c83-4975-85a0-a856c1974f9d)

3.3. Calculation of Log-Likelihood Functions

Now, in the section, likelihood function will be calculated to observe how a set of parameters explains the observed data. In simpler word, it helps us to identify the actual scores if the guess about the distribution is correct. Now, instead of dealing with the likelihood function directly, we often use the log likelihood. It's like taking the log of a big number to make it easier to work with. The log likelihood still helps us find the best guess for the distribution of scores, but it's simpler to calculate and understand. Further, to calculate the likelihood, variance needs to be calculated initially. As in the following figure 22, the variance and the log-likelihood are calculated (Gelman et al, 2006). Moreover, for the variance and the log-likelihood we can create following tables.

![22](https://github.com/user-attachments/assets/83798d60-7d93-41c8-95b8-227965cbb7ac)

3.4. Calculation of AIC and BIC

AIC (Akaike Information Criterion) and BIC (Bayesian Information Criterion) are the calculation on whose basis models are compared and selected. They balance how well the model fits the data with how complicated it is. AIC looks at how well the model explains the data and how many variables it uses. BIC is similar, but it's stricter with how much it penalizes complexity. Both AIC and BIC help researchers pick the best model that explains the data well without being too complicated. that provides the best explanation of the data while using the fewest parameters, helping researchers make informed decisions about model selection and avoiding overfitting. Following figure 23 shows the output for AIC and BIC along with the number of parameters used (Hastie et al, 2009).

![23](https://github.com/user-attachments/assets/e1f5497a-89a1-4f5d-afbf-fd135f4bd7ee)

3.5. Analyzing Model Prediction Errors
The following figures 24, 25, 26, 27, and 28 compares the theoretical quantiles (expected value) with sample quantiles (observed value) for all of the five models. Further, the x-axis of the QQ plot represents the theoretical quantiles, and the y-axis represents the sample quantiles as shown in the figure. Here, if the points on the QQ plot falls close to the diagonal line then it signifies that the expected or theoretical value of the model matches the observed quantiles of the dataset, in simpler terms if the expected value has a close match with observed value, then it is considered to be a good fit. Sine a lot of experiment has been done with the model 1, 2, 4, and 5 don’t have a good fit as model 3, because in model 1, 2, 4 and 5 we can see that the points deviate significantly from the diagonal line. Nonetheless, for model 3 the points on the QQ plot fall close to a diagonal line.

![24](https://github.com/user-attachments/assets/3f893405-5e5d-4f35-9357-027f18437407)

![25](https://github.com/user-attachments/assets/48391234-124b-4041-b8d7-8139034c4780)

3.6. Selecting Optimal Regression Model

When selecting the ideal regression model, we want one that is just right not too basic, not too difficult, but fits the data nicely. We utilize a few tools to assist is making decisions. AIC and BIC are scores that indicate how good a model is. Lower scores indicate that the model matches the data better. We also look at residuals, which are the disparities between what our model predicts and what really happens. We want the differences to be minor. After comparing these scores and analyzing the residuals for each model, we conclude that Model 3 is the winner. It has the lowest scores and the smallest discrepancies between predicted and observed data. So, Model 3 is the greatest option for effectively explaining our facts without being overly convoluted. This strategy ensures that we select the appropriate model to fully comprehend our data.

3.7. Model Training, Testing, and Confidence Interval Estimation

In this section the division of the data is done into two groups: one for training the model and one for testing. Further, 70% of the data is used for training and 30% is set aside for testing, which is utilized to choose the best model from the training data, which was Model 3. This model is utilized to estimate a value known as "q", following that, estimated value is utilized to create predictions about the test data. Likewise, Residual Sum of Squares" (RSS)" is also calculated to see how well the forecasts matches the actual findings, interm allowing to observe how well the selected model fits the test data. Finally, confidence interval is calculated to demonstrate the accuracy of the model. This interval provides a range in which the real values of the parameters are likely to be, providing dependability to the selected model's predictions. Following figure 29 shows the model predictions and the 95% confidence intervals.

![27](https://github.com/user-attachments/assets/9bbf2cdb-8d04-403f-8737-855f4d241cfa)
