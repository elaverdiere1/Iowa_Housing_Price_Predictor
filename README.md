# Project 2 Housing Price Prediction

## Problem Statement

I was given a data set for the housing values in Ames Iowa and tasked with figuring out a way to perdict the potential sale prices of houses using data with known sale prices.

The data will be presented to the Ames city government to try and help them make redevelopment decision for the city while trying to avoid the issues of displacement or gentrification.

## Summary

Things to look at in this report.

- taking in the data and cleaning it
- creating visuals to try and understand the data
- pick which features are worth using in a regression model
- figure out what features are also important to the problem which might not all be the same as what is good for the regression model
- how can those features be used in land development decisions
- how is the final model and sale prices important to city planning

## Data Dictionary

|     Feature     | Type | Description |
|:----------------|------|-------------|
| Id              | int |ID number of each house|
| PID             | int |Parcel identification number|
| MS SubClass     | int |The building class|
| MS Zoning       | object |The general zoning classification|
| Lot Frontage    | float |Linear feet of street connected to property|
| Lot Area        | int |Lot size in square feet|
| Street          | object |Type of road access|
| Alley           |  object |Type of alley access|
| Lot Shape       | object |General shape of property|
| Land Contour    | object |Flatness of the property|
| Utilities       | object |Type of utilities available|
| Lot Config      | object |Lot configuration|
| Land Slope      | object |Slope of property|
| Neighborhood    | object |Physical locations within Ames city limits|
| Condition 1     | object |Proximity to main road or railroad|
| Condition 2     | object |Proximity to main road or railroad(if second is present)|
| Bldg Type       | object |Type of dwelling|
| House Style     | object |Stlye of dwelling|
| Overall Qual    | int |Overall material and finish quality|
| Overall Cond    | int |Overall condition rating|
| Year Built      | int |Original construction date|
| Year Remod/Add  | int |Remodel date|
| Roof Style      | object |Type of roof|
| Roof Matl       | object |Roof material|
| Exterior 1st    | object |Exterior covering on house|
| Exterior 2nd    | object |Exterior covering on house (if more than one material)|
| Mas Vnr Type    | object |Masonry veneer type|
| Mas Vnr Area    | float |Masonry veneer area in square feet|
| Exter Qual      | object |Exterior material quality|
| Exter Cond      | object |Present condition of the material on the exterior|
| Foundation      | object |Type of foundation|
| Bsmt Qual       | object |Height of the basement|
| Bsmt Cond       | object |General condition of the basement|
| Bsmt Exposure   | object |Walkout or garden level basement walls|
| BsmtFin Type 1  | object |Quality of basement finished area|
| BsmtFin SF 1    | float |Type 1 finished square feet|
| BsmtFin Type 2  | object |Quality of second finished area (if present)|
| BsmtFin SF 2    | float |Type 2 finished square feet|
| Bsmt Unf SF     | float |Unfinished square feet of basement area|
| Total Bsmt SF   | float |Total square feet of basement area|
| Heating         | object |Type of heating|
| Heating QC      | object |Heating quality and condition|
| Central Air     | object |Central air conditioning|
| Electrical      | object |Electrical system|
| 1st Flr SF      | int |First Floor square feet|
| 2nd Flr SF      | int |Second Floor square feet|
| Low Qual Fin SF | int |Low quality finished square feet (all floors)|
| Gr Liv Area     | int |Above grade (ground) living area square feet|
| Bsmt Full Bath  | float |Basement full bathrooms|
| Bsmt Half Bath  | float |Basement half bathrooms|
| Full Bath       | int |Full bathrooms above grade|
| Half Bath       | int |Half baths above grade|
| Bedroom AbvGr   | int |Number of bedrooms above basement level|
| Kitchen AbvGr   | int |Number of kitchens|
| Kitchen Qual    | object |Kitchen quality|
| TotRms AbvGrd   | int |Total rooms above grade (does not include bathrooms)|
| Functional      | object |Home functionality rating|
| Fireplaces      | int |Number of fireplaces|
| Fireplace Qu    | object |Fireplace quality|
| Garage Type     | object |Garage location|
| Garage Yr Blt   | float |Year garage was built|
| Garage Finish   | object |Interior finish of the garage|
| Garage Cars     | float |Size of garage in car capacity|
| Garage Area     | float |Size of garage in square feet|
| Garage Qual     | object |Garage quality|
| Garage Cond     | object |Garage condition|
| Paved Drive     | object |Paved driveway|
| Wood Deck SF    | int |Wood deck area in square feet|
| Open Porch SF   | int |Open porch area in square feet|
| Enclosed Porch  | int |Enclosed porch area in square feet|
| 3Ssn Porch      | int |Three season porch area in square feet|
| Screen Porch    | int |Screen porch area in square feet|
| Pool Area       | int |Pool area in square feet|
| Pool QC         | object |Pool quality|
| Fence           | object |Fence quality|
| Misc Feature    | object |Miscellaneous feature not covered in other categories|
| Misc Val        | int |$Value of miscellaneous feature|
| Mo Sold         | int |Month Sold|
| Yr Sold         | int |Year Sold|
| Sale Type       | object |Type of sale|
| SalePrice       | int |Property's sale price in dollars|

## Information from Data

The data had a lot of missing values to deal with.  For some of the columns they were mostly missing and I dropped those.  Some were simple numeric values like bathrooms so I set those to 0 for the missing.  Other columns were categories that gave value descriptions like good so I set the missing in those to NA as a placement value to signify no information. The final missing values were in columns that had numeric values I set to the mean of the column.

Two of the houses in the data were rather extreme outliers.  They were large houses that sold for a low price. I dropped those to create my model.

Using a heatmap and correlations I found some of the most likely features to model.  I also set up some new columns to simplify the data and improve the model.
Features
- Overall Quality
- Above ground square footage
- Garage square footage
- Basement square footage
- Year Remodel
- Neighborhood
New Columns
- Above ground bathroom column that combined the full and half bath above ground columns
- Basement bathroom column that combined the full and half bath basement columns
- A ratio for above ground bathrooms divided by rooms as this ratio can have an affect on the sale price
- A interaction column between the total above ground square footage and the number of rooms as livable space can be an important factor on value

I also found that the sale prices were heavily skewed so to try and create a more normal distribution for modeling I did a log transform on the sale price column.

Using this information I created a regression model to predict sale prices on new data.

Part of this project was a Kaggle submission.  I used the same features but had to add the outliers back in to the data as I needed the correct number of rows when predicting the sale values for the kaggle contest.   This means the model for the contest was not quite as good as the outliers created a higher variance.


## Conclusions

Using the data I have found correlations of interest that show what parts of a house are important to the sale price. These can include the overall quality, the square footage, the number of rooms, and the neighborhood. Using these features and others I created a model to predict the sale price of others houses in Ames Iowa.

This model will allow us to predict sale prices of houses all over the city. This can give us imformation on neighborhood values and the possible locations of investment and redevelopment. The knowledge can also allow us to make smart decision about new development so that we avoid issues with gentrification or displacement of the people living in those neighborhoods.

We can use infomation from the data like the mean value of houses in each neighborhood or the average year that houses were remodeled in those neighborhoods for comparison. These comparisons can be used to pinpoint neighborhoods of interest for investment but also give an idea of the local home values. With that information we can insure that development in the area will include affodable housing.


## What Next?

- Seeing if other values might have an effect on the model like the lot that the house is on or side features 
- using some more regularization techniques like the lasso or ridge on the data
- looking into what other factors might effect housing values in the lower value neighborhoods
- things like demographics, quality of the area, schools, or crime