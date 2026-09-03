# Vancouver Building Permit Analysis
An end-to-end data analysis project examining building permit activity in Vancouver, with a focus on business and operational questions involving permit processing times, construction investment, and geographic patterns, all over time.

Overview of workflow: Business questions -> Data Preparation -> Analysis -> Insight -> Visualization

## Tools & Technologies
- Python: data cleaning, transformation, some analysis
- Pandas: data manipulation
- SQL: aggregation, filtering, CTEs, window functions
- Tableau: interactive dashboard w/ KPIs development

## 1. Business Questions
A. Where is construction activity concentrated?
B. Which specific property-use categories have the longest average processing times?
C. Do larger projects take longer to process?
D. How has construction activity changed over time?
E. Are certain geographic areas associated with longer permit
F. Which geographic areas had the highest construction investment each year?

These questions are investigated and analyzed using SQL queries in step 3.

## 2. Data Preparation 
Some key steps in data preparation:
- Inspecting data for missing values
- Removing irrelevant or invalid records
- Converting date fields into useable date-time formats
- Standardizing categorical variables
- Extracting geographic coordinates for mapping and visualizations
- Identifying outliers in variables and making the decision to remove or keep them
- Preparing the cleaned dataset for SQL analysis and Tableau visualization
  
## 3. SQL Analysis + Findings
SQL queries were used to explore the questions in the first step.

### A. Where is construction activity concentrated?
- Compared total permit count across Vancouver's geographic areas using aggregations for total permits, as well as total project value, and average project value for each category
- Identifying areas with high volumes of construction activity could help highlight potential areas of focus for future investigation

The results showed that Downtown had the highest number of total permits at 7384 permits, with Kensington-Cedar Cottage in second with 3150 permits. The geographic area with the lowest number of permits, and the lowest construction activity, was South Cambie with 667.

### B. Which specific property-use categories have the longest average processing times?
- Grouped building permits by specific property use category and calculated 

C. Do larger projects take longer to process?
D. How has construction activity changed over time?
E. Are certain geographic areas associated with longer permit
F. Which geographic areas had the highest construction investment each year?
