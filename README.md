# Bike_Sharing_Case_Study
# Problem Statement:

A US bike-sharing provider `BoomBikes` has a daily dataset on the rental bikes based on various environmental and seasonal settings. It wishes to use this data to understand the factors affecting the demand for these shared bikes in the American market and come up with a mindful business plan to be able to accelerate its revenue as soon as the ongoing lockdown due to corona pandemic comes to an end.

Essentially, the company wants to know —
- Which variables are significant in predicting the demand for shared bikes.
- How well those variables describe the bike demands

**So interpretation is important!**

# Libraries Used
numpy
pandas
matplotlib
seaborn
statsmodels
sklearn
scipy

# The solution is divided into the following sections: 
- Data understanding and Exploration
- Data Visualisation 
- Data preparation
- Model building and evaluation


# 1) Data understanding and Exploration :
Read and understood the data.
- The data was from 1/1/2018 to 31/12/2019.
- Some of the variables were label encoded, e.g.'mnth','weekday', 'Season' variable had 1,2,3 & 4 instead of actual season names.
So, to avoid their misinterpretation, converted them back to their original category name and changed them to categorical datatype.

# 2) Data Analysis and Visualisation
- Univariate Numerical: 'temp','atemp','hum','windspeed','casual','registered','cnt'. Most of the variable were normally distributed with 'temp' and 'atemp' showing obvious signs of multicollinearity.

- Bivariate (Categorywise demand)
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/99eb96ea-97c7-4b7d-b595-bce5c9ec63f1)
- For the variable season, we can clearly see that the category 3 : Fall, has the highest median, which shows that the demand was high during this season. It is least for 1: spring.
- The count of users is less during the holidays
- From the "Workingday", we can see that maximum bookings happening between 4000 and 6000. There is not much of difference in booking whether its working day or not.
- The count of total users is in between 4000 to 6000 during  weather sitiation A.
- From the "Mnth", we can see that the months are following a trend and could be a good predictor variable. The bookings in the mid-month are above 4000. The count is highest in the month of Sept
- The bike demand is almost constant throughout the week. there seems no trend in the weekday dataset.
- The year 2019 had a higher count of users as compared to the year 2018.
- Also, its important to note that, almost all the categories do not have any significant outliers.


- Bivariate (Numerical) : Heatmap
  ![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/fa23d20a-e18e-4aea-b750-aa8493bd4abf)
  
Correlation of Count('cnt') with independent variables:
- Count('cnt') is highly (positively) correlated with 'casual' and 'registered' and further it is with 'atemp'.
- We can clearly understand the high positive correlation of count with 'registered' and 'casual' as both of them together add up to represent count.
- Count is negatively correlated to 'windspeed' (-0.24 approximately). This gives us an impression that the shared bikes demand will be somewhat less on windy days as compared to normal days.

Correlation among independent variables:
- Some of the independent variables are highly correlated (look at the top-left part of matrix): atemp and temp are highly (positively) correlated. The correlation between the two is almost equal to 1.

# 3) Data Preparation for Model Building:







