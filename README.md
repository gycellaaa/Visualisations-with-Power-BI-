
# Analytics Technique Portfolio

## Assignment details
The task involves analyzing a given dataset to provide insights that will support an upcoming business strategy review.

To assist with this, you have been provided with several datasets containing data about sales, customers, products, stores and sales teams.
Your initial investigation of the dataset revealed the following:

All currency amounts are:
- Recorded in the same currency, and
Have been adjusted for inflation across years.
- Each row in the Sales spreadsheet represents a sale of a Product to a Customer. The sale is made at a Store and delivered from a Warehouse. Each sale lists the Order Quantity (of the Product) sold at an Item Price (the Item Price can vary for each sale). The Total Gross Sale amount is the Order Quantity multiplied by the Item Price. Sales Teams are responsible for arranging the sale.
- There is a Discount Band which applies to each sale. The following discounts are applied depending on the Discount Band. The amount of the Discount is calculated by multiplying the Total Gross Sale by the Discount Band percentage.
Band
% of Gross Sale
NIL
0%
LOWa
1%
MED
2%
HI
5%
 
- The Total Net Sale Amount is the Total Gross Sale minus the Discount.
- Sale Cost is the total costs that have been incurred in completing the sale.
- The Profit is the Total Net Sale minus Sale Cost.
- Each Product has a Category.
- Each Sale has a Customer.

## What to do?
### A. Use PowerBI Desktop to create visualisations that will help to answer each of the following questions:

#### 1. What are the top 3 stores by total net sales amount for each of the years 2021-2022?
#### 2. Are there months in which sales of a particular product any of the states are significantly higher than others?
#### 3. Which sales team has the highest profit margin?
#### 4. Which warehouse(s) should be shut down?
#### 5. Do cities with a higher population have higher profit?

### B. Write an explanation of how your visualisation (or visualisations) addresses each of the questions (i.e., five explanations of no more than 1 page each). 
       
    Include a screenshot of your visualisation(s) for the question and refer to it/them in your explanation.

### C. Write an explanation of your data transformation process. 
    
    It should include details of any changes you make to the structure of the original dataset
     and any additional columns or measures you create to complete the analyses. 

    Please note, this is focused on your data transformation, not the processes for creating your visualisations.
    
*
    [The Raw Data Set CSV link](https://curtin-my.sharepoint.com/:x:/r/personal/21569498_student_curtin_edu_au/Documents/Sales%20Orders.xlsx?d=w475def7f80b64d3aa2981c793f059db9&csf=1&web=1&e=pkHKyO) 




## Analysis to address the respective questions
- [What are the top 3 stores by total net sales amount for each of the years 2021?](#1-what-are-the-top-3-stores-by-total-net-sales-amount-for-each-of-the-years-2021)
- [Are there months in which sales of a particular product in any of the states are significantly higher than others?](#2-are-there-months-in-which-sales-of-a-particular-product-in-any-of-the-states-are-significantly-higher-than-others)
- [Which sales team has the highest profit margin?](#3-which-sales-team-has-the-highest-profit-margin)
- [Which warehouse(s) should be shut down?](#4-which-warehouses-should-be-shut-down)
- [Do cities with a higher population have higher profit?](#5-do-cities-with-a-higher-population-have-higher-profit)

* [The Power BI File link](https://github.com/gycellaaa/Analyics/blob/main/A2_PowerBI.pbix)


## 1. What are the top 3 stores by total net sales amount for each of the years 2021-2022?

* Visualisation

Year 2021

![1. What are the top 3 stores by total net sales amount for each of the year 2021](https://github.com/user-attachments/assets/cd2b6b5d-61fa-45ce-a19b-4916b9469bd4) 


Year 2022

![1.2. What are the top 3 stores by total net sales amount for each of the year 2022?](https://github.com/user-attachments/assets/0f5b6f7f-ad81-4c15-8b4c-676197ff3194)

* Steps

Step 1. Remove non-essential columns from the dataset: specifically, 1.2 lat, 1.2 lng, iso2, iso3, and ID. Note that the ID column does not correspond to stores id.

Step 2.	renamed column 1 = to be stores ID, as data scanned from the Store_ID in the Sales Data as it is appropriate. 
Instead of using the Store ID as reference, it would be more appropriate to transform the Store ID as the City names as it would be easier for stakeholders to understand better the stores represented by the City.

Step 3. Adjust the rest of data types accordingly

Step 4. Add a conditional column to transform the Discount Band to the Discount Band Percentage per the description to change the value of Nil to %, LOW to 1%, MED to 2% and HI to 5%. 

Step 5. To determine the total net sales amount, we first need to compute the Total Gross Sales. I utilize the Custom Column feature for this calculation.

Step 6. Create a column to calculate the Discount band Multiplied with the Total Gross Sales amount. 
Named the column of this multiplication as "Discount Total".
    
    "Discount Total" = Total Gross Sale= [Total Gross Sale] *[Discount Band Percentage]

Step 7. Lastly, calculate the Total Net Sales by subtracting the Discount Total from the Gross Sales across all entries in the table.

The formula to calculate the Total Net Sale(s) amount using DAX expression: 

    Total Net Sales = SUM('Sales Data'[Total Gross Sales]) - SUM('Sales Data'[Discount Total])

* Description 

The visualisation displays a clustered bar chart “Top 3 stores according to their total net sales”, 
as well as a slicer that consists the options of the year 2021 and 2022.
The option for Clustered bar chart for this specific analysis is to mainly promotes comparison of the total net sales made by the different stores. 
Each column’s length corresponds to the net sales amount, and the additonal value indicated by the end of each bar assissts with the precise of the total net sales amount for each store rather than stressing the reader’s eyes to navigate each amount, and instead, focusing on the main insight of the chart.
When one of the slicer’s year option is chosen, it enabels simple comparison of the total net sales made by the three stores within the dedicated year.
With an integrated tooltip as a storytelling function that provides a compact view of the store, net sales and the year when navigating through specific value. Not only is assists with data filter, it provides a straightforward user-friendly interface for data exploration. It functions to tell a story and guide the reader for quick data-driven decison making. 

* Insight 

The three stores of the year 2021 is:  Canberra with net sales of 294k, Lanceston store with net sales of 302k, Toowomba with net sales of 298k.

* Assumption

I have chosen to refer store names by their respective cities, as each Store ID corresponds to a specific city in the Store data. This approach enhances readability and facilitates a more detailed analysis of total net sales attributed to each store within a city. By using city names, we can more easily assess and compare performance metrics across different locations.

## 2. Are there months in which sales of a particular product in any of the states are significantly higher than others?

    Given the complexity of the visual, which encompasses multiple datasets, 
    I have opted to present a focused scenario analysis for efficiency and clarity.

* Visualisation 

![2. Are there months in which sales of a particular product in  any of the states are significantly higher than others?](https://github.com/user-attachments/assets/7b8d83f7-8ac2-4aee-bb14-b406d208ad3c)

* Steps 

Step 1. Renamed the column "admin_name" to "States" for enhanced clarity regarding the geographic data represented.

Step 2. Introduced a new column to capture the Total Net Sale for each product, facilitating the calculation of Sales Median.
 It is important to differentiate this from the overall Total Net Sale, which aggregates individual product net sales rather than encompassing the cumulative net sales and total discounts across all products.

    Total Net Sale = [Total Gross Sales]-[Discount Total]

Step 3. Created a new DAX expression for the Sales Median 

    Sales Median = CALCULATE(MEDIAN('Sales Data'[Total Net Sale]))

* Description 

The visualization features a line and clustered column chart titled “Total Net Sales of Product by Month,” designed to analyze the monthly sales performance of a specific product across various states and identify significant deviations from overall net sales trends.
The choice of a line and clustered column chart is effective to illustrate both the temporal sales trends and the comparative metrics over months.

On the X-axis, the months of the year are plotted sequentially, while the Y-axis quantifies the Total Net Sales in monetary terms. Additionally, a secondary Y-axis for the line graph represents the median net sales of the product, facilitating direct comparisons between individual monthly sales performance and the overall sales performance throughout the year. It enables a comprehensive analysis of product performance relative to total sales across all observed years.

The dashboard features a Year slicer that enables users to filter and display month ranges within both line and column charts. Additionally, there is a Product Name slicer that allows users to narrow on specific products of interest. Finally, a State slicer provides to navigate through various geographical regions.

Furthermore, the tooltip functionality is implemented to indicate detailed information, including the month, product name, and total sales, as users interact with specific points on the chart after applying their slicer selections.

* Assumption

In utilizing the Total Net Sales median, we aim to provide stakeholders with a comprehensive basis for analyzing a product's performance over a specified year. This involves comparing a specific month’s Total Net Sales with the overall performance throughout the rest of that year as well as against historical data from prior years. 

Due to the ambiguity surrounding the specific year for the requested months, I opted to implement a slicer feature. This allows for the selection of months within a designated year, facilitating a more thorough and further insights of the whole data.

* Insight 

Consider an analysis focusing on the net sales of Accessories within Queensland for the year 2022, alongside a comparative assessment against Bar Tools sales. 

The findings reveal that there were no recorded sales of Accessories from January through May. Notably, December demonstrated a robust sales performance, generating $10.3k, significantly outperforming other months by $8.6k. In contrast, November's sales amounted to $5.6k, indicating a shortfall of $2.6k compared to the rest of the month’s performance. 

Furthermore, sales data indicated that Bar Tools experienced higher sales volumes than Accessories in the months of June, July, and October. This comparative analysis highlights the varying performance dynamics between the two product lines within the specified timeframe.


## 3. Which sales team has the highest profit margin?

* Visualisation

![3. Which sales team has the highest profit margin?](https://github.com/user-attachments/assets/d40fd3e5-7367-413e-aaa2-a202ca7f7860)

* Steps

Step 1. Followed by the DAX expression to calculate the average profit margin for each sales team 

    Average Profit Margin = AVERAGEX('Sales Data', 'Sales Data'[Profit Margin])

Step 2.	Create a DAX expression for Rank per the average profit margin:

    Rank by Profit Margin = RANKX(ALL('Sales Team'), [Average Profit Margin],,DESC)


* Desctiption

The visualization presents the "Sales Team Ranking," indicating columns for Sales Team, Rank by Profit Margin, and Average Profit Margin. This Table was selected due to its simplicity and clarity in addressing the analytical question at hand, which requires minimal data complexity.

The visual enables readers to capture the performance hierarchy of each sales team based on their profit margin percentages corresponding to the respective Total Net Sales. The color-coded rows facilitate immediate recognition of corresponding ranks and profit margins. The Rank column is organized in descending order to provide a straightforward presentation of each sales team’s performance aligned with their profit margins.

* Assumption

For the calculation of Profit Margin, I’ve utilized the standard expression: (Total Net Sales – Sale Cost) / Total Net Sales. This widely accepted equation accurately reflects the profit margin.

* Insight 

The analysis indicates that the Jonathan Hawking sales team leads the ranking with an impressive profit margin of 38%. Conversely, the lowest-performing team is Shaw Wallace, which occupies the 28th rank with a profit margin of just 35.5%.


## 4. Which warehouse(s) should be shut down?

* Visualisation

![4. Which warehouse(s) should be shut down?](https://github.com/user-attachments/assets/c9e6498e-7567-47fc-9243-8a19cb62e7d0)

* Steps

Step 1: Begin by removing the DeliverDate and ShipDate columns from the Store dataset, as they are not pertinent to the scope analysis.

Step 2.	Applied DAX expression to calculate the Total Profit        

    Total Profit = SUM('Sales Data'[Net Sales Amount]) - SUM('Sales Data'[Sale Cost])


* Description

The visualization presents a Stacked Column chart illustrating the Total Profit alongside the Total Net Sales attributed to each warehouse. The use of a stacked column format allows for a clear comparative analysis of these two critical metrics as decision-making factors in the potential closure of a warehouse, based on the available datasets. While profit is a primary focus, Total Net Sales are also essential for evaluating each warehouse's overall performance.

On the X-Axis, the chart displays Warehouse codes that correspond to their respective Net Sales and Profit figures. The Y-axis quantifies both Total Net Sales and Total Profit. The darker green bars represent Total Net Sales for each Warehouse, while the lighter green bars indicate Total Profit. This dual representation enables stakeholders to assess whether to prioritize profit margins or sales volume when considering warehouse closures, facilitating a more informed decision-making process.

* Insight 
If the stakeholder prioritizes profitability, the analysis suggests that warehouse WARE-NBV1002 should be the candidate for closure. However, it is important to note that this recommendation is based on limited data; in practice, a comprehensive evaluation would incorporate additional factors to fully assess the viability of each warehouse.

## 5. Do cities with a higher population have higher profit?

* Visualisation

![5. Do cities with a higher population have higher profit?](https://github.com/user-attachments/assets/139313c7-5cb0-4d4b-b2dd-dbaf08d5cbee)

* Step

    (Though not directly related to data transformation, the visualisation adds up to create the relevant data). 
 
 Step 1. Using the R Script visual to add a line trend & precise coordinates: 

    library(ggpubr)
    ggscatter(dataset, x = "population", y = "Total Profit",
    add = "reg.line", conf.int = TRUE) +
    stat_cor(label.x = 1000000, label.y = 300000, size = 6, color = "red") +
    stat_regline_equation(label.x = 3000000, label.y = 300000, size = 6, color = "blue",
    aes(label = paste(..eq.label.., sep = "~~~")))



* Description

The initial chart presents a Correlation Plot generated using R-script, which allows for the inclusion of a correlation line to facilitate the visual representation of relationships. The correlation coefficient is R = -0.18, p = 0.35, to indicate a weak and statistically insignificant relationship between Population and Total Profit. This prompts the question: is there a notable trend where increases in Profit correspond to increases in Population?
Furthermore, the regression line is represented by the equation y = 24000-0.002x, which will be useful for predictive analyses if additional data becomes available.

The accompanying second chart features red shading that indicates the density of Total Profit against Population, visually assessing the presence or absence of any correlation. 
The X-axis represents Total Profits, while the Y-axis represents Population.

* Insight

Given the correlation coefficient of R = -0.18 and p = 0.35, it is evident that there is no correlation between City and Population, as the negative value of R suggests a lack of relationship.


## Acknowledgments  
Special thanks to [Danny Toohey] for providing the assignment details and guidance.  
