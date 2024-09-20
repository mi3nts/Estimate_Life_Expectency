This folder consists of the Life expectency data from IHME. The link to the website is:: https://ghdx.healthdata.org/record/ihme-data/united-states-causes-death-life-expectancy-by-county-race-ethnicity-2000-2019

After you go the website, click on "Files (76)". Then download the second file "Life expectancy estimates 2000-2019, both sexes [CSV]. You will need to register to download the data. The zip file will consist of 20 items. Keep all the 20 files inside the folder "Life_Expectency_Data". There are several columns in the csv file. The meaning of the columns can be found in the same website in the file "Data Release Information Sheet". 

The life expectency is given as age groups and by classification such as total, latino, Black, White etc. at the spatial level of the country, state and county. Meaning, life expectency of age group <1 year old, 1 to 4 year old, 5 to 9 year old and so on; of variety of race_name. There are altogether 19 age groups and 7 race_name.

We will be estimating the Total life expectency of age groups <1 year old (or superficially speaking life expectency at birth).  

The code to extract the total life expectency of age groups < 1 year old of a single year and of all the years is given in the notebook: Single_Year.ipynb and All_Years.ipynb respectively.
