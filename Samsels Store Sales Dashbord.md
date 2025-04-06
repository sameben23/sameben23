# Samsels Store Sales Dashboard

### Project Overview 
Samsels Store Dashboard is a comprehensive management tool designed to provide valuable insights across six key areas:

- **Summary Metrics**  
  Get a quick snapshot of overall store performance through high-level KPIs.

- **Sales Analysis**  
  Dive into sales data to identify trends, top-performing periods, and areas for improvement.

- **Profit Analysis**  
  Analyze profit margins across different products, categories, and timeframes.

- **Location Analysis**  
  Understand how different store locations or regions contribute to overall performance.

- **Product Analysis**  
  Track the performance of individual products to make informed stocking and pricing decisions.

- **Revenue Trends**  
  Visualize revenue growth and fluctuations over time to guide strategic planning.

Each page offers detailed information to help optimize store operations. With **real-time data visualization**, the dashboard enables:

- Informed decision-making  
- Operational efficiency  
- Enhanced understanding of customer behavior and product success

### Objective
The aim was to help the management of Samsels Store track KPIs in real-time and make data-driven decisions to boost sales and reduce losses

### Data Sources
The data was sourced from "Samsels Store Sales data", an Excel file containing transaction history, customer data, and product information.

### Data Cleaning & Transformation
Data was cleaned using Excel and Power Query

### Data Model
Established a star schema with the fact table "Samsels Store" and dimension tables "City", "State", and "Product Category" to enable efficient slicing and filtering of sales and performance metrics.
![WhatsApp Image 2025-04-06 at 10 55 28_8e0cdb77](https://github.com/user-attachments/assets/48408312-0c45-44d9-8337-a9c8d13a04e8)

### Pages in the Report
1. Summary Page
![image](https://github.com/user-attachments/assets/61ea13be-ef23-43ae-a261-37a3e593e053)

2. Sales Analysis Page
![image](https://github.com/user-attachments/assets/ae5916b1-e17b-498e-8434-36cfbe7a1372)

3. Product Analysis Page
![image](https://github.com/user-attachments/assets/ed377f6a-91e9-4304-9207-9fb1a12ca446)

4. Location Analysis Page
![image](https://github.com/user-attachments/assets/6e70c924-a9b1-4200-8fe1-36a686ae51cd)

5. Product Analysis Page
![image](https://github.com/user-attachments/assets/ff67fc85-7f09-4310-af11-bbdaaeb427a3)

6. Revenue Analysis Page
![image](https://github.com/user-attachments/assets/3579ad7b-338e-4d7d-b451-85394b2e6e1e)

### DAX Measures Create
Here are some of the key DAX measures used in the dashboard:
```DAX 
CurrentTime = FORMAT(NOW(), "HH:MM AM/PM")

Greeting = 
VAR CurrentHour = HOUR(NOW())
RETURN 
IF(CurrentHour < 12, "Good Morning",
   IF(CurrentHour < 18, "Good Afternoon", 
   "Good Evening"))

MoMClientGrowth = 
VAR CurrentMonthClient = 
    CALCULATE(
        [ClientsCount],
        DATESMTD('Calendar_Date'[Date])
    )

VAR PreviousMonthClient = 
    CALCULATE(
        [ClientsCount],
        DATEADD('Calendar_Date'[Date], -1, MONTH)
    )

RETURN 
DIVIDE(
    CurrentMonthClient - PreviousMonthClient,
    PreviousMonthClient,
    0
)


MoMProductsGrowth = 
VAR CurrentMonthProduct = 
    CALCULATE(
        [ProductCount],
        DATESMTD('Calendar_Date'[Date])
    )

VAR PreviousMonthProduct = 
    CALCULATE(
        [ProductCount],
        DATEADD('Calendar_Date'[Date], -1, MONTH)
    )

RETURN 
DIVIDE(
    CurrentMonthProduct - PreviousMonthProduct,
    PreviousMonthProduct,
    0
)

MoMQuantityGrowth = 
VAR CurrentMonthQuantity = 
    CALCULATE(
        SUM('Samsels store'[Quantity]),
        DATESMTD('Calendar_Date'[Date])
    )

VAR PreviousMonthQuantity = 
    CALCULATE(
        SUM('Samsels Store'[Quantity]),
        DATEADD('Calendar_Date'[Date], -1, MONTH)
    )

RETURN 
DIVIDE(
    CurrentMonthQuantity - PreviousMonthQuantity,
    PreviousMonthQuantity,
    0
)


MoMRevenueGrowth = 
VAR CurrentMonthRevenue = 
    CALCULATE(
        SUM('Samsels store'[Revenue]),
        DATESMTD('Calendar_Date'[Date])
    )

VAR PreviousMonthRevenue = 
    CALCULATE(
        SUM('Samsels store'[Revenue]),
        DATEADD('Calendar_Date'[Date], -1, MONTH)
    )

RETURN 
DIVIDE(
    CurrentMonthRevenue - PreviousMonthRevenue,
    PreviousMonthRevenue,
    0
)


ProductCount = DISTINCTCOUNT('Samsels Store'[Product Name])

Profit Margin = DIVIDE(SUM('Samsels Store'[Profit]),SUM('Samsels Store'[Revenue]))
Revenue PY = 
var RevenuePriorYear = CALCULATE(SUM('Samsels Store'[Revenue]), SAMEPERIODLASTYEAR(Calendar_Date[Date]))
RETURN
    RevenuePriorYear


Revenue YoY % = DIVIDE(SUM('Samsels Store'[Revenue]) - [Revenue PY],[Revenue PY]) 
```
### Link to Dashboard
https://app.powerbi.com/view?r=eyJrIjoiYTE4ZTA5Y2MtNzkxMC00OGViLWI2MmMtNWI1MWZkNGMyZWViIiwidCI6ImVkMTlkYTUwLTc2MTktNGIxNy1iNGNhLTVjMTlhYTk0NWRjMCJ9 

### Key Findings
1. Exceeded Revenue Targets Significantly:
The store achieved $765.95K in revenue for 2023, surpassing the annual target of $150K by 410.64%, and December’s monthly revenue also exceeded its target by 52.72% — highlighting strong performance at both yearly and monthly levels.
2. Strong Year-over-Year Growth in October:
October 2023 recorded the highest YoY revenue growth of 509.4%, indicating a standout month, likely due to a promotional campaign, seasonal surge, or operational efficiency.
3. Furniture Category Drives Revenue and Quantity: 
Furniture (blue bubbles) consistently contributes high sales volumes and revenue, making it the top-performing category compared to Office Supplies and Technology.

### Recommendations

