# BIKE-SHARING
INTRODUCTION
This case study aims to give an idea of applying linear regression in a real business scenario for a bike-sharing provider "BoomBikes" to model the demand for shared bikes with the available independent variables. It will be used by the management to understand how exactly the demands vary with different features. They can accordingly manipulate the business strategy to meet the demand levels and meet the customer's expectations. Further, the model will be a good way for management to understand the demand dynamics of a new market.

DATA EXPLORATION AND CLEANING
In the data set we had few columns which did not contribute towards business goal and thus could be ignored for our analysis. Such columns were instant, dteday, casual and registered. We have dropped these columns.
There were few categorical columns in this data set which hold the values in numerical form. Those were converted to their respective categorical form as per the data dictionary for better representation and understanding of data.
It was assumed that 0 - 6 represent Sunday - Saturday.
EDA AND DATA VISUALIZATION
In this step we visualized and explored the categorical as well as continuous variables present in the data set.

image

Most of the days have temperature 10-30 degrees. T
Distribution of temp and atemp are almost similar.
Most of the days are with humidity 50-80.
Wind speed seems to be distributed mostly between 5 - 20.
Total count of rental bikes seems to be normally distributed with a mean value between 4000-5000.
image

There are no significant outliers as such present in the data
Weather is surely impacting the bike rental counts as clearly visible from the plot. The meadin value is highest when the weather is good and then decreasing as the weather becomes worse.
Season is also a fairly contributing factor in the total rental count. Summer and Fall are more favourable seasons.
Working day seems to have a very little impact.
More bikes are rented between the months Jun-Oct.
Most of the days are good or fair weather days.
Demand seems to be less on holidays.
image

Most of the days in Fall season were good with clear sky followed by Summer, Spring and Winter.
Winter has most number of bad weather days.
image

Most of the days in the month of June, July, August and November are good weather days.
October has the most number of bad weather days with heavy shower/snow.
image

Rental count was the highest in the Fall season irrespective of the weather condition.
Spring season has the lowest demand.
image

In most of the months if weather is good/fair, demand is more.
In July, irrespective of the weather condition, demand is high.
The demand is the lowest in the month of January.
image

Looks like holidays have less demand.
Looks like holidays have less demand.

image

Temperature and rental count are highly correlated.
The demand is high on good weather days and when temperature is pleasant (20-30 degree).
image

Humidity and rental count are negatively correlated.
The demand is high on good weather days when humidity is low (40-60).
image

'temp' and 'atemp' are highly correlated, which means their impact on the total rental counts are fairly similar. Hence, we may consider just one (say temp) and ignore the other one while building our model to avoid any multicollinearity.

image

'temp' and 'atemp' are very highly correlated. If both present, they might introduce multicollinearity. Hence, we need to keep any one and drop the other one as they both have same correlation coefficient 0.63 with the target variable 'cnt'.
From the above heatmap we can clearly see that the independent variables 'temp' and 'atemp' are highly correlated to the dependent variable 'cnt', followed by 'windspeed'.
'windspeed' and 'humidity' are correlated with a negative coefficient as humidity tends to be more when there is less wind.
Assumption - To get rid of independent variables with coefficient > 0.7 or < -0.7 with other independent variable(s).

image

Now that we have dropped 'atemp' , we don't have any other very highly correlated independent variables. We can now start with model building process.

DATA PREPARATION
Creating Dummy variables for the categorical columns - 'weekday','mnth','season','weathersit','yr','holiday' & 'workingday'.
Splitting data into Train and Test in 70-30 proportion.
Rescaling the features of the training data using Min-Max Scaler.
image

The heatmap above displays the collinearity between independent variables and the dependent (cnt) variable.
This also tells us about existing multi-collinearity between the independent variables.
This will be helpful while considering multiple independent variables in model building step.
The hypothesis was be formulated as -
Null Hypothesis - H0 : Coefficients of the independent variables are insignificant
Alternate Hypothesis - H1 : Coefficients of the independent variables are significant
MODEL BUILDING
Assumptions
There is a linear relationship between X and y
Error terms are normally distributed with a mean value 0
Error terms have constant variance ( homoscedasticity )
Error terms are independent of each other ( no multicollinearity )
Also we are going to assume 99% confidence interval. So, we will take into consideration p-value below 1% or p-value < 0.01. Similarly we will assume VIF limit of 5.

Splitting training data into X and y
RFE (Recursive Feature Elimination) - First we will use RFE for feature elimination. The columns we get from RFE will be considered for further manual refining of the model.
Building model using statsmodel, for the detailed statistics
Final model co-efficients and VIF:

image

p-values for all variables are significant as they are exactly 0.

image
