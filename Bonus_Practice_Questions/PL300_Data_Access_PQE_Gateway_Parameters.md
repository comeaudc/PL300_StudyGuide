# PL-300 Practice Questions: Data Access, Power Query, Gateways, and Parameters

**10 original scenario-based multiple-choice questions with answers and explanations**

These questions are designed for beginner-to-lower-intermediate PL-300 practice. They are practice questions, not actual Microsoft exam questions.

## 1. Data Access: Import vs. DirectQuery

A company has a moderately sized sales database. Users want fast report interactions, and refreshing the data every morning is acceptable. Which storage mode is generally the best starting point?

A. DirectQuery, because it always provides the fastest reports  
B. Import, because data is loaded into the semantic model and can be refreshed on a schedule  
C. Live connection to a CSV file  
D. Export the database to PDF

**Answer: B. Import.**

**Explanation:** Import loads data into the Power BI semantic model, which generally supports fast interactive analysis. The model must be refreshed to bring in source changes.

## 2. Data Access: DirectQuery

A retailer has a very large supported relational database. The report must query the source data as users interact, rather than importing the entire table into the semantic model. Which option best fits this requirement?

A. Import  
B. DirectQuery  
C. Power Query's Column Quality  
D. A calculated column

**Answer: B. DirectQuery.**

**Explanation:** DirectQuery leaves data in the source and sends queries to it as users interact with the report. Performance depends on source performance, network connectivity, and model design.

## 3. Power Query Editor: Transform Before Load

An analyst connects Power BI to an Excel workbook. They need to remove blank rows, split a `FullName` column, and change `OrderDate` from Text to Date before building visuals. Where should they perform these tasks?

A. Power Query Editor  
B. The report's Format pane  
C. A dashboard tile  
D. Workspace access settings

**Answer: A. Power Query Editor.**

**Explanation:** Power Query Editor is used to clean and shape data before loading it into the model. Its applied steps can be rerun when the data is refreshed.

## 4. Power Query: Parameters for Environment Switching

An analyst develops a report using a test SQL Server. The same report will later connect to the production server. They want to change the server name in one place instead of editing several query steps. What should they use?

A. A bookmark  
B. A Power Query parameter referenced by the connection/query  
C. A slicer  
D. A calculated column

**Answer: B. A Power Query parameter referenced by the connection/query.**

**Explanation:** Parameters store reusable values such as server names, database names, folder paths, or date boundaries. Queries can reference a parameter so the value can be changed centrally.

## 5. On-Premises Data Gateway: Scheduled Refresh

A Power BI semantic model uses a database located on a company's on-premises network. The model is published to the Power BI service, and scheduled refresh must reach that database. What is commonly required?

A. An on-premises data gateway configured for the source, with valid credentials  
B. A separate report for each refresh time  
C. A DAX measure that stores the database password  
D. A bookmark that points to the server

**Answer: A. An on-premises data gateway configured for the source, with valid credentials.**

**Explanation:** A gateway commonly enables the Power BI service to securely access supported on-premises sources for refresh. The gateway and data source must be configured correctly, and credentials must be valid.

## 6. Gateway Troubleshooting: Desktop Works, Service Refresh Fails

An analyst can refresh a report successfully in Power BI Desktop. After publishing, scheduled refresh fails because the Power BI service cannot reach the on-premises database. What should the analyst or administrator check first?

A. Whether the report uses enough colors  
B. Gateway availability and configuration, data source mapping, and credentials in the service  
C. Whether every visual has a title  
D. Whether the report contains a bookmark

**Answer: B. Gateway availability and configuration, data source mapping, and credentials in the service.**

**Explanation:** Desktop can connect from the analyst's computer, but the Power BI service may need a configured gateway to reach an on-premises source. Check gateway status, the matching data source, permissions, and credentials.

## 7. Power Query: Append vs. Merge

A company receives one sales file per month. Each file has the same columns, and the analyst wants a single table containing all transactions from every month. Which Power Query operation should they use?

A. Merge Queries  
B. Append Queries  
C. Pivot Column  
D. Group By

**Answer: B. Append Queries.**

**Explanation:** Append combines tables by stacking rows. Merge joins tables using matching key columns, adding columns from the matched table.

## 8. Power Query: Unpivot Columns

A spreadsheet has columns `Product`, `January`, `February`, and `March`. The analyst wants a normalized table with one row per product and month, using columns such as `Product`, `Month`, and `Sales`. Which operation should they use?

A. Unpivot the month columns  
B. Append the same table to itself  
C. Merge on the Product column  
D. Change the Product column to Whole Number

**Answer: A. Unpivot the month columns.**

**Explanation:** Unpivot turns multiple month columns into attribute-value rows, which is often easier to model and analyze over time.

## 9. Power Query: Applied Steps

An analyst removes blank rows and changes column data types in Power Query Editor. After new data is added to the source, the analyst refreshes the model. What normally happens to those Power Query transformations?

A. They are discarded after the first load.  
B. They are applied again as part of the query's refresh process.  
C. They run only when a user clicks a visual.  
D. They are converted automatically into DAX measures.

**Answer: B. They are applied again as part of the query's refresh process.**

**Explanation:** Power Query records transformations as applied steps. When the query refreshes, those steps are evaluated against the retrieved source data.

## 10. Choose the Best Access Method

A report connects to an on-premises SQL database. The business accepts scheduled data refresh and prioritizes responsive report interactions over seeing every source change immediately. The data volume is manageable for the model. Which setup is generally the best fit?

A. Import storage mode, with a gateway configured if required for service refresh  
B. DirectQuery in every case, because it never needs source connectivity  
C. Use Power Query parameters instead of a storage mode  
D. Publish the report as a PDF and schedule a PDF refresh

**Answer: A. Import storage mode, with a gateway configured if required for service refresh.**

**Explanation:** Import is often a good fit when the data fits the model and scheduled refresh is acceptable. If the source is on-premises and the Power BI service must access it for refresh, a gateway is commonly needed.

---

## Quick Review

| Concept | Key point |
|---|---|
| **Import** | Loads data into the semantic model; refresh brings in changes |
| **DirectQuery** | Sends queries to the source as users interact |
| **Power Query Editor** | Cleans and shapes data before loading |
| **Parameter** | Stores a reusable value such as a server name or file path |
| **On-premises gateway** | Enables the service to reach supported on-premises sources when needed |
| **Gateway troubleshooting** | Check gateway status, source mapping, permissions, and credentials |
| **Append** | Stacks rows from tables |
| **Merge** | Joins tables using matching columns |
| **Unpivot** | Turns multiple columns into attribute-value rows |
| **Applied Steps** | Transformations rerun during refresh |

## Exam Tip

- **Fast interactive analysis and scheduled updates are acceptable:** consider Import.
- **Queries must use source data as users interact:** consider DirectQuery, while accounting for source performance.
- **Clean or reshape data before loading:** use Power Query.
- **Calculate a value that responds to slicers:** use a DAX measure.
- **Power BI service needs to reach an on-premises source:** check whether a gateway is required.
- **Need to switch a server or folder path centrally:** consider a Power Query parameter.
