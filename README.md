# Superstore Sales Dashboard (Power BI)

An interactive Power BI dashboard built on the Superstore sales dataset, modelled as a star schema, with DAX measures and interactive visuals.

Internship task for Datheon.
## Files
- `Superstore Dashboard.pbix`: the Power BI report (open in Power BI Desktop)
- `Superstore Dashboard.pdf`: exported PDF of the report page
- `superstore_sales (1).csv`: source data

## Data model (star schema)
- **FactOrders**: Order ID, Order Date, Ship Date, Customer ID, Product ID, Region, Sales, Quantity, Discount, Profit
- **DimCustomer**: Customer ID, Customer Name, Segment
- **DimProduct**: Product ID, Category, Sub-Category, Product Name
- **DimRegion**: Region
- **DimDate**: calendar table built in DAX (Date, Year, Month No, Month, Quarter), marked as the date table

All dimensions relate to FactOrders one-to-many, single direction.

## DAX measures
- `Total Sales = SUM(FactOrders[Sales])`
- `Total Profit = SUM(FactOrders[Profit])`
- `Total Orders = DISTINCTCOUNT(FactOrders[Order ID])`
- `Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)`
- `YoY Sales Growth % = VAR PY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DimDate[Date])) RETURN DIVIDE([Total Sales] - PY, PY)`

## Visuals
- KPI cards: Total Sales, Total Profit, Total Orders
- Monthly sales line chart
- Treemap of sales by Category and Sub-Category, with Profit Margin % in the tooltip
- Slicers: Year and Region

## Key figures
- Total Sales: 2,297,200.86
- Total Profit: 286,397.02
- Total Orders: 5,009
- YoY Sales Growth: 2016 -2.83%, 2017 +29.47%, 2018 +20.36%

## Data preparation notes
- The CSV contained 806 extra rows at the bottom (pasted lookup tables for People and Returns). These were filtered out in Power Query, leaving 9,994 order lines.
- Dates are in US format (m/d/yyyy), so the locale is set to English (United States) when typing the date columns.
- Region is held in its own table linked to FactOrders, because customers place orders in more than one region.
- 32 Product IDs appear with more than one product name, so DimProduct keeps the first name for each ID.

## Tools
Power BI Desktop, Power Query (M), DAX

## Author
Jacob Tumwine 
