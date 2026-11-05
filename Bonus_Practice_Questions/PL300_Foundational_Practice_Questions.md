# PL-300 Practice Questions: Foundational Topics

**10 scenario-based multiple-choice questions with answers and explanations**

These are original practice questions modeled on the scenario-based style of the Microsoft PL-300 exam, not actual exam questions.

## 1. Power Query: Column Quality

A sales analyst imports a CSV file into Power Query Editor. The Column Quality bar for the `CustomerID` column shows 95% valid, 3% error, and 2% empty. What does this tell the analyst?

A. 95% of the rows contain unique CustomerIDs.  
B. 5% of the values are either errors or empty.  
C. 5% of the rows are duplicates.  
D. The column contains 5% incorrect data types.

**Answer: B. 5% of the values are either errors or empty.**

**Explanation:** Column Quality reports the percentage of valid, error, and empty values. It does not identify duplicates or guarantee uniqueness.

## 2. Power Query: Column Distribution

An analyst wants to identify whether a `ProductCategory` column contains repeated categories and how frequently each category occurs. Which Power Query profiling feature is most appropriate?

A. Column Quality  
B. Column Distribution  
C. Column Profile only  
D. Applied Steps

**Answer: B. Column Distribution.**

**Explanation:** Column Distribution displays value frequency and distinct/unique value information, helping reveal repeated categories and their distribution.

## 3. Power Query: Column Profile

A column contains employee salaries. An analyst needs to inspect the minimum, maximum, average, count, and distribution of values for that column. Which feature should they use?

A. Column Quality  
B. Column Distribution  
C. Column Profile  
D. Manage Relationships

**Answer: C. Column Profile.**

**Explanation:** Column Profile provides detailed statistics for a selected column, including measures such as minimum, maximum, average, and count where applicable.

## 4. Power Query: Profiling Scope

A dataset contains 150,000 rows. An analyst notices that Power Query's profiling statistics appear to reflect only the first 1,000 rows. They need statistics based on the full dataset. What should they do?

A. Change the data type to Text.  
B. Enable Column Quality for the entire dataset.  
C. Change profiling to use the entire dataset.  
D. Load the data into Excel first.

**Answer: C. Change profiling to use the entire dataset.**

**Explanation:** Power Query data profiling uses the first 1,000 rows by default. Change the profiling scope to the entire dataset when full-data statistics are needed.

## 5. Power Query: Data Types

A CSV contains a `TransactionDate` column with values such as `10/15/2026`. Power BI imports the column as Text, preventing correct date filtering and time-based analysis. What should the analyst do?

A. Rename the column `TransactionDate`.  
B. Change the column's data type to Date, checking the locale if necessary.  
C. Remove duplicate dates.  
D. Create a relationship to the Date table before changing the type.

**Answer: B. Change the column's data type to Date, checking the locale if necessary.**

**Explanation:** The correct data type enables date-aware operations. If dates are interpreted incorrectly because of regional formats, use the appropriate locale when converting.

## 6. Power Query: Errors vs. Empty Values

A numeric `Revenue` column contains some blank cells and some values that display as errors after the analyst changes the column type to Decimal Number. What is the best first step?

A. Immediately replace every error and blank with zero.  
B. Use Column Quality and Column Profile to identify the issue, then investigate the errors and decide how to handle them.  
C. Delete the entire Revenue column.  
D. Create a DAX measure to convert the errors to numbers.

**Answer: B. Use Column Quality and Column Profile to identify the issue, then investigate the errors and decide how to handle them.**

**Explanation:** Profile the data first. Empty values and conversion errors are different problems and should be handled according to their cause and business meaning.

## 7. Power Query: Merge vs. Append

A company has January sales and February sales tables with the same columns. The analyst wants one table containing all sales rows from both months. Which Power Query operation should they use?

A. Merge Queries  
B. Append Queries  
C. Group By  
D. Pivot Column

**Answer: B. Append Queries.**

**Explanation:** Append stacks rows from multiple tables. Merge joins tables horizontally using matching key values.

## 8. Data Modeling: Relationships

A Power BI model contains a `Customers` table with one row per customer and a `Sales` table with many transactions per customer. What is the recommended relationship between these tables?

A. One-to-one, with Sales filtering Customers.  
B. One-to-many from Customers to Sales.  
C. Many-to-many from Customers to Sales.  
D. No relationship; use a merge instead.

**Answer: B. One-to-many from Customers to Sales.**

**Explanation:** Customers is the dimension table on the one side; Sales is the fact table on the many side. A relationship lets customer filters affect sales analysis.

## 9. Data Modeling: Star Schema

An analyst builds a model with a `Sales` table containing transaction amounts and `Customer`, `Product`, and `Date` tables containing descriptive attributes. What is this design generally called?

A. A flat-file model  
B. A star schema  
C. A many-to-many schema  
D. A normalized transaction-only schema

**Answer: B. A star schema.**

**Explanation:** A star schema centers on a fact table containing events or measurements, surrounded by dimension tables used for filtering and grouping.

## 10. Excel vs. Power BI: Transformation

An analyst imports an Excel workbook into Power BI. They need to remove blank rows, split a full-name column, and set data types before loading the data. Where should they perform these transformations?

A. In Power Query Editor, using applied transformation steps.  
B. Only in the report's visual formatting pane.  
C. In DAX measures after the data is loaded.  
D. In the relationship view by changing cross-filter direction.

**Answer: A. In Power Query Editor, using applied transformation steps.**

**Explanation:** Power Query handles data extraction and transformation before loading data into the model. Applied steps record the transformation sequence for refreshes.

---

## Quick Review: Key Concepts

| Feature | What it tells you |
|---|---|
| **Column Quality** | Percentage of valid, error, and empty values |
| **Column Distribution** | Frequency of values, distinct values, and unique values |
| **Column Profile** | Detailed statistics and value distribution for a selected column |
| **Append** | Adds rows from one table to another |
| **Merge** | Joins tables using matching columns |
| **Power Query Editor** | Cleans and transforms data before loading |
| **Relationships** | Connects tables so filters and analysis work across the model |
| **Star schema** | Organizes fact and dimension tables for analytical reporting |

## Exam Tips

- **Distinct values** are different values; **unique values** are values that appear exactly once.
- Power Query profiling defaults to the **first 1,000 rows** unless the profiling scope is changed.
- **Append** combines tables vertically (adds rows); **Merge** combines tables horizontally based on matching columns.
- Investigate errors and blank values before deciding how to handle them; do not automatically replace them with zero.

# PL-300 Practice Questions: Intermediate Scenarios

**10 original multiple-choice scenario questions with answers and explanations**

These questions are designed for intermediate PL-300 practice. They cover data preparation, modeling, DAX, and report behavior in the style of certification exam scenarios. They are practice questions, not actual Microsoft exam questions.

## 1. Power Query: Merge Join Kind

A retailer imports a `Sales` table and a `Products` table into Power Query. The analyst needs to keep every sales row, including sales with a ProductID that does not match a row in `Products`. Product details should be added where a match exists. Which join kind should the analyst use when merging `Sales` with `Products`?

A. Inner  
B. Left outer  
C. Right anti  
D. Full outer

**Answer: B. Left outer.**

**Explanation:** A left outer join retains every row from the first (left) table and brings in matching rows from the second table. Unmatched sales rows remain, with nulls for the product fields.

## 2. Power Query: Reference vs. Duplicate

An analyst has a cleaned `Sales` query and wants to create two additional queries based on it: one for detailed sales reporting and one aggregated by region. They want the new queries to build on the existing transformation steps rather than independently repeat the original source and cleaning process. What is the best option?

A. Create a Reference of the cleaned query for each new query.  
B. Duplicate the query and manually repeat all transformations.  
C. Export the cleaned query to CSV and reimport it twice.  
D. Create a relationship between the two new queries.

**Answer: A. Create a Reference of the cleaned query for each new query.**

**Explanation:** A referenced query uses the output of the original query as its starting point. This helps centralize shared transformation logic. A duplicate copies the existing query steps into a separate query.

## 3. Data Modeling: Filter Direction

A model has a `Product` dimension related one-to-many to a `Sales` fact table. A report should allow users to select a product and see the matching sales. There is no requirement for sales selections to filter the Product table. Which cross-filter direction is generally recommended?

A. Both  
B. Single, from Product to Sales  
C. Single, from Sales to Product  
D. Disable the relationship

**Answer: B. Single, from Product to Sales.**

**Explanation:** In a typical star schema, dimension tables filter fact tables. Single-direction filtering is generally preferred unless a specific requirement calls for bidirectional filtering.

## 4. DAX: Measure vs. Calculated Column

A report needs to display total revenue that changes when a user filters by year, region, or product. Which option is most appropriate?

A. A calculated column that stores the total revenue for every row  
B. A measure using `SUM(Sales[Revenue])`  
C. A Power Query index column  
D. A calculated table with one row per revenue value

**Answer: B. A measure using `SUM(Sales[Revenue])`.**

**Explanation:** A measure is evaluated in the current filter context, so its result changes with report filters and slicers. A calculated column is computed row by row during model processing and stored in the model.

## 5. DAX: CALCULATE and Filter Context

A measure is defined as:

```DAX
Online Revenue =
CALCULATE(
    SUM(Sales[Revenue]),
    Sales[Channel] = "Online"
)
```

A report page is filtered to `Channel = "Store"`. What does this measure return under the standard `CALCULATE` filter behavior?

A. Revenue for Store only  
B. Revenue for Online only  
C. Revenue for both Store and Online  
D. An error because two channel filters are applied

**Answer: B. Revenue for Online only.**

**Explanation:** The filter argument on `Sales[Channel]` replaces an existing filter on that same column in the usual case, so the measure calculates Online revenue. `KEEPFILTERS` would instead intersect the new filter with the existing filter.

## 6. DAX: DISTINCTCOUNT

A sales manager wants to count how many different customers made purchases in the current report context. Some customers may have made multiple purchases. Which DAX expression is most appropriate?

A. `COUNTROWS(Sales)`  
B. `COUNT(Sales[CustomerID])`  
C. `DISTINCTCOUNT(Sales[CustomerID])`  
D. `SUM(Sales[CustomerID])`

**Answer: C. `DISTINCTCOUNT(Sales[CustomerID])`.**

**Explanation:** `DISTINCTCOUNT` counts distinct values in a column within the current filter context. `COUNTROWS(Sales)` counts transaction rows, not unique customers.

## 7. Data Modeling: Inactive Relationship

A `Date` table has an active relationship to `Sales[OrderDate]` and an inactive relationship to `Sales[ShipDate]`. The report needs a measure for sales by shipping date without changing the model's active relationship. Which DAX function should the measure use?

A. `RELATED`  
B. `USERELATIONSHIP` inside `CALCULATE`  
C. `DISTINCTCOUNT`  
D. `CROSSFILTER` with no arguments

**Answer: B. `USERELATIONSHIP` inside `CALCULATE`.**

**Explanation:** `USERELATIONSHIP` activates an existing inactive relationship for the calculation in which it is used. This is a common approach for role-playing date dimensions such as order date and ship date.

## 8. Report Design: Drill-Down Hierarchy

A report contains a sales chart organized by Year, Quarter, Month, and Day. Users need to move from yearly totals into quarterly, monthly, and daily detail within the same visual. Which feature should the analyst configure?

A. A drill-down hierarchy in the visual  
B. A report-page tooltip only  
C. A conditional formatting rule  
D. A synced slicer

**Answer: A. A drill-down hierarchy in the visual.**

**Explanation:** A hierarchy lets users drill through levels of detail in the same visual. Drillthrough is different: it navigates to another report page filtered to a selected data point.

## 9. Power BI Performance: Unused Columns

A model imports a large transaction table with 40 columns, but only 15 columns are used in relationships, calculations, or reports. The unused columns contain high-cardinality text values and increase model size. What is the best optimization step?

A. Add more calculated columns to improve filtering.  
B. Remove the unused columns from the model, preferably in Power Query when appropriate.  
C. Change every relationship to bidirectional.  
D. Convert all columns to Text.

**Answer: B. Remove the unused columns from the model, preferably in Power Query when appropriate.**

**Explanation:** Unneeded columns consume memory and can increase model size and processing cost. Removing them before loading can improve model efficiency.

## 10. Power BI Service: Row-Level Security

A report is published to the Power BI service. Sales managers should see only the rows for the regions assigned to them. The model includes a `Region` column and an appropriate security role has been defined. What must happen for the role's row-level security to apply to a manager?

A. The manager must be assigned to the appropriate RLS role in the semantic model's security settings.  
B. The report author must hide the other regions in each visual.  
C. The manager must use a page-level filter.  
D. The report must be exported to Excel for each manager.

**Answer: A. The manager must be assigned to the appropriate RLS role in the semantic model's security settings.**

**Explanation:** Row-level security restricts which rows a user can access through the semantic model. The user or an appropriate security group must be assigned to the role. Hiding categories or applying visual filters is not a security control.

---

## Quick Review: Intermediate Concepts

| Concept | Exam takeaway |
|---|---|
| **Left outer merge** | Keeps all rows from the first table and adds matching values from the second |
| **Reference query** | Starts from the output of another query |
| **Single-direction relationship** | Typically filters from dimension to fact |
| **Measure** | Evaluates in the current filter context |
| **`CALCULATE`** | Evaluates an expression in a modified filter context |
| **`DISTINCTCOUNT`** | Counts distinct column values |
| **`USERELATIONSHIP`** | Uses an existing inactive relationship for a calculation |
| **Drill-down** | Moves through hierarchy levels within a visual |
| **Model optimization** | Remove unnecessary rows and columns |
| **RLS** | Restricts rows users can access through the semantic model |

## Instructor Note

These questions span several PL-300 skill areas rather than a single exam domain. For exam practice, have learners explain not only why the correct answer is right, but also why each distractor is wrong.
