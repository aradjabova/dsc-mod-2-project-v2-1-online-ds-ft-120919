
# Purpose

For this analysis, I will be working with the dataset.

I'll clean, explore, and model this dataset with a multivariate/single linear regression to predict the sale price of houses as accurately as possible.

I have created some questions for the model and analysis to answer.

# Dataset

In this analysis I will be working with the King County House Sales dataset.  The dataset can be found in the file `"kc_house_data.csv"`, in this repo.

The description of the column names can be found in the column_names.md file in this repository. 


# Methodology

![methodology.png](Images/methodology.png)

* Obtain - get all the data needed to use
* Scrub - clean the data to from missing data; null values; place holders etc
* Explore - find patterns/correlations/relations between the data
* Model - create  models to predict the target values (carefull of multicolinearity)
* N(results) - test the results make sure they are valid

# Scrub/Overview

![map_price.png](attachment:map_price.png)

This is a map overview of the houses sold in Kings County Seattle, WA.
* Some places in Kings County are sold for higher
* There are clusters of homes that are sold for higher 

What/Is there realtionships?


## Overview

![Screen%20Shot%202020-02-16%20at%204.57.33%20PM.png](attachment:Screen%20Shot%202020-02-16%20at%204.57.33%20PM.png)

* There are about 21 different columns in the dataset
* There are about 21,597 entries in the data
* There are a some missing data in some columns
* There are some placeholders in the columns

                        Each Column Scatter Plotted Against Eachother

![download.png](attachment:download.png)

Shows all the columns plotted against eachother.
* There are some categorical columns in the data
* Some columns have a positive linear realtionships with the price (target)
* Some columns have positive relationships with the target
* Most of the distributions on the columns are not completely normal but are skewed
* Some columns have relationships with other columns (good to look out for multicolinearity)


![download%20%281%29.png](attachment:download%20%281%29.png)

A correlation map shows the correlation between each columns against each other:
* price is very correlated to:
    * sqft_living15 - .59
    * sqft_above - .61
    * grade - .67
    * sqft_living - .7
    * bathrooms - .51
* Some columns have strong correlations to each other
    * important because regressions cannot have multicolinearity

## Missing Values

![missing_bar.png](attachment:missing_bar.png)

While looking into the data we can see that we have missing data:
* view
* waterfront

How to deal with:
* Since it is only two columns that are missing data we can drop them
* Do not use these columns for regression features

### Duplicates

![Duplicates.png](attachment:Duplicates.png)

When cleaning data a key thing to consider is duplicate data:
* using a unique feature (column)
* print the duplicate columns of the unique features
*  **the ID's may be duplicated but the houses were resold at later dates (keep)**

### Place Holders

![Placeholders.png](attachment:Placeholders.png)

After printing all the unique values of each of the columns:
* Sqft_basement have '?' values
    * Probably means they do not know if the house has a basement
    * Replace '?' with 0 - count them as not having until proven otherwise

## Outliers

![price_original.png](attachment:price_original.png)

![price_transformed.png](attachment:price_transformed.png)

![price_orig_box.png](attachment:price_orig_box.png)

![price_trans_box.png](attachment:price_trans_box.png)

![orig_cor_price_sqftliving.png](attachment:orig_cor_price_sqftliving.png)

![trans_cor_price_sqftliving.png](attachment:trans_cor_price_sqftliving.png)

![grade_orig_box.png](attachment:grade_orig_box.png)

![grade_tran_box.png](attachment:grade_tran_box.png)

![orig_cor_price_sqftabove.png](attachment:orig_cor_price_sqftabove.png)

![trans_cor_price_sqftabove.png](attachment:trans_cor_price_sqftabove.png)

# For Seller Question 1: How well can the zipcode, number of floors and month to sell predict the price?

## Explore Patterns/ Trends

![Q1%20zipcodes.png](attachment:Q1%20zipcodes.png)

Exploring Zipcodes against price:
* some zipcodes have higher average priced homes:
    *98039; 98040; 98004; etc.
* Some zipcodes have average lower sold houses:
    *98001; 98002; 98032; etc.

There is definetly a relationship between zipcodes and prices

![Q1%20months.png](attachment:Q1%20months.png)

Exploring months against prices:
* Some months have a **slight** better average selling amount
* There is not a strong correlation but there is a slight one

![Q1%20floors.png](attachment:Q1%20floors.png)

Exploring the realtionship betweeen floors and prices:
   * Having a higher number of floors does increase the number the amount the home is sold for to an extent
   * 1 floor homes have more homes sold for 210000; but they do have homes sold for highest amounts too

## Model

### Actual Model

![Screen%20Shot%202020-02-17%20at%2011.41.07%20AM.png](attachment:Screen%20Shot%202020-02-17%20at%2011.41.07%20AM.png)
![Screen%20Shot%202020-02-17%20at%2011.41.26%20AM.png](attachment:Screen%20Shot%202020-02-17%20at%2011.41.26%20AM.png)
![Screen%20Shot%202020-02-17%20at%2011.41.39%20AM.png](attachment:Screen%20Shot%202020-02-17%20at%2011.41.39%20AM.png)
![Screen%20Shot%202020-02-17%20at%2011.42.00%20AM.png](attachment:Screen%20Shot%202020-02-17%20at%2011.42.00%20AM.png)
![Screen%20Shot%202020-02-17%20at%2011.42.13%20AM.png](attachment:Screen%20Shot%202020-02-17%20at%2011.42.13%20AM.png)




    The average error is about $117,000 in this model

### Explaination

                                TESTING MULTICOLINEARITY

![q1%20nomulti%20floorzip.png](attachment:q1%20nomulti%20floorzip.png)

Zipcodes and floors do not have a realtionship; meaning that knowing the zipcode cannot predict the number of floors a house has

![q1%20nomulti%20monzip.png](attachment:q1%20nomulti%20monzip.png)

Zipcodes and months have no relationship; meaning that the month cannot predict which zipcode the house is from; vice versa

![q1%20nomulti%20floormon.png](attachment:q1%20nomulti%20floormon.png)

Number of floors and months have no relationship; meaning that the number of floors cannot predict which zipcode the house is from; vice versa

Multicolinearity - meaning that the fetures in the model are able to predict each other


As the above graphs show; the features used in this model cannot predict eachother; so one of the assumptions of the multiple linear regression is met

## Interpert

Model:
* has a 93 % accuarcy of guessing the price of homes given the zipcode, number of floors; and month to sell

Coeficents
* zipcodes - all the zipcodes have an average of 3.56e+05 positive of coefficents
    * each different zipcode has a different strength of relationship to price 
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not completely big compared to the model coefficents
* floors - floors have different best coeficents for the model
    * floors to price does not have a concreat positive realtionship; could go either way
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not completely big compared to the model coefficents    
* months - all have positive realtions with price but some months have slightly different average coefficents
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not completely big compared to the model coefficents

Residuals:
* Skew: .495
    * meaning that the skew of the residuals is not bad (close to normality)
* Kurtosis: 3.741
    * the amount of residuals are all in 3.741 standard deviations away from the mean
    * which is pretty normal not that bad a big high
* Condition Numbers:
    * substantially lower; can indicated that there is little to no multicolinearity in the model

![Q1%20meme%20sell%20house.jpg](attachment:Q1%20meme%20sell%20house.jpg)

                                        Residual Distribution

![Q1%20Distribution.png](attachment:Q1%20Distribution.png)

The residual distribution looks pretty normal which meets one of the assumptions of multilinear regression.


This means that the residuals the are around our linear regression model are normal distributed around it. (none of the true points are too far from our predicted value)

                               Ploting the Residuals of the Regression 

![Q1%20Residuals.png](attachment:Q1%20Residuals.png)

**Homoscedasticity is the third assumption necessary when creating a linear regression model, meaning that the residuals are linear and not cone shaped**


The residuals plotted shows that the residuals are homoscedastic. They are linear and not cone shaped.


                                       Train Test Split

![Q1%20train%20test.png](attachment:Q1%20train%20test.png)

After double checking the testing and training errors of the model the model is not overfitted

# For Seller Question 2: How well does you house condition and number of bedrooms predict price?


## Explore

![Q2%20bedrooms%20price.png](attachment:Q2%20bedrooms%20price.png)

Exploring number of bedrooms against price:
* some number ofbedrooms have higher average priced homes:
    *4; 5; 6 number bedrooms
* Some zipcodes have average lower sold houses:
    *1; 2; 3

There is definetly a relationship between number of bedrooms and prices

![Q2%20grade%20price.png](attachment:Q2%20grade%20price.png)

Exploring condition against price:
* some number of bedrooms have higher average priced homes:
    *9, 10, 11, condition
* Some zipcodes have average lower sold houses:
    *5, 6, 7 condition

There is definetly a relationship between condition and prices

## Model

### Actual Model

![Q2%20Model.png](attachment:Q2%20Model.png)

### Explaination


                                TESTING MULTICOLINEARITY

![Q2%20no%20multi%20grade%20bed.png](attachment:Q2%20no%20multi%20grade%20bed.png)

Number of bedrooms and condition do not have a realtionship; meaning that knowing the numberof bedrooms cannot predict the grade a house has

## Interpert

Model:
* has a 87 % accuarcy of guessing the price of homes given the grade and number of bedrooms

Coeficents
* condition - all the condition coefficents have an average of 2.56e+05 positive of coefficents
    * each different condition has a different strength of relationship to price 
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not completely big compared to the model coefficents
* number of bedrooms - all the number of bedrooms coefficents have an average of 2.18e+04 positive of coefficents
    * number of bedrooms to price does have a concreat positive realtionship; usually more would be more price
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not completely big compared to the model coefficents    

Residuals:
* Skew: .468
    * meaning that the skew of the residuals is not bad (close to normality)
* Kurtosis: 2.478
    * the amount of residuals are all in 2.478 standard deviations away from the mean
    * which is pretty normal not that bad a big high
* Condition Numbers: 23.2
    * substantially lower; can indicated that there is little to no multicolinearity in the model

![meme%202.jpg](attachment:meme%202.jpg)

                                        Residual Distribution

![Q2%20distribution.png](attachment:Q2%20distribution.png)

The residual distribution looks pretty normal; is a bit skewed and leaning but semi normal which meets one of the assumptions of multilinear regression.


This means that the residuals the are around our linear regression model are normal distributed around it. (none of the true points are too far from our predicted value)

                               Ploting the Residuals of the Regression 

![Q2%20residuals.png](attachment:Q2%20residuals.png)

**Homoscedasticity is the third assumption necessary when creating a linear regression model, meaning that the residuals are linear and not cone shaped**


The residuals plotted shows that the residuals are homoscedastic. They are linear and not cone shaped.


                                    Train Test Split

![Q2%20Train%20Test.png](attachment:Q2%20Train%20Test.png)

After double checking the testing and training errors of the model the model is not overfitted or underfitted

# For Realtor Question 3: How well does the square foot of the houaew and sqaure foot of the basement predict price?


## Explore

![Q3%20sqft%20above%20price.png](attachment:Q3%20sqft%20above%20price.png)

Exploring square foot above against price:
* As the sqare foot above goes up the prie of the houses goes up


There is definetly a relationship between sqare foot above and prices

![Q3%20sqft%20base%20price.png](attachment:Q3%20sqft%20base%20price.png)

Exploring square foot basement against price:
* As the sqare foot basement goes up the prie of the houses goes up


There is definetly a relationship between sqare foot basement and prices

## Model

### Actual Model


![Q3%20model.png](attachment:Q3%20model.png)

### Explaination

![Q3%20no%20multi%20above%20base.png](attachment:Q3%20no%20multi%20above%20base.png)

Square foot basement and sqare foot above do not have a realtionship; meaning that knowing the sqare foot basement cannot predict the sqarefoot above of a house has

## Interpert

Model:
* has a 89 % accuarcy of guessing the price of homes given the square foot basement and square foot above

Coeficents
* sqare foot basement - the sqare foot lot coefficents have an average of 229 positive of coefficents
    * this means that for ever square foot basement increate there is a 229 time increase in price
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not that bad; 0.742
* square foot above - the sqare foot lot coefficents have an average of 213 positive of coefficents
    * this means that for ever square foot above increase there is a 213 time increase in price
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not big of 2.904
Residuals:
* Skew: .156
    * meaning that the skew of the residuals is not bad (close to normality)
* Kurtosis: 2.95
    * the amount of residuals are all in 2.859 standard deviations away from the mean
    * which is pretty normal not that bad a big high
* Condition Numbers: 4.41
    * substantially lower; can indicated that there is little to no multicolinearity in the model

![meme3.jpg](attachment:meme3.jpg)

                                        Residual Distribution

![Q3%20distribution.png](attachment:Q3%20distribution.png)

The residual distribution looks pretty normal; is a bit weird at the top but semi normal which meets one of the assumptions of multilinear regression.


This means that the residuals the are around our linear regression model are normal distributed around it. (none of the true points are too far from our predicted value)

                               Ploting the Residuals of the Regression 

![Q3%20residuals.png](attachment:Q3%20residuals.png)

**Homoscedasticity is the third assumption necessary when creating a linear regression model, meaning that the residuals are linear and not cone shaped**


The residuals plotted shows that the residuals are homoscedastic. They are linear and not cone shaped.


![Q3%20qqplot.png](attachment:Q3%20qqplot.png)

                                    Train Test Split

![Q3%20train%20test.png](attachment:Q3%20train%20test.png)

After double checking the testing and training errors of the model the model is not overfitted or underfitted

# For Realtor Questions 4: How does the square foot of the property and the square foot of the house predict the price of the house?

## Explore

![Q4%20sqft%20above%20price.png](attachment:Q4%20sqft%20above%20price.png)

Exploring square foot above against price:
* There is a positive linear relationship between these two features

The higher the square foot above the higher the price

![Q4%20lot%20and%20price.png](attachment:Q4%20lot%20and%20price.png)

Exploring square foot lot against price:
* There is a positive linear relationship between these two features

The higher the square foot lot the higher the price

## Model

### Actual model

![Q4%20Model.png](attachment:Q4%20Model.png)

### Explaination


![Q4%20nomulti%20.png](attachment:Q4%20nomulti%20.png)

Square foot lot and sqare foot above do not have a realtionship; meaning that knowing the sqare foot lot cannot predict the sqarefoot above of a house has

## Interpert

Model:
* has a 86 % accuarcy of guessing the price of homes given the square foot lot and square foot above

Coeficents
* sqare foot lot - the sqare foot lot coefficents have an average of 1.14 positive of coefficents
    * this means that for ever square foot lot increate there is a 1.14 time increase in price
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not that bad; 0.119
* square foot above - the sqare foot lot coefficents have an average of 246.67 positive of coefficents
    * this means that for ever square foot lot increate there is a 246.67 time increase in price
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not big of 1.09
Residuals:
* Skew: .148
    * meaning that the skew of the residuals is not bad (close to normality)
* Kurtosis: 2.859
    * the amount of residuals are all in 2.859 standard deviations away from the mean
    * which is pretty normal not that bad a big high
* Condition Numbers: 11.3
    * substantially lower; can indicated that there is little to no multicolinearity in the model

                                        Residual Distribution

![Q4%20distributuion.png](attachment:Q4%20distributuion.png)

The residual distribution looks pretty normal; is a bit weird at the top but semi normal which meets one of the assumptions of multilinear regression.


This means that the residuals the are around our linear regression model are normal distributed around it. (none of the true points are too far from our predicted value)

                               Ploting the Residuals of the Regression 

![Q4%20residuals.png](attachment:Q4%20residuals.png)

**Homoscedasticity is the third assumption necessary when creating a linear regression model, meaning that the residuals are linear and not cone shaped**


The residuals plotted shows that the residuals are homoscedastic. They are linear and not cone shaped.


                                    Train Test Split

![Q4%20trai%20test.png](attachment:Q4%20trai%20test.png)

After double checking the testing and training errors of the model the model is not overfitted or underfitted

# For Seller & Realtor Questions 4: How does the year the house was built and month selling and condition effect price?

## Explore

![Q5%20condition%20price.png](attachment:Q5%20condition%20price.png)

Exploring Condition against price:
* some conditions have higher average priced homes:
    * 5
* Some zipcodes have average lower sold houses:
    *2, 3; etc.

There is definetly a relationship between condition and prices

![Q5%20month%20price.png](attachment:Q5%20month%20price.png)

Exploring months against prices:
* Some months have a **slight** better average selling amount
* There is not a strong correlation but there is a slight one

![Q5%20yr%20price.png](attachment:Q5%20yr%20price.png)

Exploring year built against prices:
* Some years have a **slight** better average selling amount
* There are great differences between the different years that houses are built and price

## Model

### Actual Model

![Q5%20model%201.png](attachment:Q5%20model%201.png)
![Q5%20model%202.png](attachment:Q5%20model%202.png)
![Q5%20model%203.png](attachment:Q5%20model%203.png)

### Explaination

![Q5%20no%20multi1.png](attachment:Q5%20no%20multi1.png)

Months and Condition do not have a realtionship; meaning that knowing the months cannot predict the condition a house has

![Q5%20no%20multi%202.png](attachment:Q5%20no%20multi%202.png)

Year built and Condition do not have a realtionship; meaning that knowing the year built cannot predict the condition a house has

![Q5%20no%20multico3.png](attachment:Q5%20no%20multico3.png)

Months and year built do not have a realtionship; meaning that knowing the months cannot predict the year built of a house.

## Interpert

Model:
* has a 87 % accuarcy of guessing the price of homes given the grade and number of bedrooms

Coeficents
* condition - all the condition coefficents have an average of 2.56e+05 positive of coefficents
    * each different condition has a different strength of relationship to price 
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are pretty big compared to the model coefficents
* year built - all the number of bedrooms coefficents have a high average based on all the different years built
    * year builts to price does not have a concreat positive realtionship;
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are  big compared to the model coefficents    
* months - all the number of bedrooms coefficents have an average of 2.68e+04 positive of coefficents
    * month to price does not have a concreat positive realtionship; 
    * all p-values are less that 0.05 or 0 which means that the model did not randomly guess this but it was predicted
    * the standard errors are not  big compared to the model coefficents    

Residuals:
* Skew: .544
    * meaning that the skew of the residuals is not bad (close to normality)
* Kurtosis: 2.614
    * the amount of residuals are all in 2.614 standard deviations away from the mean
    * which is pretty normal not that bad a big high
* Condition Numbers: 93
    * substantially lower; can indicated that there is little to no multicolinearity in the model

![meme4.jpg](attachment:meme4.jpg)

                                        Residual Distribution

![Q5%20distribution.png](attachment:Q5%20distribution.png)

The residual distribution looks pretty normal which meets one of the assumptions of multilinear regression.


This means that the residuals the are around our linear regression model are normal distributed around it. (none of the true points are too far from our predicted value)

                               Ploting the Residuals of the Regression 

![Q5%20residual.png](attachment:Q5%20residual.png)

**Homoscedasticity is the third assumption necessary when creating a linear regression model, meaning that the residuals are linear and not cone shaped**


The residuals plotted shows that the residuals are homoscedastic. They are linear and not cone shaped.


                                       Train Test Split

![Q5%20train%20test.png](attachment:Q5%20train%20test.png)

After double checking the testing and training errors of the model the model is not overfitted

# Future Work

Some futer work that I would like to do:
* Gather data on waterfront:
    * Do a data analysis with the the waterfront to see if it makes a difference in price
* Gather data on view:
    * Do a data analysis with the the view to see if it makes a difference in price
* Gather data on the sqarefoot basement:
    * Find out about the sqarefootage of the basement to see if it makes a difference in price
* Gather data on year renovates:
    * Do a data analysis with the the year renovated to see if it makes a difference in price

# Conclusion

There are different features that can be used to precit the price of a house.

Depending on the information about a house provided, we would be able to predict the price of a house to a certain degree (have a margin of error) in the predicted price.
