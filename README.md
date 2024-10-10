# Estimate Life Expectency

This respository consists of the code, data and links to data to estimate the life expectency of age group less than 1 year old in USA.  

The source of the life expectency data is [IHME](https://ghdx.healthdata.org/record/ihme-data/united-states-causes-death-life-expectancy-by-county-race-ethnicity-2000-2019). More about it in the Life_Expectency_Data folder.

The life expectency is estimated using a set of variables from 2 different different sources of data:

1. Livestock Data from the following paper: [Livestock 2010](https://www.nature.com/articles/sdata2018227). More about it in the livestock directory. 

2. Set of demographic data from ACS. More about it in the demographic directory.

All_Years.ipynb notebook extracts the total life expectency of age group less than 1 year old for 20 years of data. 
Single_Year.ipynb extracts the total life expectency of age group less than 1 year old for a single year.

