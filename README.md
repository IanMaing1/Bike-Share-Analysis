# Bike Share Analysis


### Project Overview

The objective of this project was to analyze bike share data for the years 2021 and 2022. The analysis aimed to identify trends in rider activity and sales over these two years. This helped in understanding usage patterns, seasonality, and the overall performance.


<img width="706" alt="image" src="https://github.com/user-attachments/assets/5d59bc55-05b4-4f64-bc58-001150a95727">


### Data Sources

The following files were utilized for the data analysis project:

1. bike_share_yr_0: Contains bike share data for the year 2021. This file includes information on rider activity, environmental conditions, and temporal variables.
2. bike_share_yr_1: Contains bike share data for the year 2022. This file provides similar data as the previous year, allowing for year-over-year comparisons and trend analysis.

### Tools

1. SQL Server: Data cleaning and analysis. [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
2. Power BI: Creating reports and analysis. [Download here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

### Data Analysis

SQL Query
```sql
WITH cte AS (
  SELECT * FROM bike_share_yr_0
  UNION ALL --combining the data in the two files
  SELECT * FROM bike_share_yr_1
)

SELECT
  a.dteday,
  a.season,
  a.yr,
  a.weekday,
  CASE a.weekday
    WHEN 0 THEN 'sun'
    WHEN 1 THEN 'mon'
    WHEN 2 THEN 'tue'
    WHEN 3 THEN 'wed'
    WHEN 4 THEN 'thu'
    WHEN 5 THEN 'fri'
    WHEN 6 THEN 'sat'
  END AS weekday_name,
  a.hr,
  a.rider_type,
  a.riders,
  b.price,
  b.COGS,
  (a.riders * b.price) AS revenue,
  (a.riders * b.COGS) AS total_cost,
  ((a.riders * b.price) - (a.riders * b.COGS)) AS profit
FROM cte a
LEFT JOIN cost_table b
ON a.yr = b.yr;
```
