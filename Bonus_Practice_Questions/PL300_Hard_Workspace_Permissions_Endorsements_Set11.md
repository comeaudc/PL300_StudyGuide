# PL-300 Hard Scenario Practice — Set 11
## Workspace roles, permissions, endorsements, and mixed exam topics

These are original, challenging PL-300-style practice questions—not official Microsoft exam questions. Choose the **best** answer. Answers and explanations follow each question.

---

### 1. Workspace roles: least privilege for report consumers

A Power BI workspace contains reports and semantic models used by 80 department employees. Employees must view reports and interact with filters, but must not edit content or publish new reports. Which workspace role is most appropriate?

A. Admin  
B. Member  
C. Contributor  
D. Viewer

**Correct answer: D — Viewer**

**Explanation:** Viewer is the read-only workspace role. Admin, Member, and Contributor provide content-management or editing capabilities that these users do not need. Export behavior is separately governed by tenant, report, and semantic-model settings.

---

### 2. Workspace roles and row-level security

A regional manager is assigned to an RLS role that filters Sales to the manager's region. The manager is also added to the workspace as a Contributor. The manager reports seeing sales for every region. What is the best explanation and corrective action?

A. RLS does not support text columns; change Region to a number  
B. Contributors have edit permissions and are not restricted by RLS; give the manager read-only access, such as Viewer or app access, and assign the RLS role  
C. RLS works only in Power BI Desktop  
D. Build permission overrides RLS; remove Build permission

**Correct answer: B**

**Explanation:** RLS is enforced for read-only consumers. Workspace Admin, Member, and Contributor roles have edit permissions and are not restricted by RLS in the same way. Use Viewer or app access for users who must be restricted by RLS. Build permission is not the cause.

---

### 3. Build permission versus workspace role

A business analyst needs to create a new report using an existing certified semantic model. The analyst must not modify the semantic model or manage the workspace. What should the owner grant?

A. Admin workspace role  
B. Contributor workspace role  
C. Build permission on the semantic model  
D. Member workspace role

**Correct answer: C — Build permission**

**Explanation:** Build permission allows a user to create new content, such as reports, based on a semantic model. It does not grant workspace-management rights or permission to edit the semantic model itself.

---

### 4. Endorsements: promoted versus certified

A department analyst created a useful semantic model. The department recommends it for reuse, but it has not gone through the organization's formal central review and approval process. Which endorsement is the best fit?

A. Certified  
B. Promoted  
C. Sensitivity labeled  
D. Published

**Correct answer: B — Promoted**

**Explanation:** Promoted indicates that content is considered valuable and ready for broader reuse. Certified is intended for content that has met the organization's formal quality and approval standards.

---

### 5. Endorsements: restricting certification authority

An organization wants only members of its BI governance team to certify semantic models. Report authors should still be able to promote their own content when appropriate. What should the Power BI administrator configure?

A. Give every report author the Admin role  
B. Configure the tenant's certification settings to specify authorized users or security groups  
C. Disable promoted endorsements  
D. Give all users Build permission on every semantic model

**Correct answer: B**

**Explanation:** Certification authority can be controlled through Power BI/Fabric tenant settings by specifying authorized users or security groups. This separates formal certification from ordinary content creation and promotion.

---

### 6. Workspace access: publishing versus consuming an app

A BI team publishes a Power BI app from a workspace. Employees should consume the app but should not be added as workspace members or receive permission to edit reports. What is the most appropriate approach?

A. Add every employee as a Contributor  
B. Distribute the app and grant access through its audience configuration  
C. Give every employee Admin access  
D. Share the workspace credentials

**Correct answer: B**

**Explanation:** Apps provide a controlled way to distribute content without granting workspace editing roles. Configure the app audience to expose only intended content. Review semantic-model permissions as well if users need additional capabilities.

---

### 7. Semantic model permissions: report sharing

A report author shares a report with a colleague. The colleague can view the report but cannot create a separate report from its underlying semantic model. Which permission is most directly needed?

A. Build permission on the semantic model  
B. Admin role on the workspace  
C. Reshare permission on the report only  
D. Permission to edit the report theme

**Correct answer: A — Build permission**

**Explanation:** Viewing a report does not automatically grant permission to build new reports from its semantic model. Build permission enables downstream report creation and is distinct from workspace roles and report viewing access.

---

### 8. Sensitivity labels and exporting data

A semantic model is labeled Confidential. A user creates a report from the model and exports data to an Excel file. The organization wants the sensitivity classification to remain associated with supported exported files. Which statement best describes sensitivity labels?

A. They replace workspace permissions and RLS  
B. They classify and help protect content; supported downstream content and exports can inherit the label  
C. They automatically prevent every user from exporting data  
D. They make the semantic model certified

**Correct answer: B**

**Explanation:** Sensitivity labels classify content and can provide protection through supported information-protection capabilities. Labels can be inherited by supported downstream content and export formats. They do not replace access permissions or RLS, and a label does not itself certify content or universally block exports.

---

### 9. Workspace roles: choosing between Member and Contributor

A developer must publish reports and update semantic models in a workspace. The developer does not need to manage workspace access, add members, or delete the workspace. Which role is generally the best fit?

A. Viewer  
B. Contributor  
C. Member  
D. Admin

**Correct answer: B — Contributor**

**Explanation:** Contributor can create, edit, and publish workspace content without the broader workspace-management capabilities associated with Member and Admin. Admin should be reserved for workspace administrators.

---

### 10. Endorsements and discovery: finding trusted reusable content

An organization has many semantic models. Users need to identify models that have passed a formal governance review rather than models that an individual author simply recommends. Which characteristic should users look for?

A. Promoted endorsement  
B. Certified endorsement  
C. Viewer workspace role  
D. Build permission

**Correct answer: B — Certified endorsement**

**Explanation:** Certified is the stronger endorsement and signals that content has met the organization's defined certification criteria. Promoted indicates recommended content but does not necessarily mean it completed a formal governance review. Build permission and workspace roles control access, not content quality or approval status.

---

## Quick review: concepts tested

- Workspace roles: Admin, Member, Contributor, Viewer
- Least-privilege access for report consumers
- RLS behavior for read-only users versus workspace editors
- Build permission versus workspace access
- App audiences versus workspace membership
- Report sharing versus semantic-model permissions
- Promoted versus certified endorsements
- Tenant controls for certification authority
- Sensitivity labels, inheritance, and export protection
- Choosing Contributor versus Member or Admin

## Exam reminders

- **Viewer** is the read-only workspace role; use it when consumers must remain subject to RLS.
- **Contributor** can create and edit content but is not a workspace administrator.
- **Build** allows downstream content creation from a semantic model; it is not the same as workspace edit access.
- **Promoted** means recommended for reuse; **Certified** means it met formal organizational criteria.
- **Sensitivity labels** classify and help protect information; they do not replace RLS, permissions, or endorsement.
