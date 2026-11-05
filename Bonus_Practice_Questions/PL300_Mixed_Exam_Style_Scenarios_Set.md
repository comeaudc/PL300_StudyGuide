# PL-300 Mixed Scenario Practice — Exam-Style Set

**Difficulty:** Mixed (intermediate to hard)  
**Format:** 10 scenario-based multiple-choice questions  
**Answers:** Each correct answer and explanation appears immediately after its question.

These are original practice questions written in an exam-style format. They are not official Microsoft exam questions.

---

## Question 1 — Power Query: Merge Behavior

A company receives a monthly transactions file and a product reference table. Some transaction rows contain a `ProductID` that does not exist in the product reference table. The analyst must retain every transaction row and bring in the matching product description when one exists.

Which merge join kind should the analyst use?

A. Inner  
B. Left outer  
C. Right outer  
D. Full outer

**Correct answer: B. Left outer.**

**Explanation:** A left outer join keeps every row from the first (left) table and adds matching rows from the second (right) table. Transactions without a matching product remain in the result, with null values for the product fields. An inner join would discard unmatched transactions.

---

## Question 2 — Data Modeling: Relationship Cardinality

A model contains a `Customers` table with one row per customer and a `Sales` table with multiple transactions per customer. Each sale belongs to exactly one customer. The analyst needs customer attributes to filter sales.

Which relationship should be created?

A. One-to-one, with Sales filtering Customers  
B. One-to-many, with Customers on the one side and Sales on the many side  
C. Many-to-many, with bidirectional filtering  
D. Many-to-one, with Sales on the one side

**Correct answer: B. One-to-many, with Customers on the one side and Sales on the many side.**

**Explanation:** The customer key is unique in `Customers` but repeats in `Sales`. This is the standard dimension-to-fact relationship in a star schema. Single-direction filtering from Customers to Sales is generally the preferred starting point.

---

## Question 3 — DAX: Distinct Counts

A report displays the number of unique customers who made purchases. A customer can make many purchases, and the report must respond to date and product slicers.

Which measure should the analyst create?

A. `COUNT(Sales[CustomerID])`  
B. `COUNTROWS(Sales)`  
C. `DISTINCTCOUNT(Sales[CustomerID])`  
D. `SUM(Sales[CustomerID])`

**Correct answer: C. `DISTINCTCOUNT(Sales[CustomerID])`.**

**Explanation:** `DISTINCTCOUNT` counts unique values in the specified column and respects the current filter context. `COUNT` would count nonblank customer IDs on transaction rows, potentially counting the same customer multiple times.

---

## Question 4 — Data Preparation: DateTime Keys

A source table contains a `TransactionTimestamp` column with date and time values. The model has a date dimension with one row per calendar date. The analyst needs a relationship that matches transactions to the correct calendar date, regardless of the time portion.

What should the analyst do in Power Query?

A. Convert the timestamp directly to Text  
B. Extract or derive a Date-only column from the timestamp and use it for the relationship  
C. Round the timestamp to the nearest hour  
D. Create a many-to-many relationship between the timestamp and date columns

**Correct answer: B. Extract or derive a Date-only column from the timestamp and use it for the relationship.**

**Explanation:** The date dimension contains date values without time. A DateTime value such as `2026-11-03 14:30` will not match a Date value of `2026-11-03` as a relationship key. Create a Date-only column and ensure both relationship columns use compatible Date data types.

---

## Question 5 — Power BI Service: Workspace Permissions

A report author publishes a report and semantic model to a workspace. A department manager needs to view the content but should not edit reports, modify the semantic model, or change workspace content.

Which workspace role is most appropriate?

A. Admin  
B. Member  
C. Contributor  
D. Viewer

**Correct answer: D. Viewer.**

**Explanation:** Viewer is the read-only workspace role. Admin, Member, and Contributor have varying levels of content-management or editing permissions. If row-level security is also required, Viewer access is the appropriate workspace role for applying RLS restrictions to the user.

---

## Question 6 — Power Query: Query Folding

An analyst connects Power Query to a supported SQL database. After adding a custom transformation, the **View Native Query** option becomes unavailable. The analyst needs to determine whether query folding has stopped at that step.

What is the best next action?

A. Assume every step after the unavailable option is definitely incorrect  
B. Inspect the applied steps and test folding behavior around the transformation; use an appropriate folding indicator or source-side query inspection where available  
C. Delete all transformations and use DAX instead  
D. Change the semantic model to DirectQuery

**Correct answer: B. Inspect the applied steps and test folding behavior around the transformation; use an appropriate folding indicator or source-side query inspection where available.**

**Explanation:** An unavailable View Native Query option can indicate that folding is not available at that step, but it is not a universal proof that no folding occurs anywhere in the query. Inspect the transformation sequence and verify source behavior. Some connectors and steps do not expose native query viewing in the same way.

---

## Question 7 — Report Design: Drillthrough

A report includes a bar chart showing total revenue by salesperson. Managers want to select a salesperson and open a detail page that shows that salesperson's individual transactions.

Which feature should the analyst configure?

A. Drillthrough  
B. A report-page tooltip  
C. A bookmark navigator  
D. Conditional formatting

**Correct answer: A. Drillthrough.**

**Explanation:** Drillthrough passes the selected salesperson context to a dedicated detail page. A tooltip is intended to show additional information on hover, while bookmarks save report view states or navigation experiences.

---

## Question 8 — DAX: Inactive Relationships

A sales model has an active relationship between `Date[Date]` and `Sales[OrderDate]`. It also has an inactive relationship between `Date[Date]` and `Sales[ShipDate]`. A user needs a measure that calculates sales by ship date while preserving the existing model design.

Which DAX function should the analyst use inside `CALCULATE`?

A. `RELATED()`  
B. `USERELATIONSHIP()`  
C. `DISTINCT()`  
D. `CROSSFILTER()` in every case

**Correct answer: B. `USERELATIONSHIP()`.**

**Explanation:** `USERELATIONSHIP` activates an existing inactive relationship for the calculation in which it is used. This allows a measure to evaluate sales by ShipDate without changing which relationship is active for the rest of the model.

---

## Question 9 — Refresh: On-Premises Data

A semantic model refreshes successfully in Power BI Desktop but fails during scheduled refresh in the Power BI Service. Its source is a SQL Server database hosted on the organization's on-premises network.

What should the administrator check?

A. Whether the report has a date hierarchy  
B. Whether an online and correctly configured on-premises data gateway is available, with matching data source settings and valid credentials  
C. Whether the report uses a custom theme  
D. Whether all report consumers have Contributor access

**Correct answer: B. Whether an online and correctly configured on-premises data gateway is available, with matching data source settings and valid credentials.**

**Explanation:** The Power BI Service needs a gateway to reach an on-premises source. The gateway must be online, and the semantic model connection must map to the correct gateway data source with valid credentials. A successful Desktop refresh does not configure the Service gateway automatically.

---

## Question 10 — Security: Dynamic Row-Level Security

A company has one sales semantic model used by employees across several regions. Each employee should see only the rows assigned to their organizational login. The organization wants one reusable security role rather than a separate role for every employee.

Which solution is most appropriate?

A. Create a report filter that users can change themselves  
B. Create a dynamic RLS role using `USERPRINCIPALNAME()` and compare it to the user's email or login field in the model  
C. Create a separate workspace for every employee  
D. Hide the other regions' columns in the report

**Correct answer: B. Create a dynamic RLS role using `USERPRINCIPALNAME()` and compare it to the user's email or login field in the model.**

**Explanation:** Dynamic RLS uses the identity of the signed-in user to filter rows. A role filter can compare `USERPRINCIPALNAME()` with a user mapping or email column. Users or groups must still be assigned to the role in the Power BI Service. Hiding columns or adding editable report filters does not provide row-level security.

---

## Quick Review

| Skill area | Remember |
|---|---|
| Merge joins | Left outer retains every row from the first table |
| Relationships | Dimension tables usually sit on the one side; fact tables on the many side |
| Distinct counts | Use `DISTINCTCOUNT` when repeated transactions should count once per entity |
| Date relationships | Match compatible Date values; remove the time portion when joining to a date dimension |
| Workspace roles | Viewer is read-only; other workspace roles provide editing or management capabilities |
| Query folding | Verify which transformations are pushed to the source; do not infer too much from one UI indicator |
| Drillthrough | Opens a detail page with selected filter context |
| Inactive relationships | Use `USERELATIONSHIP` inside a measure's `CALCULATE` when appropriate |
| Gateway refresh | Service access to on-premises sources requires gateway configuration |
| Dynamic RLS | Use the signed-in identity to apply user-specific row filters |

## Exam Practice Reminders

- Identify the exact requirement before selecting a feature: retain unmatched rows, count unique entities, navigate to details, or restrict data.
- Distinguish Power Query transformations from DAX calculations and report interactions.
- Check relationship direction and cardinality before adding bidirectional or many-to-many relationships.
- A report filter, hidden field, or bookmark is not a substitute for RLS.
- A successful refresh in Desktop does not prove that the Power BI Service is configured to refresh the source.
