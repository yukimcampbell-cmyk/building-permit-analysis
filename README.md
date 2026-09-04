# Vancouver Building Permit Analysis
An end-to-end data analysis project investigating operational and business questions around Vancouver's building permit processing, construction investment, and geographic activity over time.

Overview of workflow: Business Questions → Data Preparation → SQL Analysis → Findings → Visualization

## Tools & Technologies
- Python: data cleaning, transformation, exploratory analysis
- Pandas: data manipulation
- SQL: aggregation, filtering, CTEs, window functions
- Tableau: interactive dashboard and KPI development

## Dataset
I used the Vancouver Open Data REST API to programmatically retrieve the Building Permit dataset. The dataset contains building permit records from 2017–2026, including information on permit processing times, project values, property use, and geographic areas.

## A. Business Questions

**1. Where is construction activity concentrated?**

- Identifying areas with high volumes of construction activity could help highlight potential areas of focus for future investigation.

**2. Which specific property-use categories have the longest average processing times?**
  
- Identifying property-use categories with longer processing times can help highlight areas where permitting processes may require additional time or operational attention.
  
**3. Do larger projects take longer to process?**

- Understanding whether project scale is associated with longer processing times can help identify whether larger projects may require additional review or operational resources.
    
**4. How has construction activity changed over time?**

- Tracking construction activity over time provides insight into changes in development activity and the overall scale of construction in Vancouver.
  
**5. Are certain geographic areas associated with longer permit processing times?**

- Identifying geographic areas with consistently longer processing times can help highlight potential operational bottlenecks and areas that may warrant further investigation.

**6. Which geographic areas had the highest construction investment each year?**
  
- Understanding where construction investment is concentrated can help identify geographic areas experiencing the greatest levels of development activity and how these areas change over time.

These questions are investigated and analyzed using SQL queries in Step C: SQL Analysis.

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

Finding: Downtown had the highest number of total permits at 7384 permits, with Kensington-Cedar Cottage in second with 3150 permits. The geographic area with the lowest number of permits was South Cambie with 667.

### 2. Which specific property-use categories have the longest average processing times?
Grouped building permits by specific property use category and calculated the average processing times for each category. Since some categories had very few records, a minimum threshold of 20 permits was used to reduce the influence of small sample sizes on the average processing times.

Finding: Average processing times varied substantially across the 85 property-use categories. Multiple Dwellings and Parking Garages had the highest average processing time at 487.47 days, while Park or Playground averaged 21.82 days.

### 3. Do larger projects take longer to process?
Analyzed the relationship between project value and permit processing time to determine whether larger construction projects tend to require more time to process. Using CASE WHEN, each permit was sorted into three categories (Small, Medium, Large) based on project value.

Finding: Large projects had the longest processing time at 172.9 days, followed by Medium projects at 115.6 days and Small projects at 65.77. This indicates a strong association between project value and permit processing times.

### 4. How has construction activity changed over time?
Analyzed permit activity and project values across the years to identify trends in construction investment and volume over time.

Finding: Total project value varied substantially from year to year, with no clear upward or downward trend from 2017–2025. Total project value declined in 2020 and 2021, although this analysis does not establish whether the COVID-19 pandemic caused the decline. 2026 was excluded from this comparison because the dataset is incomplete for that year.

### 5. Are certain geographic areas associated with longer permit processing times?
Compared average permit processing times across Vancouver's geographic areas using aggregations. Again, since some categories had very few records, a minimum threshold of 20 permits was used to reduce the influence of small sample sizes on the average processing times.

Finding: South Cambie had the longest average permit processing time, while Downtown had the shortest among geographic areas meeting the 20-permit threshold. Interestingly, this contrasts with permit volume in Query 1: Downtown had the highest number of permits, while South Cambie had the lowest.

### 6. Which geographic areas had the highest construction investment each year?
Aggregated total project value by geographic area and year, then used a `RANK()` window function to identify the geographic area with the highest construction investment in each year. Projects with zero or missing project values were excluded.

Finding: Downtown had the highest total investment in 6 of the 9 years from 2017–2025. However, Oakridge had the highest total investment in 2020 and 2021.

## D. Visualization
The Tableau workbook is available in the `tableau/` folder.

