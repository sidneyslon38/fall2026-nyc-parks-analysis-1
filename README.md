# Analysis of Park Cleaning and Inspection Data from 2025

In this repository, I have merged [Daily Task cleaning records](https://data.cityofnewyork.us/City-Government/Daily-Tasks-Park-Cleaning-Records/kwte-dppd/about_data), [Park Inspection records](https://data.cityofnewyork.us/dataset/Parks-Inspection-Program-Inspections/yg3y-7juh/about_data), and [2020 Census data](https://www.census.gov/) with median incomes for each census tract, to understand if there is a correlation between cleaning and inspection results for New York City parks, and higher or lower income neighborhoods across the city.

Due to the size of the data files required to run this analysis, find all data files in this [Google Drive folder](https://drive.google.com/drive/folders/1zL--3Tq25xFGTQfq8PrOSQOVpeoRCPH7?usp=sharing). Download them, and drag them into an empy "data" folder, nested under "NYC Parks Dept Cleaning Schedule Analysis".

## Methodology

The purpose of this analysis was to determine if there is a trend between median census tract income in New York City, and park conditions. Specifically, the efforts of the Parks Department. 

All of the data analyzed here is publicly available.

The key to this analysis was merging multiple datasets. Daily Task records are extremely long, so first, I matched each "gispropnum" to it's specific park name. Then, I filtered down to only one row per park. Since each row in the Daily Task records is a specific visit, with the number of crew members and hours spent, I gathered averages for each park name across the dataset. 

Once taking a closer look at the newly filtered dataset, I also realized that some parks are extremely large, and some are extremely small. This analysis only looks at parks between 0.1 and 300 acres in size. This includes the majority of parks on the initial list, well beyond what the 25th and 75th percentiles for acreage. However, parks smaller than 0.1 are often not the types of green spaces I am considering for this analysis, and parks above 300 acres are so large, I did not want to skew the data, as these massive green spaces are often cleaned in small sections, touch many more census tracts, and feature many unique spaces that may not be a typical green space.

I also filtered out all playgrounds in the dataset. For the purposes of this analysis, I was only looking at "green spaces" in the truest sense of the word: lawns, running paths, waterfronts, fields, forests, hiking trails, etc.

From there, I merged the filtered park dataset to my census tracts. I used GeoPandas to create a spatial merge, with weighted averages. This means that every census tract polygon that intersected with a park property polygon was included. Weights were based on how much a census tract overlapped. A half-mile buffer around each park polygon was created, to consider the immediately surrounding neighborhood's income. 

## Results

Ultimately, median income and park cleaning tasks held a weak statistical correlation. While there was a slight slope with neighborhood income levels and hours spent cleaning, there are many other factors contributing to park cleanliness that likely weigh heavier than income.

While this may not have been the results I expected, it was a valuable conclusion nonetheless. This analysis shows that the Parks Department attempts to treat every park fairly equal, regardless of its surrounding neighborhood income level. 

Having the average hours spent cleaning, and crew size data is also helpful on a borough-wide level. No park gets, on average, more than 2 hours of cleaning, and with the exception of Staten Island, no more than an average of three crew members at a time. 

PIP inspection data is also included, as a measurement of actual park conditions. The data revealed that cleaning efforts also do not strongly correlate to overall park conditions, which means there are external factors (like park goers) contributing more heavily to negative conditions.

## AI Disclosure

Claude Code was used to help me understand statistical regressions, and walked me through the GeoPandas steps. I would not have known how to conduct a spatial merge without the advice of Claude Code for this analysis. However, it was only used as a learning tool, and for each line of code it recommended, I had it walk me through the steps so that I understand how everything is working. The Jupyter notebook is also heavily annotated, explaining each step.