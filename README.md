# DAX measures workflow
## DAX Measures Workflow in Power BI

#### Your DAX expression

[MaxProcessDate] = MAX(Loans[PROCESS_DATE])

calculates the maximum PROCESS_DATE from the Loans table. How you use this will depend on context:

If you use it as a measure, it will return the latest date in the current filter context—often the latest available loan record.
If you use it as a calculated column, DAX will compute the same value for every row (the absolute max PROCESS_DATE in the whole table).
Normally, MAX is used as a measure in Power BI for reporting, to show the latest transaction or event per grouping.
Example as a measure:

MaxProcessDate = MAX(Loans[PROCESS_DATE])
This measure can then be dragged into visuals, and the max date will respect visuals’ filters (e.g., for each product, client, or region).

#### Key Differences
Purpose	Recommended Use	Behavior
Calculated Column	Rare, usually unused	The same value for every row in Loans
Measure	Common for reporting	Respects current filters (context-aware)

Relationships

If you filter other tables by [MaxProcessDate], create relationships by linking Loans[PROCESS_DATE] to a date table, and use the measure in visuals to reflect the freshest data.

#### Typical Use Cases:

Show most recent loan activity.
Filter a report to only show data for the latest process date.
Compare measures as of the most recent data refresh.

1. Data Modeling
Import Data: Bring data into Power BI from various sources.
Establish Relationships: Define relationships between tables (e.g., star schema) to enable accurate calculations across tables. Proper relationships allow DAX measures to utilize context efficiently.
Create Calculated Columns: Use DAX expressions to create new columns at the row level within a table. Calculated columns are evaluated when the data is loaded or refreshed and are useful for static or row-level calculations.

3. Measure Creation
Define Measures: Measures are DAX formulas that perform calculations on your data, dynamically responding to filters and slicers in reports. Measures typically aggregate data (e.g., SUM, AVERAGE, COUNT) based on context.
Common DAX Functions:
SUM(), COUNTROWS(), CALCULATE(), FILTER(), ALL(), RELATED(), IF(), SWITCH()
Reusable Logic: Measures are highly reusable and meant for aggregations, unlike calculated columns, which are static.

4.. Context Evaluation
Row Context: Used mostly in calculated columns, where DAX evaluates the formula for each row.
Filter Context: Measures work within the filter context applied by visuals, slicers, or page filters, making them dynamic.

5. Report Visualization
Add to Visuals: Drag and drop measures onto visuals such as charts and tables. Measures update automatically when filters and slicers change, reflecting values based on the current context.

6. Best Practices
Keep Measures Centralized: Store measures in a dedicated table for easy reference.
Use Descriptive Names & Documentation: Name your measures clearly and comment logic as needed.
Optimize DAX Code: Avoid unnecessary complexity; use variables (VAR) to clarify logic and boost performance.
