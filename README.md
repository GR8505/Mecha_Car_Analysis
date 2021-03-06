# Mecha_Car_Analysis
-----------------------------------------------------------------------------

 ----------------
| MPG REGRESSION |
 ----------------
-------------------------------------------------------------------------------------------------------
1. Which variables/coefficients provided a non-random amount of variance to the mpg values in the
   dataset?

-------------------------------------------------------------------------------------------------------
From the correlation plot I saw that vehicle length and mpg had a moderate positive correlation.
In addition, ground clearance and mpg had a weak positive correlation. AWD and spoiler angle each 
share a weak negative correlation with mpg, while vehicle weight had a very weak positive correlation 
with mpg.

From this analysis, vehicle length and ground clearance looked like the two most significant 
independent variables that affected the dependent variable (mpg).

Nevertheless, I performed backward selection with all variables before choosing the most parsimonious 
model.

-------------------------------------------------------------------------------------------------------
| Backward Selection |
-------------------------------------------------------------------------------------------------------
I ran the following linear regression model first:
lm(mpg ~ v_length + g_clearance + AWD + v_weight + s_angle, MechaCar_data)


-------------------------------------------------------------------------------------------------------
As initially anticipated, vehicle length and ground clearance were the two most significant independent 
variables in this model. The p-values for AWD, spoiler angleand vehicle weight were all > 0.05.  However, 
v_weight was just above 0.05.  I removed spoiler angle (as it had the highest p-value) to see whether 
the p-values of both vehicle weight and AWD would decline.  
I also monitored the AIC (which is a measure of fit for the model). The lower the AIC the more realistic
the model.
-------------------------------------------------------------------------------------------------------

I then ran this model:
lm(mpg ~ v_length + g_clearance + AWD + v_weight, MechaCar_data)

-------------------------------------------------------------------------------------------------------
Clearly both AWD and vehicle weight are not significant to this model as both their p-values increased. 
AIC dropped from 366.6861 to 365.8857 with the removal of the independent variable, spoiler angle.  
I then proceeded to remove both AWD and vehicle weight variables.
------------------------------------------------------------------------------------------------------

I ran the following model:
lm(mpg ~ v_length + g_clearance, MechaCar_data)

------------------------------------------------------------------------------------------------------
Both independent variables, vehicle length and ground clearance are signifcant. However, the AIC
increased and the r-squared declined. n our previous lm model mpg ~ v_length + g_clearance + AWD + 
v_weight, the AIC was 365.8857 but now it is 367.3899. 
I then proceeded to add vehicle weight back to the model to see how it affected both the r-squared and 
AIC
-------------------------------------------------------------------------------------------------------

Ran the following model:
lm(mpg ~ v_length + g_clearance + v_weight, MechaCar_data)

-------------------------------------------------------------------------------------------------------
AIC improved but was still higher than the AIC value of 365.8857 for lm model mpg ~ v_length + g_clearance 
+ AWD + v_weight.  Therefore, the most parsimonious model was mpg ~ v_length + g_clearance + AWD + v_weight
-------------------------------------------------------------------------------------------------------

 -----------------------------------------------------------------------------
| mpg_reg <- lm(mpg ~ v_length + g_clearance + AWD + v_weight, MechaCar_data) |
 -----------------------------------------------------------------------------

-------------------------------------------------------------------------------------------------------
2. Is the slope of the linear model considered to be zero? Why or why not?

Null Hypothesis: The slope of the linear model is zero
Aleternative Hypothesis: The slope of the linear model is not zero

The p-value for our model is 1.586e-11, which is significantly lower than 0.05.  Therefore, this 
serves as enough evidence to reject our null hypothesis, so I concluded that the slope of the 
linear model is not zero.

-------------------------------------------------------------------------------------------------------
3. Does this linear model predict mpg of MechaCar prototypes effectively? Why or why not?

Based on the r-squared value, roughly 71 percent of the mpg values can be predicted correctly
using the linear model.  Therefore, this is a robust model.  However, we must take note that the
p-value of the y-intercept is < 0.05, which indicates that there could be other variables that 
have not been taken into account that explains our model (or can be used to predict mpg).

-------------------------------------------------------------------------------------------------------
 -------------------------
| SUSPENSION COIL SUMMARY |
 -------------------------

Q: The design specifications for the MechaCar suspension coils dictate that the variance of the 
   suspension coils must not exceed 100 pounds per inch. Does the current manufacturing data meet this 
   design specification? Why or why not?

A: Yes. According to our summary_table2, the variance of the suspension coils is less than 100 pounds
   per inch (at 76.23459).


-------------------------------------------------------------------------------------------------------
 ------------------------
| SUSPENSION COIL T-TEST |
 ------------------------
 
Q: Using the same suspension coil data and the MechaCarChallenge.RScript file, determine if the 
   suspension coil’s pound-per-inch results are statistically different from the mean population 
   results of 1,500 pounds per inch. 

A: Tested to see if the data was normally distributed.  From my population density diagram the data didn't 
   appear to be left or right skewed but the results from the shapiro test indicated that the data was not
   normally distributed.


   Null Hypothesis: There is no statistical difference between the observed sample mean and the population
                    mean of 1,500 pounds per inch
   Alternative Hypothesis: There is a statistical difference between the observed sample mean and the 
                           population mean of 1,500 pounds per inch

   Proceeded to create sample data to perform my one-sample T-Test
    ---------
   | Results |
    ---------
   The p-value of 0.3471 is greater than 0.05, therefore I did not have sufficient evidence to reject the 
   null hypothesis.  Hence, the suspension coil's pound per inch results are statistically different from
   the mean population results of 1,500 pounds per inch.

------------------------------------------------------------------------------------------------------------
 -----------------------
| DESIGN YOUR OWN STUDY |
 -----------------------

Metrics to Include in Study 
* Total Cost to Manufacture
* Number of Safety Features (Will have 10 categories => 1, 2, 3, 4, 5, 6......10)
* Horsepower (Will be categorical 85-120, 121-199, 200-299, 300-399, 400-520.....)


What Questions to Ask
* How does Horsepower and the Number of Safety Features affect MPG?
  In this test, I will test to see whether the mean MPG is affected for vehicles with 200HP-299HP and 10 Safety 
  Features.

  Null Hypothesis: The mean MPG for both groups are equal
  Alternative Hypothesis: At least one of the means is different from the other group


What Test to Perform 
* I will perform a two-way ANOVA.


What Data do I need to Collect 
* I will need to filter all vehicles with HP of 200 to 299 with their mpg values 
* I will also need to create another sample with all vehicles with 10 Safety Features and their mpg values 

-------------------------------------------------------------------------------------------------------------
