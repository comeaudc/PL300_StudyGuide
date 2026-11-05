# PL-300 Hard Scenario Practice — Set 14
**Focus: Query folding, DAX, and analytical logic**

Choose the best answer. Answers and explanations follow each question. These are original practice questions, not official Microsoft exam items.

---

### 1. Query folding: A nonfolding step interrupts the query

A Power Query query connects to a large SQL Server table. It filters rows by date and selects five columns. A later custom transformation cannot be translated into SQL. You then add another filter that would otherwise be foldable.

What is the most accurate expectation?

A. All steps after the custom transformation are automatically sent to SQL Server  
B. The later filter may be evaluated by the Power Query engine because folding was broken at the earlier step  
C. Query folding is restored automatically whenever a later step uses a standard filter  
D. The source database executes every step because the original connection is SQL Server  

**Correct answer: B**

**Explanation:** Query folding depends on whether Power Query can translate the sequence of transformations into a source query. A nonfolding step can prevent subsequent steps from folding. Place foldable filters and column selection early, and inspect folding indicators or the native query where available.

---

### 2. Query folding: Best transformation order

A table contains 80 million rows. You need to keep records from the last two years, remove 25 unused columns, and add a custom index. The date filter and column removal are supported by the source connector, but the index operation does not fold.

Which sequence is generally best?

A. Add the index, filter the dates, then remove columns  
B. Filter the dates, remove unused columns, then add the index  
C. Load all rows, then filter in a report visual  
D. Convert all columns to text, add the index, then filter  

**Correct answer: B**

**Explanation:** Apply foldable row filters and column selection before a nonfolding operation. This gives the source an opportunity to reduce rows and columns before the remaining work is performed by Power Query. Confirm actual folding behavior for the connector and transformations used.

---

### 3. Query folding: Incremental refresh

You configure incremental refresh on a large SQL fact table. The query uses `RangeStart` and `RangeEnd` parameters to filter a datetime column. Refreshes are unexpectedly slow, and the SQL source appears to return far more rows than the partition date range requires.

What should you investigate first?

A. Whether the `RangeStart` and `RangeEnd` filters fold to the SQL source  
B. Whether the report page has too many slicers  
C. Whether the fact table is sorted alphabetically in Model view  
D. Whether the date column is hidden from report view  

**Correct answer: A**

**Explanation:** Incremental refresh relies on the date-range filter to isolate rows for each partition. If the filter does not fold, Power Query may retrieve and process far more data than intended. Verify folding for the range filter and check source-side query behavior.

---

### 4. DAX: `CALCULATE` and filter replacement

A matrix displays sales by Region. The page is filtered to `West`, but a measure must always show sales for `East`, even when a user selects another region.

Which measure meets the requirement?

A. `East Sales = CALCULATE([Sales], Sales[Region] = "East")`  
B. `East Sales = CALCULATE([Sales], KEEPFILTERS(Sales[Region] = "East"))`  
C. `East Sales = FILTER(Sales, Sales[Region] = "East")`  
D. `East Sales = COUNTROWS(FILTER(Sales, Sales[Region] = "East"))`

**Correct answer: A**

**Explanation:** A filter argument in `CALCULATE` normally replaces an existing filter on the same column. The measure replaces the current Region filter with East. `KEEPFILTERS` intersects the new filter with the existing one, which can return blank when the current selection is West.

---

### 5. DAX: `KEEPFILTERS` and intersection logic

A report page is filtered to the `West` region. A measure should return sales only for regions included in both the report selection and a specified group: `West` and `Central`.

Which expression correctly preserves the intersection?

A. `CALCULATE([Sales], Sales[Region] IN {"West", "Central"})`  
B. `CALCULATE([Sales], KEEPFILTERS(Sales[Region] IN {"West", "Central"}))`  
C. `CALCULATE([Sales], REMOVEFILTERS(Sales[Region]))`  
D. `CALCULATE([Sales], ALL(Sales[Region]))`

**Correct answer: B**

**Explanation:** `KEEPFILTERS` makes the new region condition intersect with the existing filter context. With the page filtered to West, the result includes West only. Without `KEEPFILTERS`, the filter argument would replace the existing Region filter and could include both West and Central.

---

### 6. DAX: Row context and context transition

A measure uses `SUMX` to iterate over a Customer table. For each customer, it calls a measure that calculates total sales. The result evaluates sales separately for each customer.

Why does the measure evaluate in the current customer context?

A. `SUMX` automatically changes every row context into filter context  
B. A measure invocation performs context transition, applying the current row context as filter context  
C. `SUMX` disables filter context while iterating  
D. Measures are always evaluated once for the entire table, regardless of the iterator  

**Correct answer: B**

**Explanation:** When a measure is evaluated in row context, the implicit `CALCULATE` around the measure triggers context transition. The current customer row becomes filter context for the measure. This is an important distinction when using measures inside iterators such as `SUMX`.

---

### 7. DAX: `ALL` versus `REMOVEFILTERS`

A report contains a Product Category slicer. A measure must calculate each category's percentage of total sales across all categories while retaining filters such as Date and Region.

Which denominator is most appropriate?

A. `CALCULATE([Sales], REMOVEFILTERS(Product[Category]))`  
B. `CALCULATE([Sales], REMOVEFILTERS())`  
C. `CALCULATE([Sales], ALL(Sales))`  
D. `CALCULATE([Sales], KEEPFILTERS(Product[Category]))`

**Correct answer: A**

**Explanation:** Removing the filter from only `Product[Category]` clears the category selection while retaining other report filters, such as Date and Region. Removing all filters would ignore more of the report context than required.

---

### 8. DAX logic: `BLANK()` and zero

A KPI measure returns `BLANK()` when there are no qualifying transactions. The report requirement says the KPI should display zero instead of blank, without changing the underlying transaction data.

Which approach is best?

A. Replace all blank values in the source fact table with zero  
B. Wrap the measure with `COALESCE([Qualifying Sales], 0)`  
C. Use `DISTINCTCOUNT` on the transaction ID  
D. Add a calculated column containing zero for every row  

**Correct answer: B**

**Explanation:** `COALESCE` returns the first expression that is not blank. It can provide a display value of zero when the measure returns `BLANK()`, without modifying source records or adding unnecessary calculated columns.

---

### 9. DAX logic: Distinct counts across groups

A business has customer transactions across multiple product categories. The same customer can purchase from several categories. A matrix displays distinct customers by category, and the total row is required to show unique customers across the entire selection.

What should you expect from a `DISTINCTCOUNT(CustomerID)` measure?

A. The total row always equals the sum of category-level distinct counts  
B. The total row recalculates the distinct count over the total filter context and may be less than the sum of category rows  
C. The total row is always blank when customers appear in multiple categories  
D. The total row counts transaction rows instead of unique customers  

**Correct answer: B**

**Explanation:** A measure is recalculated in the total row's filter context; Power BI does not necessarily add the visible row results. Customers appearing in multiple categories are counted once in the overall total, so the total can be lower than the sum of category-level distinct counts.

---

### 10. DAX logic: `USERELATIONSHIP` and filter context

A model has a Date dimension with an active relationship to `Sales[OrderDate]` and an inactive relationship to `Sales[DeliveryDate]`. A visual uses the Date dimension. You need a measure that groups sales by delivery date rather than order date.

Which expression is correct?

A. `Delivery Sales = CALCULATE([Sales], USERELATIONSHIP('Date'[Date], Sales[DeliveryDate]))`  
B. `Delivery Sales = CALCULATE([Sales], RELATED(Sales[DeliveryDate]))`  
C. `Delivery Sales = CALCULATE([Sales], REMOVEFILTERS('Date'))`  
D. `Delivery Sales = USERELATIONSHIP('Date'[Date], Sales[DeliveryDate])`

**Correct answer: A**

**Explanation:** `USERELATIONSHIP` is used within a calculation such as `CALCULATE` to activate the existing inactive relationship for that measure evaluation. The Date visual context then filters Sales through DeliveryDate for this calculation.

---

## Topic checklist

- [x] Query folding breaks and transformation order
- [x] Folding with incremental refresh parameters
- [x] `CALCULATE` filter replacement
- [x] `KEEPFILTERS` and filter intersection
- [x] Row context and context transition
- [x] `ALL` / `REMOVEFILTERS`
- [x] `BLANK()` and `COALESCE`
- [x] `DISTINCTCOUNT` totals
- [x] `USERELATIONSHIP`
