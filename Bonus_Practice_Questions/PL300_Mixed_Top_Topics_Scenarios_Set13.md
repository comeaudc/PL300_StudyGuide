# PL-300 Mixed Scenario Practice — Set 13
**10 original exam-style questions covering high-value Power BI topics**

Choose the **best** answer for each scenario. Answers and explanations appear immediately after each question. These are original practice questions, not official Microsoft exam items.

---

### 1. Modeling: Relationship cardinality

A sales table contains one row per transaction and may contain many transactions for the same product. A product table contains one row per product, with a unique `ProductID`. You need product attributes to filter sales in reports.

Which relationship should you create?

A. One-to-one, with Sales filtering Product  
B. One-to-many, with Product on the one side and Sales on the many side  
C. Many-to-many, with bidirectional filtering  
D. Many-to-one, with Sales on the one side and Product on the many side  

**Correct answer: B**

**Explanation:** `ProductID` is unique in Product but repeats in Sales. Product belongs on the **one** side and Sales on the **many** side. A single-direction filter from the dimension to the fact table is generally the preferred star-schema pattern.

---

### 2. DAX: Filter context and `CALCULATE`

A report page is filtered to the `West` region. A measure must calculate sales for the `East` region regardless of the current Region filter.

Which measure is most appropriate?

A. `East Sales = CALCULATE([Total Sales], Sales[Region] = "East")`  
B. `East Sales = SUMX(FILTER(Sales, Sales[Region] = "East"), Sales[SalesAmount])`  
C. `East Sales = CALCULATE([Total Sales], KEEPFILTERS(Sales[Region] = "East"))`  
D. `East Sales = DISTINCTCOUNT(Sales[Region])`

**Correct answer: A**

**Explanation:** A Boolean filter passed to `CALCULATE` replaces an existing filter on the same column by default. Therefore, the current `West` filter on `Sales[Region]` is replaced with `East`. `KEEPFILTERS` would intersect the filters, producing no rows when West and East conflict.

---

### 3. Power Query: Merge versus append

You receive monthly files with the same columns and structure. Each file contains that month's transactions. You need one table containing all transactions from every month.

Which operation should you use?

A. Merge queries  
B. Append queries  
C. Group By  
D. Pivot column  

**Correct answer: B**

**Explanation:** Append stacks rows from multiple tables with matching or compatible columns. Merge joins tables horizontally using matching key values, which is appropriate when you need to bring related columns from another table.

---

### 4. Power Query: Query folding

A large SQL table contains several years of transactions. In Power Query, you need to filter it to the current year and remove unused columns. You want the source database to perform as much of this work as possible.

What should you do?

A. Load the entire table, then apply filters in DAX  
B. Apply foldable filters and column removal early, and verify that the steps fold  
C. Convert every column to text before filtering  
D. Disable query folding so Power Query controls all transformations  

**Correct answer: B**

**Explanation:** Query folding allows Power Query to translate supported transformations into a source query. Applying filters and selecting needed columns early can reduce the amount of data transferred. Verify folding because not every transformation or connector supports every step.

---

### 5. Incremental refresh: Late-arriving changes

A fact table retains five years of sales history. The source system can correct transaction records for up to 30 days after the transaction date. You want routine refreshes to pick up those corrections without reprocessing all five years.

Which configuration best meets the requirement?

A. Store five years and refresh the most recent 30 days  
B. Store 30 days and refresh five years  
C. Store five years and refresh only the most recent day  
D. Store and refresh only five years, with no incremental refresh policy  

**Correct answer: A**

**Explanation:** The store period controls how much historical data is retained. The refresh period controls the recent window that is reprocessed. Because records can change for up to 30 days, the refresh window should cover at least that correction period. The `RangeStart` and `RangeEnd` filters should fold to the source when possible.

---

### 6. Security: Row-level security and workspace roles

A report consumer must see only rows for their assigned sales territory. They should be able to view reports but must not edit workspace content.

What should the administrator do?

A. Assign the user the Contributor role and configure RLS  
B. Assign the user the Viewer role and add them to the appropriate RLS role  
C. Assign the user the Member role and configure object-level security  
D. Give the user Build permission only; this automatically applies territory filtering  

**Correct answer: B**

**Explanation:** A Viewer can consume workspace content while remaining subject to RLS. Workspace roles with edit permissions—Admin, Member, and Contributor—are not restricted by RLS in the same way as read-only consumers. Build permission enables downstream use of a semantic model; it does not itself define row filters.

---

### 7. Connectivity: Import versus DirectQuery

A report must display data from a very large SQL database with minimal data duplication. The business requires visuals to query the source at report interaction time, and the source can support the query workload.

Which storage mode best fits?

A. Import  
B. DirectQuery  
C. Dual for every table  
D. Enter Data  

**Correct answer: B**

**Explanation:** DirectQuery leaves the data in the source and sends queries to it as users interact with the report. This can provide access to current source data, but performance depends on the source, network, query design, and concurrency. Import instead stores a refreshed copy in the semantic model.

---

### 8. Report design: Drillthrough

A sales summary page shows revenue by region. Users want to right-click a region and open a detail page that displays the customers and transactions for that selected region.

Which feature should you configure?

A. Drill down  
B. Drillthrough  
C. Report-page tooltip  
D. Sync slicers  

**Correct answer: B**

**Explanation:** Drillthrough navigates to a separate report page and passes the selected context—such as Region—to that page. Drill down changes the level of detail within a visual's hierarchy; a tooltip displays supplementary information on hover.

---

### 9. DAX: Active and inactive relationships

A Date table has an active relationship to `Sales[OrderDate]` and an inactive relationship to `Sales[ShipDate]`. A report needs a measure that calculates sales by shipping date while preserving the model's active OrderDate relationship for other measures.

Which function should the measure use?

A. `RELATED()`  
B. `USERELATIONSHIP()` inside `CALCULATE()`  
C. `CROSSFILTER()` with no relationship arguments  
D. `DISTINCTCOUNT()`  

**Correct answer: B**

**Explanation:** `USERELATIONSHIP` activates an existing inactive relationship for the calculation in which it is used. For example: `Sales by Ship Date = CALCULATE([Total Sales], USERELATIONSHIP('Date'[Date], Sales[ShipDate]))`.

---

### 10. Performance: Identifying a slow visual

A report page loads slowly. You need to determine which visual is generating a long-running DAX query and distinguish query time from visual-rendering time.

Which tool should you use first?

A. Performance Analyzer  
B. Manage relationships  
C. Model view  
D. Power Query data profiling  

**Correct answer: A**

**Explanation:** Performance Analyzer records the time taken by visuals and separates categories such as DAX query time and visual display time. It helps identify which visuals need investigation. It does not directly measure every aspect of semantic-model schema efficiency or replace deeper model analysis.

---

## Quick topic checklist

- [x] Star-schema relationships and cardinality
- [x] `CALCULATE` filter behavior
- [x] Append versus merge
- [x] Query folding
- [x] Incremental refresh
- [x] RLS and workspace roles
- [x] Import versus DirectQuery
- [x] Drillthrough
- [x] Active and inactive relationships
- [x] Performance Analyzer
