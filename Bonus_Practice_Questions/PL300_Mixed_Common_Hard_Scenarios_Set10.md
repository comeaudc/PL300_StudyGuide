# PL-300 Mixed Scenario Practice — Set 10
## 10 common but challenging exam-style questions

These original practice questions cover a mix of frequently tested Power BI topics. They are not official Microsoft exam questions. Choose the **best** answer for each scenario.

---

### 1. Incremental refresh: detecting new and changed records

A sales table contains several years of transaction data and receives new transactions every day. The source also occasionally corrects records from the previous 10 days. You want to reduce refresh time while ensuring recent corrections are picked up.

What should you configure?

A. A standard scheduled refresh that refreshes the entire table  
B. Incremental refresh with a refresh period that includes the most recent 10 days  
C. DirectQuery for the entire semantic model  
D. A calculated table that filters the current year

**Correct answer: B**

**Explanation:** Incremental refresh partitions historical data and refreshes the configured recent period. The refresh window must include the period in which source records can be corrected. A window that only includes the current day could miss changes to earlier records.

---

### 2. DAX filter context: replacing an existing filter

A report contains a `Sales` table with `Region` and `Revenue` columns. A visual is grouped by Region. You need a measure that always returns revenue for the West region, regardless of the Region currently selected in the visual.

Which measure should you use?

A. `West Revenue = CALCULATE(SUM(Sales[Revenue]), Sales[Region] = "West")`  
B. `West Revenue = SUMX(FILTER(Sales, Sales[Region] = "West"), Sales[Revenue])`  
C. `West Revenue = CALCULATE(SUM(Sales[Revenue]), KEEPFILTERS(Sales[Region] = "West"))`  
D. `West Revenue = SUM(Sales[Revenue])`

**Correct answer: A**

**Explanation:** `CALCULATE` modifies filter context. Its Boolean filter on `Sales[Region]` replaces an existing filter on that same column, so the measure evaluates West revenue even when the visual row is another region. `KEEPFILTERS` would intersect the existing filter with West and could return blank for other regions.

---

### 3. Relationships: multiple date columns

An Orders table contains `OrderDate` and `ShipDate`. Both columns need to connect to the same Date table. Reports should use Order Date by default, but some measures must calculate sales by Ship Date.

What should you do?

A. Create two active relationships from Date to Orders  
B. Create one active relationship for OrderDate and one inactive relationship for ShipDate; use `USERELATIONSHIP` in measures that need ShipDate  
C. Duplicate the Orders table and create a separate Date table for each date  
D. Remove both date columns and create a calculated date key

**Correct answer: B**

**Explanation:** A model can have multiple relationships between the same tables, but only one can be active for a given relationship path. Keep the commonly used OrderDate relationship active and activate the ShipDate relationship inside specific measures with `USERELATIONSHIP`.

---

### 4. Power Query: query folding and performance

A large SQL table is imported into Power BI. You filter the rows to the previous two years and remove several unused columns. The Power Query steps currently fold to the SQL source. You then add a custom transformation that Power Query cannot translate into SQL. Refresh becomes significantly slower.

What is the most appropriate first action?

A. Move the non-folding transformation after the row filters and column removal, where possible  
B. Convert the table to DirectQuery  
C. Disable query folding for the entire query  
D. Replace all Power Query steps with calculated columns

**Correct answer: A**

**Explanation:** Apply foldable filters and column selection as early as possible so the source processes less data before rows are brought into Power Query. Place non-folding steps later when possible. DirectQuery is not an automatic fix and has its own modeling and performance constraints.

---

### 5. Row-level security: testing and workspace roles

You create a role that filters a Sales table so each regional manager sees only their own region. You test the role successfully in Power BI Desktop. After publishing, a user assigned to the role can see all regions because they were given the Member role in the workspace.

What should you do?

A. Add another DAX filter to the role  
B. Change the user to Viewer in the workspace and assign them to the RLS role  
C. Give the user Build permission on the semantic model  
D. Create a separate report for each region

**Correct answer: B**

**Explanation:** RLS applies to users consuming content with read-only access, such as workspace Viewers or users with app access. Workspace Admin, Member, and Contributor roles have edit permissions and are not restricted by RLS in the same way. Assign consumers an appropriate read-only access path.

---

### 6. Storage mode: choosing a model design

A semantic model combines a large fact table in SQL Server with a small dimension table that users frequently slice by. The fact table must remain in DirectQuery to meet data-freshness requirements. You want the dimension to work efficiently with the DirectQuery fact table and support cross-source composite-model behavior.

Which storage mode is often appropriate for the dimension table?

A. Import  
B. DirectQuery  
C. Dual  
D. Direct Lake

**Correct answer: C**

**Explanation:** Dual storage mode allows a dimension table to behave as either Import or DirectQuery depending on the query plan. It is commonly used for dimensions related to DirectQuery fact tables in composite models. The best design still depends on the source configuration and model requirements.

---

### 7. Visual interactions: one slicer should not affect a chart

A report page contains a Date slicer, a Region slicer, a matrix, and a trend chart. Users want the Date slicer to filter every visual, but the Region slicer should not affect the trend chart.

What should you configure?

A. Sync slicers  
B. Edit interactions  
C. Drillthrough filters  
D. A report-page tooltip

**Correct answer: B**

**Explanation:** Edit interactions controls how a slicer or visual affects other visuals on the page. Set the Region slicer's interaction with the trend chart to None while leaving its other interactions unchanged. Sync slicers controls slicer behavior across pages, not visual interaction on a page.

---

### 8. Data modeling: many-to-many dimension values

A company tracks sales by Customer and Product. A separate CustomerProduct table lists which products each customer is eligible to purchase. One customer can be associated with many products, and one product can be associated with many customers.

What is the most appropriate modeling approach?

A. Create a many-to-many relationship directly between Customer and Product and remove the mapping table  
B. Use the CustomerProduct table as a bridge table with relationships to Customer and Product  
C. Merge Customer and Product into the Sales fact table in Power Query  
D. Create a bidirectional relationship between every table

**Correct answer: B**

**Explanation:** A bridge table represents the many-to-many association and provides a clear path between the dimensions. Avoid adding bidirectional filtering everywhere; it can create ambiguous filter paths and unexpected results. Configure relationship directions and cardinality deliberately.

---

### 9. Refresh troubleshooting: on-premises data

A published Import-mode semantic model connects to a SQL Server database located on the company's internal network. Refresh works in Power BI Desktop but fails in the Power BI service because the data source is not reachable.

What should you configure?

A. An on-premises data gateway, then map the semantic model's data source and credentials  
B. A personal bookmark for the SQL connection  
C. A sensitivity label on the semantic model  
D. A DirectQuery connection from the report to the local computer

**Correct answer: A**

**Explanation:** The Power BI service needs a gateway to reach supported on-premises data sources. Configure the gateway, ensure the server/database details match the semantic model connection, and provide valid credentials. Desktop connectivity alone does not provide the service with network access.

---

### 10. Performance: identifying the source of a slow visual

A report page has one visual that takes several seconds to load. Other visuals on the page respond quickly. You need to determine whether the delay is caused by the DAX query, visual rendering, or other processing.

Which tool should you use first?

A. Model view  
B. Performance Analyzer  
C. Power Query Column Profile  
D. Manage roles

**Correct answer: B**

**Explanation:** Performance Analyzer records visual load timings and separates query duration from visual display and other processing. You can copy the visual's DAX query for further investigation, including in DAX Query View. It measures report visual performance, not the overall efficiency of the semantic model schema by itself.

---

## Quick review: concepts tested

- Incremental refresh and refresh windows
- `CALCULATE` filter replacement versus `KEEPFILTERS`
- Active and inactive relationships; `USERELATIONSHIP`
- Query folding and Power Query step order
- RLS behavior with workspace roles
- Dual storage mode in composite models
- Edit interactions versus Sync slicers
- Bridge tables for many-to-many modeling
- On-premises data gateways
- Performance Analyzer and visual query diagnostics
