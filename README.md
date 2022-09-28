# Ames-housing

#Summary

## Problem Statement
We intend to build a model which can effectively predict housing sale prices. We further intend to identify features that contribute to changes in housing prices so as to equip real estate agents with the knowledge to better advise their clients and improve their sales margin


## Data cleaning, feature engineering and data visualization
### Data cleaning
To begin with, all null or missing values were identified. 

    * Handling ordinal columns
Refering to the [data description](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt) provided, missing values in ordinal columns were handled first. All null values were replaced with the integer "0" while the other subcategories within each column were ordered in ascending order i.e. Quality columns were ordered as follows : "Ex" = 5, "Gd" = 4, "TA" = 3, "Fa"= 2, "Po"= 1.

    * Impute values for LotFrontage (dealing with missing values)
Next missing values in LotFrontage were identified. LotArea and LotShape were used to predict missing LotFrontage and after running a linear regression model, missing values were imputed with predicted values. the original LotFrontage column was then dropped.

    * Dropping columns with <5% unique values
For nominal columns such as "Alley", "Garage Type" and "Misc Feature" all null values were replaced with the string "None" as cross-referenced from the data description. Next, features with more than 95% of common values were dropped as these features would not be efficient to predict "SalePrice". As a rule of thumb, if one value dominates a column, it will not be a good predictor of the target. 

The following features were dropped:'Street', 'Condition2', 'RoofMatl', 'Heating', 'MiscFeature','Utilities', 'LandSlope', 'LowQualFinSF', 'KitchenAbvGr', '3SsnPorch', 'PoolArea', 'PoolQC', 'MiscVal'

    * Dropping rows where =<5% data is null
Numeric columns which still contained missing/null values were then identified. Rows that contained missing values from these columns were then dropped.
    

### Feature engineering
    * Creating TotalBaths column, dropping other Bath columns
A TotalBaths column was created by adding the features 'BsmtFullBath', 'BsmtHalfBath', 'FullBath' and 'HalfBath'. This was done to reduce model complexity yet retain predictive features. 

    * Creating Age column
Similarly an Age column was manufactured by subtracting "YearRemod/Add" from "YrSold".
    
### Data cleaning pt 2.
    * Checking for intercorrelated features for numerical data and dropping columns with high colinearity with other features but low correlation to SalePrice
Intercorrelated features needed to be dropped as they do not accurately aid in predicting sale price. Features with higher correlation to Sale price were retained while those with lower correlation to sale price were dropped. As a result, the following columns were dropped: "KitchenQual","BsmtQual","ExterQual","Age","GarageYrBlt","YearRemod/Add","BsmtFinType1","BsmtFinType2","1stFlrSF","2ndFlrSF","TotRmsAbvGrd","Fireplaces","GarageArea"

    * Dropping outliers beyond 4std from continuous variables based on skew
Looking at the skew of continuous features, outliers above 4std were removed from features that had a skew greater than 1.

    * Final steps
All nominal columns were then dummified. ID and PID columns were dropped.

## Data modelling
Linear regression, ridge regression and lasso regression were used to model the data.
