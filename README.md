# Vancouver Building Permit Analysis
An end-to-end data analysis project examining building permit activity in Vancouver, with a focus on business and operational questions involving permit processing times, construction investment, and geographic patterns, all over time.

Overview of workflow: Pre-Analysis Questions -> Data Preparation -> Analysis -> Insight -> Visualization

## Tools & Technologies
- Python: data cleaning, transformation, some analysis
- Pandas: data manipulation
- SQL: aggregation, filtering, CTEs, window functions
- Tableau: interactive dashboard w/ KPIs development

## Dataset
I used a REST API to retrieve the Building Permit dataset from Vancouver Open Data. 
This data includes information on building permit records from 2017-2026.

## A. Pre-Analysis Questions
**1. Where is construction activity concentrated?**
- Identifying areas with high volumes of construction activity could help highlight potential areas of focus for future investigation.
**2. Which specific property-use categories have the longest average processing times?**
- Identifying property-use categories with longer processing times can help highlight areas where permitting processes may require additional time or operational attention.
**3. Do larger projects take longer to process?**
**4. How has construction activity changed over time?**
- Tracking construction activity over time provides insight into changes in development activity and the overall scale of construction in Vancouver.
**5. Are certain geographic areas associated with longer permit processing times?**
  - Identifying geographic areas with consistently longer processing times can help highlight potential operational bottlenecks and areas that may warrant further investigation.
**6. Which geographic areas had the highest construction investment each year?**
- Understanding where construction investment is concentrated can help identify geographic areas experiencing the greatest levels of development activity and how these areas change over time.

These questions are investigated and analyzed using SQL queries in step 3.

## B. Data Preparation 
Some key steps in data preparation:
- Inspecting data for missing values
- Removing irrelevant or invalid records
- Converting date fields into useable date-time formats
- Standardizing categorical variables
- Extracting geographic coordinates for mapping and visualizations
- Identifying outliers in variables and making the decision to remove or keep them
- Preparing the cleaned dataset for SQL analysis and Tableau visualization
  
## C. SQL Analysis + Findings
SQL queries were used to explore the questions in the first step.

### 1. Where is construction activity concentrated?
Compared total permit count across Vancouver's geographic areas using aggregations for total permits, as well as total project value, and average project value for each category.

Results: Downtown had the highest number of total permits at 7384 permits, with Kensington-Cedar Cottage in second with 3150 permits. The geographic area with the lowest number of permits, and the lowest construction activity, was South Cambie with 667.

### 2. Which specific property-use categories have the longest average processing times?
Grouped building permits by specific property use category and calculated the average processing times for each category. Since some categories had very few rows of data, the minimum for the number of total permits was set to 20 to prevent inaccurate representations when calculating average.

Results: There was a large range of average processing times over the 85 property-use categories. For example, the Multiple Dwellings and Parking Garages category had the highest average processing time at 487.47 days, whereas the Park or Playground	category had an average time of 21.82.

### 3. Do larger projects take longer to process?
Analyzed the relationship between project value and permit processing time to determine whether larger construction projects tend to require more time to process. Using CASE WHEN, each permit was sorted into three categories (Small, Medium Large) based on project value.

Results: Large projects had the longest processing time at 172.9 days, followed by Medium projects at 115.6 days and Small projects at 65.77. This suggests a strong relationship between project value (size) and permit processing times.

### 4. How has construction activity changed over time?
Analyzed permit activity and project values across the years to identify trends in construction investment and volume over time.

Results: From 2017-2025, there seems to be little relationship between year and total project value. There is a decline in 2020 and 2021 which could be attributed to the COVID-19 pandemic but no conclusions can be drawn. Data for 2026 is incomplete so it can be ignored for this purpose.

### 5. Are certain geographic areas associated with longer permit processing times?
Compared average permit processing times across Vancouver's geographic areas using aggregations. Again, since some categories had very few rows of data, the minimum for the number of total permits was set to 20 to prevent inaccurate representations when calculating average.

Results: The geographic area with the longest permit processing times was South Cambie and the area with the shortest processing times was Downtown. This matches up with Query A, which showed that Downtown had the highest construction activity and South Cambie, the lowest.

### 6. Which geographic areas had the highest construction investment each year?
Aggregated total project value by geographic area and year, then used a `RANK()` window function to identify the geographic area with the highest construction investment in each year. Projects with zero or missing project values were excluded.

Results: Downtown had the highest total investment for 7 out of the 10 years from 2017-2026. However, Oakridge had the highest total in 2020 and 2021.
