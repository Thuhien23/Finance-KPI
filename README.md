# Overview
This repository contains data and analysis scripts for performing data cleaning, exploratory data analysis (EDA), and performance calculations using Power BI. The dataset consists of four main tables:

**Actual**: Contains monthly sales data for each salesperson.

**Calendar**: Provides date-related information.

**dimPeople**: Describes salespeople and their teams.

**Targets**: Specifies monthly sales targets for each salesperson.

# Data Cleaning and Transformation Steps
### Actual Table
**Step 1**: Use the first row as headers.

**Step 2**: Format the "Month" columns as dates.

**Step 3**: Unpivot all columns except "Sales Person".

### Calendar Table
**Step 1**: Add additional columns for "Year", "Month", and "Month Name".

### Targets Table
**Step 1**: Use the first row as headers.

**Step 2**: Format the "Month" columns as dates.

**Step 3**: Unpivot all columns except "Sales Person".

### Applying Changes
### Close and Apply: Ensure all transformations are applied to the respective tables.
### Check Data Model: Validate the data model for correctness and completeness.

## Performance Calculations using DAX
1. **Total Sales Actual:** SUM(Actual[Sales]) // Calculates the total actual sales across all salespeople

2. **Total Sales Target:** SUM(Targets[Sales]) // Calculates the total sales targets across all salespeople

3. **Variance:** [Total Sales Actual] - [Total Sales Target] // Calculates the difference between total actual sales and total sales targets

4. **Variance %:** DIVIDE([Variance], [Total Sales Target]) // Calculates the percentage variance between actual and target sales

5. **YTD Sales Actual:** CALCULATE([Total Sales Actual], DATESYTD('Calendar'[Date])) // Calculates year-to-date actual sales using the current date context

6. **YTD Sales Target:** CALCULATE([Total Sales Target], DATESYTD('Calendar'[Date])) // Calculates year-to-date sales targets using the current date context

7. **YTD Variance:** [YTD Sales Actual] - [YTD Sales Target] // Calculates year-to-date variance between actual and target sales

8. **YTD Variance %:** DIVIDE([YTD Variance], [YTD Sales Actual]) // Calculates year-to-date percentage variance between actual and target sales

9. **Variance Pct Label:** // Generates a formatted label indicating variance direction (up or down)

> var up = "🟢"

> var down = "🔴"

> var formatted_var_pct = FORMAT(ABS([Variance %]), "0.0%")

> RETURN

>formatted_var_pct & " " & IF([Variance %] > 0, up, down)
    
*This calculation formats the variance percentage and adds a visual indicator (green for positive variance, red for negative).*

10. **Trend Chart Title:** // Generates a dynamic title for trend charts based on achieved months vs total months

> var month_count = COUNTROWS('Calendar')

> RETURN

   >"We met targets for " & [Months Target Reached] & " out of " & month_count & " months"
    
*This calculation creates a title indicating how many months met the sales target out of the total months available in the calendar.*

![image](https://github.com/Thuhien23/Finance-KPI/assets/96719464/110a03d9-e743-46cf-ab4d-247d6e700339)
