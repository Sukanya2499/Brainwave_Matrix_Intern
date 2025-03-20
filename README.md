# Brainwave_Matrix_Intern
![Screenshot (197)](https://github.com/user-attachments/assets/aaa46571-88af-4a1c-903b-a22e12dfa6a6)
Created a different table for measures (Measure Table)
1st Card -> 
•	Total Gross Revenue = SUM('supermarket_sales'[Total]).

•	A line chart of ‘Total Gross Revenue’ vs. ‘Date’ has drawn.

•	To show sales growth or negative growth,
           Revenue Change %(Gross Revenue) = 
           VAR SelectedMonth = SELECTEDVALUE(supermarket_sales[Month]) 
           VAR CurrentMonthRevenue = SUM(supermarket_sales[Total])  
           VAR PreviousMonthRevenue =
           CALCULATE(
           SUM(supermarket_sales[Total]),
           FILTER(
            ALL(supermarket_sales),  
            supermarket_sales[Month] = 
                SWITCH(
                    SelectedMonth,
                    "Feb", "Jan",
                    "Mar", "Feb",
                    BLANK()
                  )
           )
      )
   VAR RevenueChange = CurrentMonthRevenue - PreviousMonthRevenue
   VAR PercentageChange = DIVIDE(RevenueChange, PreviousMonthRevenue, 0)
   VAR FormattedResult = IF(
        NOT ISBLANK(PreviousMonthRevenue),
        FORMAT(PercentageChange, "0.00%") & " | " & FORMAT(RevenueChange, "#,##0"),
        BLANK()
    )
RETURN
FormattedResult


•	To customize the font color of the above DAX ,

Revenue Change Numeric(Gross Revenue)(for Formatting) = 
VAR SelectedMonth = SELECTEDVALUE(supermarket_sales[Month])  
VAR CurrentMonthRevenue = SUM(supermarket_sales[Total])  

VAR PreviousMonthRevenue =
    CALCULATE(
       SUM(supermarket_sales[Total]),
        FILTER(
            ALL(supermarket_sales),  
            supermarket_sales[Month] = 
                SWITCH(
                    SelectedMonth,
                    "Feb", "Jan",
                    "Mar", "Feb",
                    BLANK()
                )
        )
    )

VAR PercentageChange = DIVIDE(CurrentMonthRevenue - PreviousMonthRevenue, PreviousMonthRevenue, 0)

RETURN
IF(NOT ISBLANK(PreviousMonthRevenue), PercentageChange, BLANK())



2nd Card & 3rd Card ->
Similarly two other cards, ‘Total Net Revenue’ & ‘Total Gross Income’ are created.

•	‘Gross Revenue’, ‘Net Revenue’, ‘Gross Income’ are shown based on ‘Product Line’ using a clusted bar chart.
•	Customer type for overall sales is shown using a donut chart.
•	Payment type in cities is shown using stacked bar chart.
•	Average rating of each product line is shown using a donut chart.
Used DAX: Avg Rating = AVERAGE(supermarket_sales[Rating])
•	Based on city and gender, quantity, gross revenue, net revenue and gross income are shown using a matrix visual.
Used DAX: Total Quantity = SUM(supermarket_sales[Quantity]), rest of the measures are already shown previously.



