# PL-300 Advanced Practice Question Bank

> Reusable instructor handout. Each question includes the correct answer and a brief explanation.

---

## Q1. Query Folding
A SQL Server query stops folding after adding a custom M function. Refresh performance becomes poor.

**Answer:** B — Rewrite the logic so it executes in SQL.

**Why:** Preserving query folding pushes work to the source instead of Power BI.

---

## Q2. Composite Model
You have a large Azure SQL Sales table and a small Excel Budget table.

**Answer:** Import Excel + DirectQuery SQL (Composite Model).

**Why:** Keeps the large table in SQL while providing fast access to small lookup/budget data.

---

## Q3. DAX Filter Context
A KPI should ignore Region slicers but respect Year and Product.

**Answer:** `CALCULATE([Total Sales], REMOVEFILTERS(Region))`

**Why:** Removes only the Region filter.

---

## Q4. Relationships
A Customer dimension uses bidirectional filtering with Sales, causing ambiguity.

**Answer:** Change to Single-direction filtering.

**Why:** Single-direction relationships are preferred in a star schema.

---

## Q5. Visual Selection
Which visual explains what factors influence premium purchases?

**Answer:** Key Influencers

**Why:** It identifies statistically significant drivers.

---

## Q6. Drill Through
Users want to right-click Canada and open a page filtered to Canada.

**Answer:** Drill Through

**Why:** Drill Through opens another report page while passing filter context.

---

## Q7. Dynamic RLS
500 sales reps should only see their own customers.

**Answer:** Dynamic RLS using `USERPRINCIPALNAME()`.

**Why:** One role scales better than hundreds of static roles.

---

## Q8. Certified Semantic Model
A certified semantic model is already used by many reports.

**Answer:** Connect using a Live Connection.

**Why:** Reuses measures, relationships, and governance.

---

## Q9. Incremental Refresh
A model reloads 5 years every refresh.

**Answer:** Configure RangeStart/RangeEnd and Incremental Refresh.

**Why:** Only recent partitions refresh.

---

## Q10. Model Optimization
A model contains unused large text columns.

**Answer:** Remove unused columns in Power Query.

**Why:** Text columns compress poorly and increase model size.

---

## Q11. High Cardinality
A TransactionID column is unique for every row and never used.

**Answer:** Remove it.

**Why:** High-cardinality columns consume significant memory.

---

## Q12. Auto Date/Time
A model has Auto Date/Time enabled with many date columns.

**Answer:** Disable Auto Date/Time and create one marked Date table.

**Why:** Auto Date/Time creates hidden date tables for every eligible date column.

---

## Q13. Time Intelligence
Need sales for the same period last year.

**Answer:** `SAMEPERIODLASTYEAR()`

**Why:** Shifts the current filter context back exactly one year.

---

## Q14. YTD Comparison
Need Year-to-Date this year versus last year.

**Answer:** `TOTALYTD()` + `SAMEPERIODLASTYEAR()`

**Why:** Combines YTD calculation with prior-year comparison.

---

## Q15. Cell-Level Error
Only a few rows show Error after changing a data type.

**Answer:** Cell-level error.

**Why:** Individual cells fail while the query continues.

---

## Q16. Step-Level Error
An Applied Step references a column removed earlier.

**Answer:** Step-level error.

**Why:** The entire step fails and no preview is returned.

---

## Q17. Keep Errors
You want to investigate only failing records.

**Answer:** Keep Errors.

**Why:** Filters the table to only rows containing errors.

---

## Q18. Remove Errors
What happens when Remove Errors is used?

**Answer:** Rows containing errors are removed.

**Why:** Entire records are removed, not just the error cells.

---

## Q19. Replace Errors
Business rules say invalid numeric values should become 0.

**Answer:** Replace Errors.

**Why:** Substitute a default value instead of removing rows.

---

## Q20. Formula.Firewall
Combining Excel and SQL produces a Formula.Firewall error.

**Answer:** Privacy levels are preventing source combination.

**Why:** Power Query protects data movement across sources.

---

## Q21. Tenant Settings
Users should share internally but never publish reports publicly.

**Answer:** Disable Publish to Web.

**Why:** Prevents anonymous public links while preserving internal sharing.

---

## Q22. Workspace Roles
Emma edits reports, Ryan views only, Sophia views only East region.

**Answer:** Emma = Member, Ryan = Viewer, Sophia = Viewer + Dynamic RLS.

**Why:** Workspace roles control content access; RLS controls data visibility.

---

## Q23. Dual Storage Mode
Why use Dual for dimension tables?

**Answer:** They behave as Import or DirectQuery depending on the query.

**Why:** Improves performance in composite models.

---

## Q24. Aggregation Tables
700M-row DirectQuery fact table is slow.

**Answer:** Create Import aggregation tables.

**Why:** Summary queries are answered from memory.

---

## Q25. Gateway
Refresh works in Desktop but fails after publishing from on-prem SQL.

**Answer:** Install/configure an On-premises Data Gateway.

**Why:** Fabric Service cannot directly reach local SQL Server.

---

## PL-300 Best Practices to Remember

- Remove unused columns before loading.
- Remove unused high-cardinality columns.
- Prefer measures over calculated columns when possible.
- Build a star schema.
- Preserve query folding.
- Use one marked Date table instead of Auto Date/Time.
- Use Incremental Refresh for large historical datasets.
- Reuse Certified Semantic Models.
- Use Dynamic RLS for scalable security.
- Use Single-direction relationships unless a business case requires otherwise.
