# Power BI Sales Performance Dashboard (Actual vs Target)

This project is a Power BI dashboard that tracks **Sales Actual vs Sales Target**, **Variance**, **Variance %**, **YTD performance**, and **salesperson-level performance**.  
The goal is to help leaders quickly see whether targets are being met, identify gaps, and spot trends by month and by sales person.

## Preview
https://github.com/JawadNayosh/Powerbi-sales-performance-dashboard/issues/1#issue-3804837602

## Key Insights (Example)
- We met targets for **2 out of 14 months** (based on the current filter context).
- Actual and Target trends can be compared monthly, with quick KPI cards for high-level performance.
- Salesperson table highlights **individual variance %** and trend lines over time.

## Features
- KPI Cards: Total Sales Actual, Total Sales Target, Variance, Variance %, Months Target Reached
- Monthly Actual vs Target chart
- Salesperson performance table (Actual, Target, Variance % + trend sparkline)
- Slicers for Sales Person and Date/Period

## DAX Measures Used (Sample)

Variance =
[Total Sales Actual] - [Total Sales Target]

Variance % =
DIVIDE ( [Variance], [Total Sales Target], 0 )

YTD Sales =
CALCULATE ( [Total Sales Actual], DATESYTD ( 'Calendar'[Date] ) )

YTD Target =
CALCULATE ( [Total Sales Target], DATESYTD ( 'Calendar'[Date] ) )

YTD Variance =
[YTD Sales] - [YTD Target]

YTD Variance % =
DIVIDE ( [YTD Variance], [YTD Target], 0 )

Months Target Reached =
VAR MonthlyTable =
    SUMMARIZE (
        'Calendar',
        'Calendar'[Year],
        'Calendar'[Month],
        "MonthlyActual", [Total Sales Actual],
        "MonthlyTarget", [Total Sales Target]
    )
RETURN
COUNTROWS (
    FILTER ( MonthlyTable, [MonthlyActual] >= [MonthlyTarget] )
)
##Download the .pbix file from this repo.
