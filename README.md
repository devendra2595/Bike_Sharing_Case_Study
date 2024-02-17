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
- Univariate Numerical: 'temp','atemp','hum','windspeed','cnt'. Most of the variable were normally distributed with 'temp' and 'atemp' showing obvious signs of multicollinearity.

- Bivariate (Categorywise demand)
![image](https://github.com/devendra2595/Bike_Sharing_Case_Study/assets/116253033/99eb96ea-97c7-4b7d-b595-bce5c9ec63f1)






