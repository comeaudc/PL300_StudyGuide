# PL-300 Hard Scenario Practice: Security, Connectivity, Endorsement, and Sensitivity

**Difficulty:** Hard  
**Format:** 10 scenario-based multiple-choice questions with answers and explanations immediately after each question.

These are original practice questions for PL-300 preparation, not official Microsoft exam questions. They focus on nuanced distinctions and common exam traps.

---

## Question 1 — Workspace Roles and RLS

A company publishes a semantic model containing sales data for four regions. A regional manager should view only their region's data. The manager needs to interact with reports but must not edit the semantic model or reports.

The manager is added to the workspace as a **Contributor** and assigned to the appropriate RLS role. However, the manager can see sales for every region.

What is the best explanation and correction?

A. RLS does not work in the Power BI Service; move the model to DirectQuery.  
B. Contributor permissions allow editing, so the user is not restricted by RLS; give the manager Viewer access instead.  
C. The manager needs Member access for RLS to apply.  
D. RLS applies only to report pages, so create a separate page for each region.

**Correct answer: B. Contributor permissions allow editing, so the user is not restricted by RLS; give the manager Viewer access instead.**

**Explanation:** RLS restricts data for users with read-only access, such as workspace Viewers and consumers of shared content. Workspace roles with edit permissions—Contributor, Member, and Admin—are not constrained by RLS in the same way. Assign the manager Viewer access and add them to the appropriate RLS role.

---

## Question 2 — Dynamic RLS

A sales semantic model contains a `SalespersonEmail` column. Each salesperson should see only rows where `SalespersonEmail` matches their organizational account. The company has hundreds of salespeople, and administrators do not want to maintain hundreds of manually assigned user lists.

Which approach best meets the requirement?

A. Create a separate static RLS role for every salesperson.  
B. Create a dynamic RLS role using `USERPRINCIPALNAME()` in a filter expression and assign users or groups to that role.  
C. Use a report-level filter based on the salesperson's name.  
D. Create a bookmark for each salesperson.

**Correct answer: B. Create a dynamic RLS role using `USERPRINCIPALNAME()` in a filter expression and assign users or groups to that role.**

**Explanation:** Dynamic RLS evaluates the identity of the signed-in user and compares it with a value in the model. A role filter can use `USERPRINCIPALNAME()` to match the current user's sign-in identity to `SalespersonEmail`. Users still need to be assigned to the role in the Service; the DAX expression does not automatically grant role membership.

---

## Question 3 — RLS Across Related Tables

A model uses a star schema with `DimRegion` related one-to-many to `FactSales`. The analyst creates an RLS filter on `DimRegion[RegionName]` so regional users see only their region. The relationship uses single-direction filtering from `DimRegion` to `FactSales`.

What should the analyst expect?

A. The region filter propagates from the dimension to the sales fact table, restricting visible sales rows.  
B. The region filter cannot affect the fact table unless the relationship is bidirectional.  
C. RLS filters only the dimension table and never affects related fact tables.  
D. The analyst must create a separate RLS role for every row in the fact table.

**Correct answer: A. The region filter propagates from the dimension to the sales fact table, restricting visible sales rows.**

**Explanation:** In a typical star schema, a one-to-many relationship with single-direction filtering from dimension to fact allows the RLS filter on the dimension to restrict related fact rows. Bidirectional filtering is not automatically required and should not be enabled without a modeling reason.

---

## Question 4 — Import vs. DirectQuery: Operational Requirements

A business has a 40-million-row sales table in a supported SQL database. Reports must reflect changes made in the source within a few minutes. The database team requires queries to run against the source, and the Power BI model must not import the detailed sales rows.

Which storage mode best fits the requirement?

A. Import, with a daily scheduled refresh  
B. DirectQuery  
C. Import, with incremental refresh only  
D. A calculated table in Import mode

**Correct answer: B. DirectQuery.**

**Explanation:** DirectQuery keeps the detailed data in the source and sends queries to that source as users interact with reports. It is appropriate when source-level querying and fresher data are requirements. It also makes report performance dependent on the source system, network, query design, and concurrency. Incremental refresh can reduce the amount of data refreshed in Import mode, but it still imports data.

---

## Question 5 — Import vs. DirectQuery: Performance Trade-off

A report uses DirectQuery against an operational database. Users report slow visuals during peak business hours. The source database is heavily used by operational applications. The business can accept data that is refreshed every two hours, and the dataset fits comfortably within the applicable model size limits.

What is the most appropriate recommendation?

A. Keep DirectQuery because it always provides faster report performance.  
B. Switch to Import mode and configure an appropriate refresh schedule.  
C. Switch every table to Dual storage mode without evaluating the model.  
D. Add more visuals so Power BI can cache the results.

**Correct answer: B. Switch to Import mode and configure an appropriate refresh schedule.**

**Explanation:** Import mode can improve interactive performance because queries are served from the in-memory semantic model rather than repeatedly querying the operational source. The accepted two-hour freshness requirement makes scheduled refresh a reasonable trade-off. Dual mode is a modeling option for certain composite-model scenarios, not a universal performance fix.

---

## Question 6 — Composite Models and Dual Storage

A semantic model contains a large `FactSales` table in DirectQuery and smaller dimension tables in Import mode. The analyst wants dimension tables to be usable efficiently with the DirectQuery fact table while retaining their imported data.

Which storage mode may be appropriate for the dimension tables in this composite model?

A. DirectQuery for every dimension, regardless of source  
B. Dual  
C. Direct Lake for every table  
D. DirectQuery with automatic date/time enabled

**Correct answer: B. Dual.**

**Explanation:** Dual storage mode allows a table to behave as Import or DirectQuery depending on the query context. It is commonly used for dimension tables in composite models so they can participate efficiently with DirectQuery fact tables while also benefiting from in-memory data. Whether Dual is available and appropriate depends on the model's sources and design.

---

## Question 7 — Promoted vs. Certified Content

An organization wants employees to identify useful semantic models. Department analysts should be able to mark a model as recommended for broader use. Separately, the BI governance team must identify models that have passed a formal review and meet organizational standards.

Which statement correctly distinguishes the two endorsement levels?

A. Promoted content requires tenant administrator approval; certified content can be assigned by any report author.  
B. Promoted content can be marked by content owners or users with the required permissions; certified content requires an authorized certification process established by the organization.  
C. Promoted and certified mean the same thing; both are automatic when a model is published.  
D. Certified content is only available for reports, not semantic models.

**Correct answer: B. Promoted content can be marked by content owners or users with the required permissions; certified content requires an authorized certification process established by the organization.**

**Explanation:** Promotion is a self-service endorsement that signals content is valuable and ready for broader use. Certification is a stronger organizational endorsement controlled through the organization's certification process and authorized users. Certification criteria and permissions are configured by the organization's Power BI/Fabric governance administrators.

---

## Question 8 — Sensitivity Labels and Sharing

A semantic model is labeled **Confidential** using an organizational sensitivity label. An analyst downloads a report to a supported file format and shares it externally. The analyst assumes the sensitivity label alone guarantees that every recipient will be blocked from opening the file.

Which statement is most accurate?

A. Every sensitivity label automatically blocks external sharing, regardless of its configuration.  
B. Sensitivity labels classify content and may apply protection such as encryption when configured; the label alone does not guarantee that every external recipient is blocked.  
C. Sensitivity labels are only visual tags and can never apply protection.  
D. Sensitivity labels replace workspace permissions and RLS.

**Correct answer: B. Sensitivity labels classify content and may apply protection such as encryption when configured; the label alone does not guarantee that every external recipient is blocked.**

**Explanation:** Sensitivity labels help classify and protect organizational content. Depending on the label configuration and supported file or export path, protection such as encryption may persist with exported content. A label is not a substitute for access controls, sharing policies, workspace permissions, or RLS. External access depends on the label's protection settings and the organization's policies.

---

## Question 9 — Sensitivity Labels on Exported Content

A user exports data from a Power BI report to an Excel file. The organization expects the exported file to retain the report's sensitivity classification and associated protection where supported. The exported file is opened outside Power BI.

What should the administrator verify?

A. That the sensitivity label is configured and the export format/path supports label and protection inheritance  
B. That the report has a hidden page  
C. That the semantic model uses DirectQuery  
D. That all users are workspace Members

**Correct answer: A. That the sensitivity label is configured and the export format/path supports label and protection inheritance.**

**Explanation:** Label inheritance and protection behavior depend on the sensitivity-label configuration, supported export format, and the specific export path. Administrators should validate the organization's Microsoft Purview and Power BI settings rather than assume every export inherits protection identically.

---

## Question 10 — Combining Workspace Access, RLS, and Build Permission

A report consumer needs to view a published report and create their own reports using the underlying semantic model. They should see only their assigned region. They do not need to edit the original report or semantic model.

Which permission approach best supports this requirement?

A. Add the user as a workspace Contributor and assign an RLS role.  
B. Give the user Viewer access to the workspace or share the content, grant Build permission on the semantic model, and assign the user to the appropriate RLS role.  
C. Add the user as a workspace Admin so they can create reports.  
D. Give the user Build permission only; Build automatically grants access to the report and assigns RLS.

**Correct answer: B. Give the user Viewer access to the workspace or share the content, grant Build permission on the semantic model, and assign the user to the appropriate RLS role.**

**Explanation:** Build permission allows a user to create new content based on a semantic model; it does not require giving them edit rights to the original workspace content. Keep the user in a read-only consumption context so RLS applies, and assign them to the correct RLS role. Workspace Contributor, Member, and Admin roles grant edit capabilities and are not appropriate when RLS must restrict the user's data.

---

## Quick Review

| Topic | Key exam distinction |
|---|---|
| Workspace roles | Viewer is read-only; Contributor, Member, and Admin have edit capabilities |
| RLS | Restricts data for read-only consumers; workspace users with edit permissions are not constrained by RLS |
| Dynamic RLS | Use identity functions such as `USERPRINCIPALNAME()` and assign users/groups to the role |
| RLS relationships | Dimension-to-fact filter propagation commonly supports star-schema RLS |
| Import | Data is loaded into the semantic model; refresh is needed to bring in source changes |
| DirectQuery | Data remains at the source; report queries depend on source and network performance |
| Dual | Can support dimension tables in composite models with both Import and DirectQuery behavior |
| Promoted | Self-service endorsement that content is useful and ready to share |
| Certified | Stronger endorsement controlled by an organization's authorized certification process |
| Sensitivity labels | Classify and may protect content; behavior depends on configuration and supported paths |
| Build permission | Enables creation of new reports from a semantic model; does not grant workspace edit rights |

## Hard-Question Exam Traps

- **RLS is not a replacement for workspace permissions.** A user with edit permissions in a workspace is not restricted by RLS in the same way as a Viewer.
- **Build permission is not Contributor permission.** Build enables downstream content creation without granting edit rights to the original workspace content.
- **DirectQuery is not automatically faster or more current in every practical sense.** It queries the source, so source capacity, network latency, and query complexity matter.
- **Import is not necessarily unsuitable for large data.** Consider model limits, incremental refresh, aggregation, and freshness requirements.
- **Promoted is not certified.** Certification requires an organization-controlled process.
- **A sensitivity label is not RLS.** Labels classify/protect content; RLS filters rows returned from a semantic model.
