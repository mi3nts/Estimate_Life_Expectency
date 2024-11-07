## Livestock data processing

This document provides a comprehensive overview of the livestock data processing and aggregation pipeline. The livestock data is sourced from Harvard Dataverse for 2010 and 2015, and from FAO for 2020. Detailed sources are provided below:

Data Sources:

2010 Livestock Data: Harvard Dataverse
2015 Livestock Data: Harvard Dataverse
2020 Livestock Data: FAO Livestock Systems

2010 data source:

https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/GIVQ75

2015 data source:

https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/LHBICE

2020 data soruce:

https://data.apps.fao.org/catalog//iso/9d1e149b-d63f-4213-978b-317a8eb42d02


Coordinate System: All datasets use the geographic coordinate system EPSG:4326.  Both livestock coordinate and shapefiles coordinates are aligned for this data aggregations.

Resolution: The data processing was carried out at a spatial resolution of 0.0083333 degrees (approximately 1 km at the equator), with aggregation to 0.083333 degrees (approximately 10 km at the equator) for distribution. This multi-scale approach accounts for spatial variability in data resolution, enhancing the accuracy of livestock distribution analysis. [Source: Harvard Dataverse documentation for livestock datasets]

Data Processing Steps
Data Extraction and Interpretation:

For 2010 and 2015 datasets, each pixel’s Digital Number (DN) value represents the total number of livestock within that pixel’s geographical extent. Therefore, the DN values directly correspond to livestock counts for these years.
For the 2020 dataset, however, the DN value represents livestock density (livestock per square kilometer). To convert this to absolute livestock counts, each pixel's DN value is multiplied by its area in square kilometers, calculated based on the pixel's geographic size.
Handling No-Data Values:

Each dataset includes specific no-data indicators (DN values representing missing or invalid data) as documented in the metadata. These no-data values are identified and excluded during processing to ensure that only valid livestock counts are included in the analysis.
Geospatial Masking and Boundary Definition:

U.S. county boundaries were obtained from the U.S. Census Bureau’s county shapefiles. These boundaries were used to mask the datasets, restricting the data collection to within the boundaries of the United States.
For each livestock dataset, the U.S. county shapefile was applied as a mask, ensuring that only livestock counts within the continental U.S., Alaska, and Hawaii were included.
Aggregation at Different Administrative Levels:

County-Level Aggregation: For each county, pixel-level DN values were summed to obtain the total livestock count per county. Each pixel within a county boundary contributes to the aggregate count for that specific county.
State-Level Aggregation: Using a similar approach, livestock data was aggregated at the state level by applying a state shapefile as a mask and summing pixel values within each state boundary.
ZIP Code-Level Aggregation: ZIP code-level aggregation was also performed by using a ZIP code shapefile as a mask. This provides an additional layer of granularity for data analysis.
Verification and Validation:

Multiple validation checks were performed throughout the data processing to ensure accuracy. Visual checks were conducted at various stages to compare the output against the original dataset’s visual representation, ensuring that spatial distribution patterns were preserved.
For county data, totals were compared with expected patterns to verify that data aggregation aligned correctly with each administrative boundary.
Direct Pixel-Level Verification:

To verify the accuracy of the data extraction, a subset of pixel-level data was processed directly without aggregation, enabling visual comparison with the original rasters. This step confirmed that livestock counts and densities were being read and processed correctly for each year.
Visualization:

Visualizations were generated at multiple stages to validate data integrity and alignment. Various scaling methods were applied to accommodate different ranges of livestock densities, ensuring that high-density areas were distinguishable in the output maps.
Final Output
The processed livestock data is aggregated at three administrative levels:

State-Level: Aggregated total livestock count by state.
County-Level: Aggregated total livestock count by county.
ZIP Code-Level: Aggregated total livestock count by ZIP code.
Additionally, a direct pixel-based dataset was created, providing livestock counts and densities at each individual pixel, allowing for more granular analysis.

Each output dataset is stored in CSV format, with columns indicating latitude, longitude, and livestock counts for each livestock type (e.g., chicken, cattle, pig) across the years 2010, 2015, and 2020. The 2020 data specifically includes adjustments for density-to-count conversion, and all datasets maintain consistency in coordinate systems and no-data handling.

This processed dataset serves as a comprehensive resource for analyzing livestock distribution trends across multiple years at varying administrative levels.


## Life Expectancy and Livestock data processing 

This document outlines the steps taken to merge livestock data with life expectancy data at the county level, creating a comprehensive dataset that is well-prepared for machine learning (ML) applications. The primary objective of this work is to align the datasets in a structured format, enabling exploratory data analysis and machine learning, with a focus on understanding trends and potential correlations between livestock density and life expectancy at a granular level.

Data Sources:
Life Expectancy Data (2000-2019)

Source: IHME Data - United States Causes of Death and Life Expectancy by County, Race, and Ethnicity
This dataset provides life expectancy data at the county level, broken down by race, ethnicity, and other demographic factors. Data is structured annually from 2000 to 2019 and is identified by unique county FIPS codes.
Livestock Data (2010, 2015, and 2020)

Life Ex data set
https://ghdx.healthdata.org/record/ihme-data/united-states-causes-death-life-expectancy-by-county-race-ethnicity-2000-2019

2010 data source:

https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/GIVQ75

2015 data source:

https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/LHBICE

2020 data soruce:

https://data.apps.fao.org/catalog//iso/9d1e149b-d63f-4213-978b-317a8eb42d02
The livestock data includes various livestock types (e.g., cattle, chickens, pigs) across multiple years. It is geospatially structured with county-level granularity and includes the Digital Number (DN) for each pixel, representing livestock counts (2010 and 2015) or density (2020). All datasets are provided in the EPSG:4326 coordinate system.
Data Processing and Transformation Steps:
Transformation of Livestock Data:

Data Format Transformation:
The livestock dataset was restructured into a uniform, followable format to facilitate merging with life expectancy data. This included aggregating livestock counts at the county level using the county FIPS code as the unique identifier.
Handling Density Data for 2020:
For 2020, the DN values represent livestock density (number per square kilometer) rather than raw counts. Therefore, each DN value was converted to livestock count by multiplying it by the pixel area in square kilometers.
No-Data Handling:
The livestock datasets contain specific no-data values, which were removed based on metadata information for each year. This ensures that only valid data is included in the merged dataset.
Aggregation and Summing:
For each year, pixel values within each county were summed to derive total livestock counts. This was repeated for each livestock type (e.g., cattle, chickens, pigs) to ensure that data was available in a structured manner for machine learning applications.
Preparation of Life Expectancy Data:

Alignment with County FIPS:
The life expectancy dataset, which spans 2000-2019, uses county FIPS codes for unique identification. This key was aligned with the livestock dataset for accurate merging.
Data Transformation:
Life expectancy data was transformed and aggregated as necessary to match the time intervals of the livestock data. For example, if livestock data was available every five years (2010, 2015, and 2020), the life expectancy data was filtered or interpolated to align with these years.
Yearly Data Verification:
Several checks were performed at each step to verify that the transformations were accurate and that no data was lost during aggregation.
Merging Datasets:

Joining by FIPS Code:
Both datasets were merged based on the unique FIPS code for each county. This allowed for a precise match between life expectancy values and livestock counts in each county.
Yearly Alignment:
The merged dataset was structured to maintain a consistent time-series format, aligning livestock and life expectancy data by year. This alignment ensures that each county has livestock and life expectancy data for each available year, facilitating temporal analysis.
Data Validation:
After merging, multiple validation checks were conducted to ensure that data points were correctly aligned across years and that values were reasonable. This included cross-checking a sample of counties to ensure that livestock totals and life expectancy values were accurately represented.
Preliminary Machine Learning Experiments:

Initial Machine Learning Models:
Some basic machine learning models (e.g., linear regression, decision trees) were applied as exploratory analyses. These initial experiments aimed to test the predictive capability of livestock data for estimating life expectancy trends and to identify potential data transformations needed for more robust modeling.
Focus on Data Preparation:
The primary focus of this stage was on dataset preparation and not on extensive model building. As a result, the models were intended as preliminary checks to validate the dataset’s structure and quality rather than to provide actionable insights. Advanced machine learning work is planned as a subsequent step, now that the dataset is verified.
Final Dataset Structure:

The final merged dataset includes columns for:
County FIPS Code: Unique identifier for each county.
Year: Year of the data point (aligned for livestock and life expectancy).
Life Expectancy Metrics: Life expectancy values, with breakdowns by race and ethnicity where available.
Livestock Counts: Total counts for each livestock type (cattle, chickens, pigs, etc.) for each year.
Additional Coordinates: Latitude and longitude were retained where relevant for geospatial analyses.
This dataset is now structured to facilitate both machine learning applications and detailed exploratory data analysis. It serves as a unified source for studying correlations between livestock density and public health indicators at the county level.
Visual Validation and Scaling:

Scaled Visuals: Visualizations were created using various scaling methods to accurately represent the distribution of livestock and life expectancy data across counties. These visual checks helped verify that data was aligned correctly and that aggregation methods maintained geographic and demographic fidelity.
Map Overlays: Additional maps with state and county boundaries were layered over livestock data to confirm the spatial accuracy of the merged dataset.
Summary
This data preparation and merging process has produced a robust, well-structured dataset that combines livestock counts and life expectancy metrics across U.S. counties from 2010 to 2020. By aligning livestock and life expectancy data with consistent FIPS codes and annual time stamps, this dataset is ready for advanced analysis, including predictive modeling and machine learning. Further machine learning efforts are planned, with the prepared dataset providing a reliable foundation for exploring the relationship between livestock density and life expectancy at a fine spatial and temporal scale.

