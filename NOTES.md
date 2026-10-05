# Copilot DAX Development Notes

## Measure 1: Running Total Sales
- **Requirement:** Running total (cumulative sales over date).
- **Prompt:** "Write a DAX measure for cumulative sales running total over date for Fact_Sales and Dim_Date."
- **Copilot Initial Suggestion:**
  ```dax
  Cumulative Sales = 
  CALCULATE(
      SUM(Fact_Sales[sales amount]),
      FILTER(ALL(Fact_Sales[date]), Fact_Sales[date] <= MAX(Fact_Sales[date]))
  )