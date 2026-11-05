# PL-300 Expert Scenario Practice — Set 12
## 10 mixed expert-level Power BI questions

These are original, challenging PL-300-style practice questions, not official Microsoft exam questions. Each scenario tests nuanced distinctions across modeling, DAX, security, refresh, connectivity, and governance.

---

### 1. Composite models, Dual dimensions, and cross-source performance

A semantic model uses a large SQL Server fact table in DirectQuery mode. A small Product dimension is imported from the same SQL Server database. A separate Excel-based Target table is imported from a file. Users analyze actual sales against targets by Product. Performance is poor when visuals combine the DirectQuery fact table with imported dimensions.

Which change is most appropriate to test first for the Product dimension?

A. Change Product to Dual storage mode  
B. Change the SQL fact table to Import and leave all other tables unchanged  
C. Change the Excel Target table to DirectQuery  
D. Set every relationship in the model to bidirectional

**Correct answer: A — Change Product to Dual**

**Explanation:** A Dual dimension can be cached like an Import table for queries that can use the cache, while behaving as DirectQuery when needed alongside DirectQuery tables. This is a common optimization for dimensions that filter DirectQuery facts. It does not guarantee every cross-source query will be fast; the Excel table can still introduce cross-source limitations.

---

### 2. DAX context transition and iterators

A model contains a Product table related one-to-many to Sales. A developer writes:

```dax
Average Product Revenue =
AVERAGEX(
    VALUES(Product[ProductKey]),
    CALCULATE(SUM(Sales[Revenue]))
)
```

Why is `CALCULATE` included inside `AVERAGEX`?

A. It converts the row context created by the iterator into filter context so the current product filters Sales  
B. It converts filter context into row context so `AVERAGEX` can iterate over Sales  
C. It removes all filters from Product before summing Sales  
D. It forces the Sales table to use DirectQuery

**Correct answer: A**

**Explanation:** `AVERAGEX` creates row context as it iterates over product keys. `CALCULATE` performs context transition, turning the current product key into filter context so related Sales rows are filtered for that product. The expression then averages the per-product revenue results.

---

### 3. Incremental refresh and late-arriving updates

A fact table contains five years of data. New rows arrive daily, but the source can update transactions as old as 45 days. The model stores five years and refreshes only the most recent 7 days. Some corrected historical transactions are not reflected after refresh.

What should you change?

A. Increase the incremental refresh refresh period to include at least the 45-day correction window  
B. Reduce the store period to 45 days  
C. Enable automatic date/time  
D. Change the table to DirectQuery without reviewing source capacity

**Correct answer: A**

**Explanation:** Incremental refresh refreshes only partitions within the configured refresh period. If the source can modify records up to 45 days old, the refresh window must include those records. The store period controls how much history is retained; it does not determine which historical partitions are refreshed.

---

### 4. RLS, bidirectional relationships, and security propagation

A model has Region, Customer, and Sales tables. Region filters Customer, and Customer filters Sales through single-direction relationships. A dynamic RLS role filters Region using the signed-in user's assigned region. The security filter does not reach Sales because the relationship path is not propagating as intended.

What should the modeler evaluate first?

A. Enable the relationship option to apply the security filter in both directions on the necessary relationship path, while checking for ambiguous paths  
B. Give all users Member access to the workspace  
C. Replace the dynamic role with a report-level filter  
D. Add a visual-level filter to every report page

**Correct answer: A**

**Explanation:** RLS propagation follows model relationships. In some designs, the relationship's security-filter direction must be configured to propagate security through the intended path. Enable bidirectional security filtering only where required and validate for ambiguous or unintended paths. Report filters are not a security boundary.

---

### 5. Query folding, native queries, and incremental refresh

A large SQL source is used for an incremental-refresh table. The Power Query query begins with a native SQL statement. The modeler adds transformations and notices that the `RangeStart` and `RangeEnd` filters are not being pushed to the source. Refresh takes much longer than expected.

What is the most important issue to investigate?

A. Whether the native query and subsequent transformations preserve folding so incremental date filters can be applied at the source  
B. Whether the report uses a custom theme  
C. Whether the Date table is marked as a date table  
D. Whether the table has a hidden key column

**Correct answer: A**

**Explanation:** Incremental refresh depends on the date-range filters being applied efficiently to the source. If query folding is broken, Power BI may retrieve and process far more data than intended. Verify folding for the range filters and use a source/query pattern that supports it.

---

### 6. Calculation groups and precedence

A semantic model contains a calculation group for time intelligence and another for currency conversion. A report applies both a Year-to-Date calculation item and a currency conversion calculation item. The result is incorrect because the order in which the calculation groups are evaluated affects the expression.

Which model property should the developer review?

A. Calculation group precedence  
B. Relationship cardinality  
C. Column data category  
D. Incremental refresh archive period

**Correct answer: A — Calculation group precedence**

**Explanation:** When multiple calculation groups affect the same measure, their precedence determines the order in which calculation items are applied. Review the precedence values and test the combined calculations, especially when one calculation item transforms the measure expression used by another.

---

### 7. Workspace permissions, Build access, and RLS

A user needs to create their own report from a shared semantic model. The model has dynamic RLS. The user must see only rows allowed by their role and must not edit the source semantic model or workspace content.

Which access pattern best meets the requirement?

A. Add the user as a Contributor and assign the RLS role  
B. Add the user as a Viewer, grant Build permission on the semantic model, and assign the user to the appropriate RLS role  
C. Add the user as a Member and remove the user's ability to export  
D. Give the user Admin access but hide the model from the navigation pane

**Correct answer: B**

**Explanation:** A read-only workspace role allows RLS to be enforced, while Build permission allows the user to create downstream reports from the semantic model. Assign the user to the appropriate RLS role. Contributor, Member, and Admin are edit-capable workspace roles and do not provide the intended RLS-restricted consumption experience.

---

### 8. Endorsement, certification, and governance

A semantic model is widely used across an organization. Its owner marks it as Promoted. The BI governance team later completes its formal review and approves it for organization-wide reuse. Users need to identify content that has passed this formal approval.

What should an authorized user do?

A. Change the endorsement to Certified, following the organization's certification process  
B. Add a sensitivity label named Certified  
C. Give all users Build permission  
D. Publish the model in an app and assume it is certified

**Correct answer: A**

**Explanation:** Promoted signals that content is recommended for reuse. Certified indicates that the content has met the organization's formal certification criteria. Certification should follow the organization's governance process and may be restricted through tenant settings to authorized users or groups.

---

### 9. Performance Analyzer versus model-level optimization

A report visual is slow. Performance Analyzer shows that the DAX query duration is high, while visual display time is low. The model contains a large fact table, several high-cardinality text columns, and multiple bidirectional relationships.

What is the best next step?

A. Focus on model and DAX optimization: inspect the generated query, simplify filter paths, review relationship directions, and remove unnecessary high-cardinality columns where appropriate  
B. Change the report theme and reduce the number of colors  
C. Increase the visual's display resolution  
D. Use Column Quality to identify missing values in every table

**Correct answer: A**

**Explanation:** A high DAX query duration points toward query/model work rather than visual rendering. Use the captured query to investigate DAX and evaluate model design. Unnecessary high-cardinality columns can increase model size, and excessive bidirectional relationships can complicate filter propagation and query plans. Make changes based on measured evidence.

---

### 10. DirectQuery limitations and measure design

A report uses a DirectQuery semantic model. A developer wants to create a calculated column that uses a complex DAX expression involving iterators and a measure, then use that column as a slicer. The expression is not supported in the DirectQuery calculated-column scenario.

What is the best alternative if the value is intended to respond dynamically to report filters?

A. Rewrite it as a measure and use it in a visual or filter context where measures are supported  
B. Convert the measure into a calculated column in the report  
C. Add a calculated table containing every possible filter combination  
D. Use a report tooltip as a replacement for the column

**Correct answer: A**

**Explanation:** Measures are evaluated at query time in the current filter context and are generally appropriate for dynamic calculations. Calculated columns are stored row-level values and have additional restrictions in DirectQuery. A measure cannot be used in every field well, such as a standard slicer; if users must slice by a persisted category, consider implementing that attribute upstream in the source or in a supported model design.

---

## Expert review checklist

- Composite models and Dual storage mode
- Context transition in DAX iterators
- Incremental refresh retention versus refresh windows
- RLS propagation and bidirectional security filtering
- Query folding requirements for incremental refresh
- Calculation group precedence
- Workspace roles, Build permission, and RLS
- Promoted versus Certified endorsements
- Performance Analyzer interpretation and model optimization
- DirectQuery calculated-column limitations versus measures
