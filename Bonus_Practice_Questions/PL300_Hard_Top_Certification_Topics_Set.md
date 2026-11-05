# PL-300 Hard Scenario Practice — High-Priority Certification Topics

**Difficulty:** Hard  
**Format:** 10 scenario-based multiple-choice questions  
**Answers:** Correct answer and explanation appear immediately after each question.

These are original practice questions, not official Microsoft exam questions. Topic selection follows Microsoft's PL-300 study guide, with skills measured as of April 20, 2026.

---

## Question 1 — Import, DirectQuery, and Direct Lake

A company stores its analytics data in a Microsoft Fabric lakehouse. The data volume is large, and the organization wants Power BI to query data in OneLake without importing a separate copy into the semantic model. The solution should use the Fabric lakehouse's analytical storage capabilities.

Which storage mode should the analyst evaluate first?

A. Import  
B. DirectQuery  
C. Direct Lake  
D. Dual

**Correct answer: C. Direct Lake.**

**Explanation:** Direct Lake is designed to analyze data stored in OneLake, using the lakehouse or warehouse data directly rather than importing a separate copy into the semantic model. DirectQuery sends queries to a supported external source. Import loads data into the semantic model. Dual is a storage-mode option used in composite-model designs.

---

## Question 2 — Role-Playing Date Dimensions

A sales fact table contains `OrderDateKey`, `ShipDateKey`, and `DeliveryDateKey`. Users need to analyze sales by order date, but they also need to analyze shipments and deliveries by their respective dates. The model should support intuitive filtering without requiring users to activate inactive relationships in every measure.

What is the most appropriate model design?

A. Create three separate date dimension tables, one for each date role  
B. Create one date table and connect all three date keys with active relationships  
C. Use one date table with one active relationship and two inactive relationships for every report scenario  
D. Store all three dates in a single text column

**Correct answer: A. Create three separate date dimension tables, one for each date role.**

**Explanation:** Role-playing dimensions allow the same logical date dimension to serve multiple roles. Separate role-playing date tables provide independent active relationships and intuitive filtering for Order Date, Ship Date, and Delivery Date. An alternative is one date table with one active and multiple inactive relationships, activating an inactive relationship in measures with `USERELATIONSHIP()` when appropriate. The scenario explicitly asks for independent, intuitive filtering without measure-level activation.

---

## Question 3 — CALCULATE and Filter Context

A report contains a `Product` slicer. A measure calculates sales for the Bikes category regardless of the current product selection. The current measure is:

```DAX
Bike Sales =
CALCULATE(
    [Total Sales],
    Product[Category] = "Bikes"
)
```

A user selects `Accessories` in the Product Category slicer. What will the measure return?

A. Sales for Accessories only  
B. Sales for Bikes, because the CALCULATE filter replaces the existing filter on the same column  
C. Sales for Bikes and Accessories combined  
D. Blank, because the filters conflict

**Correct answer: B. Sales for Bikes, because the CALCULATE filter replaces the existing filter on the same column.**

**Explanation:** By default, `CALCULATE` modifies filter context. A filter argument on `Product[Category]` replaces an existing filter on that same column. To intersect the Bikes filter with the existing selection instead, use `KEEPFILTERS()`. In this scenario, the measure returns Bikes sales even when Accessories is selected.

---

## Question 4 — Semi-Additive Measures

A finance report tracks account balances at the end of each day. The analyst creates this measure:

```DAX
Total Balance =
SUM(AccountBalance[Balance])
```

When users view several months, the measure adds every daily balance together. The business instead needs the balance at the end of the selected period.

Which approach is most appropriate?

A. Use `SUMX` over every date in the selected period  
B. Use a semi-additive measure that evaluates the balance on the last date in the selected period  
C. Change the balance column to Text  
D. Use `DISTINCTCOUNT` on the balance column

**Correct answer: B. Use a semi-additive measure that evaluates the balance on the last date in the selected period.**

**Explanation:** Account balances are semi-additive: they can often be summed across accounts, but should not be summed across time. A measure should identify the last date in the current period and return the balance for that date. The exact DAX depends on the model and whether dates without balances should be skipped.

---

## Question 5 — Performance Analyzer and DAX Query View

A report page takes several seconds to display. The analyst needs to determine whether the delay is caused by a particular visual's DAX query, rather than assuming the entire semantic model is slow.

Which workflow is most appropriate?

A. Use Performance Analyzer to identify the slow visual and inspect its DAX query; use DAX query view to investigate or test the query further  
B. Use Column Quality to measure visual rendering time  
C. Use Query Dependencies to identify the slowest report visual  
D. Change every relationship to bidirectional filtering

**Correct answer: A. Use Performance Analyzer to identify the slow visual and inspect its DAX query; use DAX query view to investigate or test the query further.**

**Explanation:** Performance Analyzer breaks down report visual performance, including time spent on DAX queries and other visual-processing activities. It can help identify which visual deserves investigation. DAX query view provides a place to inspect, write, and run DAX queries for further analysis. Changing relationship directions without evidence can introduce ambiguity and worsen performance.

---

## Question 6 — Query Folding and Data Reduction

A Power Query query connects to a large SQL database. It retrieves 20 million rows, performs several transformations, and then filters the data to the most recent 12 months. The analyst wants to reduce refresh time and the amount of data transferred.

What should the analyst investigate first?

A. Move the filter as early as practical and verify whether the transformations preserve query folding  
B. Load all 20 million rows and hide older rows in report visuals  
C. Replace the filter with a DAX measure  
D. Convert every column to Text before filtering

**Correct answer: A. Move the filter as early as practical and verify whether the transformations preserve query folding.**

**Explanation:** Query folding translates eligible Power Query transformations into operations performed by the source system. Applying a selective filter early can reduce the rows retrieved and processed. The analyst should verify folding for the actual connector and transformation sequence; not all operations can fold.

---

## Question 7 — Drillthrough vs. Tooltip

A sales report includes a summary page showing revenue by sales territory. Stakeholders want to right-click a territory and navigate to a dedicated detail page showing its customers, products, and transactions. The destination page should automatically receive the selected territory as a filter.

Which feature should the analyst configure?

A. Report-page tooltip  
B. Drillthrough  
C. Bookmark  
D. Sync slicer

**Correct answer: B. Drillthrough.**

**Explanation:** Drillthrough navigates from a source visual to a detail page while passing the selected data context as drillthrough filters. A report-page tooltip displays additional information when users hover over a data point; it is not intended for full-page navigation.

---

## Question 8 — Slicer Synchronization and Visual Interactions

A report has three pages: Executive Summary, Regional Analysis, and Product Analysis. A Date slicer on the Executive Summary page should retain the same selection on the other two pages. However, a separate Product slicer should affect only the Product Analysis page.

What should the analyst configure?

A. Sync the Date slicer across all three pages, but leave the Product slicer unsynchronized  
B. Sync both slicers across all pages  
C. Use Edit Interactions to synchronize the Date slicer across pages  
D. Create a bookmark for every possible Date selection

**Correct answer: A. Sync the Date slicer across all three pages, but leave the Product slicer unsynchronized.**

**Explanation:** Sync slicers controls whether a slicer's selection is shared across report pages. The Date slicer can be synchronized across all three pages, while the Product slicer remains local to its page. Edit Interactions controls how visuals on the same page affect one another; it does not synchronize slicer selections between pages.

---

## Question 9 — Incremental Refresh

A company imports several years of transaction data. New transactions arrive daily, and historical transactions are rarely changed. A full refresh takes too long. The analyst wants to refresh recent data while retaining previously loaded historical partitions.

What should the analyst configure?

A. A calculated table that filters the latest month  
B. Incremental refresh using required date/time parameters and a refresh policy  
C. DirectQuery for every dimension and fact table  
D. A report-level relative date filter

**Correct answer: B. Incremental refresh using required date/time parameters and a refresh policy.**

**Explanation:** Incremental refresh partitions data by a date/time column and refreshes the configured recent period rather than reloading the entire historical range on every refresh. Power Query parameters named `RangeStart` and `RangeEnd` are used to define the refresh window. The source and transformations should support the required filtering, ideally with query folding.

---

## Question 10 — Gateway, Credentials, and Scheduled Refresh

A Power BI semantic model connects to an on-premises SQL Server database. Refresh succeeds in Power BI Desktop but fails after publishing to the Power BI Service. The source server is not accessible from the public cloud.

What should the administrator configure or verify first?

A. An on-premises data gateway, with the correct data source mapping and credentials configured in the Service  
B. A report-page tooltip  
C. A sensitivity label on the semantic model  
D. A second relationship between the fact and dimension tables

**Correct answer: A. An on-premises data gateway, with the correct data source mapping and credentials configured in the Service.**

**Explanation:** The Power BI Service needs a gateway to reach an on-premises data source. The gateway must be online, and the semantic model's connection must be mapped to the correct gateway data source with valid credentials. Desktop refresh success does not establish that the Service has the required gateway configuration.

---

## Quick Review

| Topic | Key exam distinction |
|---|---|
| Direct Lake | Uses data in OneLake without importing a separate copy into the semantic model |
| Role-playing dimensions | One logical dimension can serve multiple roles, such as Order Date and Ship Date |
| `CALCULATE` | Changes filter context; filters on the same column replace existing filters by default |
| `KEEPFILTERS` | Intersects a filter with existing filters rather than replacing them |
| Semi-additive measures | Balances are often additive across accounts but not across time |
| Performance Analyzer | Identifies visual-level performance components and helps locate slow visuals |
| DAX query view | Lets analysts write, inspect, and run DAX queries |
| Query folding | Pushes eligible Power Query transformations to the source |
| Drillthrough | Navigates to a detail page while passing filter context |
| Sync slicers | Shares slicer selections across report pages |
| Incremental refresh | Refreshes configured recent partitions instead of all historical data |
| On-premises gateway | Enables the Power BI Service to access supported on-premises sources |

## Exam Strategy

- Read the requirement carefully: **freshness**, **performance**, **security**, and **usability** can point to different solutions.
- Do not assume DirectQuery is always the best choice for large datasets; consider source capacity, query performance, and freshness requirements.
- Distinguish model-level behavior from report-level behavior. Relationships and DAX affect the semantic model; interactions, bookmarks, tooltips, and drillthrough affect report experiences.
- When a question asks what to investigate, choose a diagnostic feature before making broad model changes.
- Pay attention to filter context. `CALCULATE`, `KEEPFILTERS`, and `USERELATIONSHIP` solve different problems.

## Microsoft Exam Reference

Skills measured as of April 20, 2026:  
https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/pl-300
