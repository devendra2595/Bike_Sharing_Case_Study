# Bike_Sharing_Case_Study
# Problem Statement:

A US bike-sharing provider `BoomBikes` has a daily dataset on the rental bikes based on various environmental and seasonal settings. It wishes to use this data to understand the factors affecting the demand for these shared bikes in the American market and come up with a mindful business plan to be able to accelerate its revenue as soon as the ongoing lockdown due to corona pandemic comes to an end.

Essentially, the company wants to know —
- Which variables are significant in predicting the demand for shared bikes.
- How well those variables describe the bike demands

**So interpretation is important!**

# Libraries Used
- numpy
- pandas
- matplotlib
- seaborn
- statsmodels
- sklearn
- 
# The solution is divided into the following sections: 

1) Data understanding and Exploration
2) Data Analysis and Visualisation 
3) Data preparation
4) Model building and evaluation
5) Verification of Linear Regression Assumptions
6) Prediction on Test Set
7) Interpretation of model
8) Conclusion and recommendations


# 1) Data understanding and Exploration :
Read and understood the data.
- The data was from 1/1/2018 to 31/12/2019.
- Some of the variables were label encoded, e.g.'mnth','weekday', 'Season' variable had 1,2,3 & 4 instead of actual season names.
So, to avoid their misinterpretation, converted them back to their original category name and changed them to categorical datatype.

# 2) Data Analysis and Visualisation
- Univariate Numerical: 'temp','atemp','hum','windspeed','casual','registered','cnt'. Most of the variable were normally distributed with 'temp' and 'atemp' showing obvious signs of multicollinearity.
  
- Bivariate (Numerical) : Heatmap
- 
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/c45a5bbb-1fd8-4881-a89c-e4fe7441ca0a)
  
Correlation of Count('cnt') with independent variables:
- Count('cnt') is highly (positively) correlated with 'casual' and 'registered' and further it is with 'atemp'.
- We can clearly understand the high positive correlation of count with 'registered' and 'casual' as both of them together add up to represent count.
- Count is negatively correlated to 'windspeed' (-0.24 approximately). This gives us an impression that the shared bikes demand will be somewhat less on windy days as compared to normal days.
Correlation among independent variables:
- Some of the independent variables are highly correlated (look at the top-left part of matrix): atemp and temp are highly (positively) correlated. The correlation between the two is almost equal to 1.


- Bivariate Categorical (Categorywise demand)
- 
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/99eb96ea-97c7-4b7d-b595-bce5c9ec63f1)
- 1) As we had previously seen that number of rides increases from may to oct which corresponds to summer & fall season.
- 2) There is a significant increase in median number of rides from 2018 to 2019 (approx 50%, went from approx 4000 to approx 6000), this shows a good upward trend.
- 3) Day of the week has almost no impact on median number of rides. we will see what the model decides about weekdays variable.
- 4) It does not matter if its working day or not(weekend or holiday), the median number of rides is almost similar in both the cases, this might be caused by the fact that most of the users belong to "registered" category who are regular users,
- 5) weather situation 1, which is Clear, Few clouds, Partly cloudy is most favourable for our business.
- 6) From the "Mnth", we can see that the months are following a trend and could be a good predictor variable. The bookings in the mid-month are above 4000. The count is highest in the month of Sept
- 7) Also, there seems to be outliers present in season and year column, next we will check the outliers


# 3) Data Preparation for Model Building:

Pre-Processing :
- Created dummy variables for categorical variables using get dumies function
- Splitted data into train and test in 70-30 ratio.
- Scaled numerical variables using MinMax Scaler .

# 4) Model Building:

- Built a test model with all 28 features. adjusted_r2 - 84.2
- Reduced the features to 15, by using Recursive Feature Elimination
- Built 1st model with 15 features, got adjusted_r2_score - 84.0
- by dropping predictors with high p value(>0.05) or high vif (>5), built final model no 6.
- Final model has 10 predictors and adjusted_r2_score - 83.1 with all vif values within range.
  
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/b69cddb5-cdb8-4614-b4f9-e9ef7e94c207)

![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/d1bed199-58d1-4578-9861-0c41383d0c67)

- This model seems good as all the features are significant and vif values in range of or below 5 i.e very low multicollinearity. 
- The R2 score and Adj. R2 score is around 83%, which means around 83% of variation in data has been explained by the model.
- The f-stat value is grater than 1 and probability of f-stat is almost zero, which means that overall variables are highly significant and overall model is good fit.

# 5) Verification of Linear Regression Assumptions (Model Evaluation) :
- Assumption 1- Error Terms are Normally Distributed
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/ffa8f92a-700f-4026-8959-51138e81e2b7)

- Assumption 2- Error Terms are Independent of each other
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/61dca621-d6d6-4251-8f63-c08143d95c95)
From graph and pearson r coeff (almost 0), it is evident that the error terms are independent of each other.

- Assumption 3- the error terms have constant variances
 ![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/204af767-64cb-40a0-add4-b5c4892ff77a)

# 6) Prediction on Test Set:

![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/478270b9-d41a-412f-bcc4-3e2e4b7d7bf3)

# 7) Interpretation of model:
Final Equation for the best fit line - Relationship between target and predictors
   cnt =( 0.130722 + 0.232563* yr - 0.096575* holiday + 0.517336* temp -0.149709* windspeed + 0.101217* season_summer
   + 0.137090* season_winter + 0.054141* mnth_Aug + 0.116291* mnth_Sep 
    - 0.081139*weathersit_2 - 0.281852*weathersit_3 )

- 1) year: year and count shows positive relation with count variable, which means the demand is going to rise over the coming years, although this result may be biased as we only had dataset of 2 years which was following the same trend.
- 2) holiday : holiday showed negative relation with count, as per our equation, on holiday the rental count would dip by 0.096575 units.
- 3) temperature - with unit increase in temp the count will increase by 0.517336. As the data had max temp 35° C, this interpretation might hold true till temp in the vicinity of 35° C only.  
- 4) windspeed : windspeed and count shows negative relation. For a unit increase in wind speed the rental count would decrease by 0.149709.
- 5) season_summer,season_winter: Both the seasons shows positive relation with the count.
- 6) mnth_Aug,mnth_Sep: In month of aug, sept the demand for rental would increase.
- 7) weathersit_2, weathersit_3: For a unit increase in weather situation 2, the count will decrease by 0.081139 and For a unit increase in weather situation 3, the count will decrease by 0.281852
 
# 8) Conclusion and Recommendations

- 1) Temperature - With increase in temp the rental count would also increase, as a good gesture, company can provide free coupon for a complimentary cold drink with the rental ride, which customers can reedem on specific stores where company has done tie ups with. Although this might seem insignificant but will definitly lead to positive word of mouth publicity and ultimately increase the awarness about the rental service.
- 2) holiday : Either company can provide some discount offers on holiday to increase the rental count or hike the rental price by some margine in order to compensate the revenue lost by dip in rental count. Company will have to implement both of these strategies and closely observe the repurcussions on rental count. Also, the price hike should be gradual or else it might hurt the sentiments of customers.
- 3) windspeed : Boombike company can improve the existing design of bikes by focusing more on aerodynamics to counter the windspeeds and include this as an additional safety measure while doing marketing and promotion in order to increase awarness among customers. 
- 4) season_summer,season_winter: as we know in summer and winter the demand is going to rise, we can deploy more bikes to reduce the waiting time of customers (if applicable) in high demand areas during peak hours.
- 5) mnth_Aug,mnth_Sep: In month of aug, sept the demand for rental would increase. to capitalise this opportunity we can organise some special campaigns in the month of may and june to enroll more customers as registered members.
- 6) weathersit_2, weathersit_3: As we know, the demand is going to decrease in these weather situations, company can provide some discount coupons to encourage new customers to try out our service.
