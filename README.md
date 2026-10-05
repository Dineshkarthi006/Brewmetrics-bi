# BrewMetrics Coffee Co. — Version-Controlled BI Solution

An auditable, end-to-end Power BI analytics platform built for BrewMetrics Coffee Co., analyzing approximately 15,500 transactions across April to July 2026. This solution leverages the Power BI Project (`.pbip`) format, Git version tracking, and GitHub Copilot to ensure transparent, reproducible data model governance.

## Data Architecture & Star Schema
The raw flat transaction dataset (`brewmetrics_sales.csv`) has been decomposed into an optimized star schema model:
* **Fact_Sales**: Contains granular transaction metrics including `quantity`, `sales_amount`, `store_format`, `date`, foreign keys (`City_ID`, `Product_ID`), and transaction IDs.
* **Dim_Date**: Calendar dimension containing dates, month numbers, month names, and day identifiers.
* **Dim_City**: Geographic dimension capturing store operational territories (`Bengaluru`, `Chennai`, `Coimbatore`, `Hyderabad`) with dedicated `City_ID` keys.
* **Dim_Product**: Product catalog maintaining standardized categories (`Coffee`, `Bakery`, `Merchandise`), item names, and unit prices indexed by `Product_ID`.

All relationships are modeled as one-to-many ($1:*$) single-directional links from dimensions to the central fact table.

## DAX Measures
The semantic model includes four production measures developed with Copilot assistance and validated against star-schema best practices:
1. **Running Total Sales**: Cumulative revenue aggregated across `Dim_Date[date]` using `CALCULATE` and `FILTER(ALL(...))`.
2. **Sales MoM Growth**: Month-over-month revenue percentage variance using `PREVIOUSMONTH` and safe zero-division handling with `DIVIDE`.
3. **City Rank**: Performance ranking of cities by sales volume utilizing `RANKX(ALL(Dim_City[city]), ...)`.
4. **Cold Brew Sales Share**: Proportional revenue contribution of Cold Brew beverages against overall sales volume.

## Key Business Insights
1. **Regional Outperformance**: Bengaluru consistently leads all markets, generating approximately 1.15M in sales across Flagship, Kiosk, and Drive-Thru formats, outperforming Chennai, Hyderabad, and Coimbatore.
2. **Cold Brew Seasonal Surge**: Cold Brew sales exhibit an aggressive spike across April and May (peaking over 300K in May) before tapering off into June, highlighting clear summer demand cycles.
3. **Channel Performance**: Flagship stores drive the vast majority of top-line revenue, followed by Drive-Thru locations, while Kiosks capture high-margin, quick-turn beverage transactions.
