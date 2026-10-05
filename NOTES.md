# Copilot DAX Development Notes

## Measure 1: Running Total Sales
- **Requirement:** Running total (cumulative sales over date).
- **Prompt:** "Write a DAX measure for cumulative sales running total over date for Fact_Sales and Dim_Date."
- **Copilot Initial Suggestion:**

- **Corrections/Refinements:** Verified column name matches `Fact_Sales[sales_amount]` (or `[sales amount]`) and confirmed filter context transitions across `Dim_Date[date]` rather than aggregating over the fact table directly, maintaining star schema performance.
- **Final DAX Code:**