# Chapter 8 — Power BI Service, Workspaces, Security, and Deployment

## Microsoft Power BI Data Analyst Associate (PL-300)

---

# Chapter Objectives

After completing this chapter, learners should understand:

* The purpose of Power BI Service
* Workspace roles and permissions
* Difference between publishing reports and publishing apps
* Semantic model permissions
* Read vs Build permissions
* Row-Level Security (RLS)
* Endorsement
* Deployment concepts
* Data lineage
* Governance features

---

# 8.1 Power BI Desktop vs Power BI Service

## Power BI Desktop

Used for development:

* Connecting to data
* Power Query transformations
* Data modeling
* DAX calculations
* Creating reports

Think:

> Where analysts build solutions

---

## Power BI Service

Used for deployment and management:

* Publishing reports
* Sharing content
* Managing workspaces
* Refresh schedules
* Security
* Collaboration

Think:

> Where organizations distribute solutions

---

# 8.2 Workspaces

A workspace is a collaborative container for Power BI content.

A workspace can contain:

* Reports
* Dashboards
* Semantic models
* Dataflows
* Paginated reports

Typical workflow:

```
Power BI Desktop

        ↓

Workspace

        ↓

Power BI App

        ↓

End Users
```

---

# 8.3 Workspace Roles

Power BI has four workspace roles:

1. Admin
2. Member
3. Contributor
4. Viewer

The PL-300 frequently tests the differences between these roles.

---

# 8.4 Workspace Role Detailed Comparison

| Capability                   | Admin | Member   | Contributor | Viewer |
| ---------------------------- | ----- | -------- | ----------- | ------ |
| View reports                 | ✅     | ✅        | ✅           | ✅      |
| Interact with reports        | ✅     | ✅        | ✅           | ✅      |
| Create reports               | ✅     | ✅        | ✅           | ❌      |
| Edit reports                 | ✅     | ✅        | ✅           | ❌      |
| Publish reports to workspace | ✅     | ✅        | ✅           | ❌      |
| Create semantic models       | ✅     | ✅        | ✅           | ❌      |
| Modify semantic models       | ✅     | ✅        | ✅           | ❌      |
| Delete reports               | ✅     | ✅        | ✅           | ❌      |
| Share reports                | ✅     | ✅        | Limited     | ❌      |
| Manage workspace users       | ✅     | Limited* | ❌           | ❌      |
| Change workspace settings    | ✅     | Limited* | ❌           | ❌      |
| Publish/update an App        | ✅     | ✅        | ❌           | ❌      |
| Add/remove workspace members | ✅     | Limited* | ❌           | ❌      |

*Some capabilities depend on tenant settings and permissions.

---

# 8.5 The Most Important PL-300 Distinction

## Publishing a Report vs Publishing an App

These are different actions.

---

## Publish Report

Meaning:

"Upload my report into the workspace."

Example:

Power BI Desktop:

```
Publish

↓

Sales Workspace

↓

Sales Report
```

Contributor:

✅ Can publish reports to a workspace

---

## Publish App

Meaning:

"Package workspace content and distribute it to users."

Example:

```
Workspace Content

↓

Publish App

↓

500 Employees
```

Contributor:

❌ Cannot publish Apps

Member/Admin:

✅ Can publish Apps

---

# PL-300 Exam Rule

If the question says:

"The user needs to create and publish reports but should not manage workspace permissions."

Answer:

✅ Contributor

---

If the question says:

"The user needs to publish an organizational App."

Answer:

✅ Member or Admin

---

# 8.6 Workspace Role Scenarios

## Scenario 1

A developer needs to:

* Build reports
* Edit reports
* Publish reports

They should not:

* Add users
* Change workspace settings

Correct:

✅ Contributor

---

## Scenario 2

A manager needs to:

* Review reports
* Publish an App
* Manage workspace content

Correct:

✅ Member

---

## Scenario 3

An administrator needs complete control.

Correct:

✅ Admin

---

# 8.7 Apps

Apps are designed for distributing finished content.

They provide:

* Controlled distribution
* Read-only consumption
* Better user experience

Example:

Sales Department App:

Contains:

* Sales dashboard
* Regional reports
* Forecast report

---

# Workspace vs App

| Workspace              | App                       |
| ---------------------- | ------------------------- |
| Development area       | Distribution method       |
| Analysts collaborate   | Users consume content     |
| Editing allowed        | Usually read-only         |
| Contains all artifacts | Contains selected content |

---

# 8.8 Semantic Model Permissions

Semantic models have additional permissions.

Important permissions:

* Read
* Build
* Reshare

---

# Read Permission

Allows:

✅ View reports using the model

Does not allow:

❌ Create new reports

---

# Build Permission

Allows:

✅ Create new reports
✅ Analyze data
✅ Connect Excel to the semantic model

---

# Read vs Build

| Permission | View Existing Reports | Create New Reports |
| ---------- | --------------------- | ------------------ |
| Read       | ✅                     | ❌                  |
| Build      | ✅                     | ✅                  |

---

# PL-300 Scenario

A user wants to create their own report using an existing certified semantic model.

Required:

✅ Build permission

---

# 8.9 Row-Level Security (RLS)

RLS controls:

> Which rows of data a user can see

Example:

Sales table:

| Region | Sales |
| ------ | ----- |
| East   | 5000  |
| West   | 7000  |

Regional manager:

East

Sees:

| Region | Sales |
| ------ | ----- |
| East   | 5000  |

---

# Static RLS

Fixed rule:

```DAX
Region = "East"
```

---

# Dynamic RLS

Uses the current user.

Example:

```DAX
USERPRINCIPALNAME()
```

Example:

```
John@company.com

↓

East Region
```

---

# RLS Does NOT Control:

❌ Who can edit reports

❌ Who can publish reports

❌ Workspace access

Those are controlled by permissions.

---

# 8.10 Endorsement

Organizations can identify trusted content.

---

# Promoted

Meaning:

"This content is useful."

Anyone with permission can promote content.

---

# Certified

Meaning:

"This content has been reviewed and approved."

Usually requires:

* Administrator approval
* Organizational process

---

# Promoted vs Certified

| Promoted            | Certified           |
| ------------------- | ------------------- |
| Recommended content | Officially approved |
| Lower trust         | Higher trust        |
| User-driven         | Organization-driven |

---

# 8.11 Data Lineage

Lineage shows dependencies between objects.

Example:

```
SQL Database

↓

Dataflow

↓

Semantic Model

↓

Report

↓

Dashboard
```

Useful for:

* Troubleshooting
* Impact analysis
* Understanding dependencies

---

# 8.12 Deployment Pipelines

Deployment pipelines support:

Development → Test → Production

Example:

```
Developer Workspace

↓

Testing Workspace

↓

Production Workspace
```

Benefits:

* Safer releases
* Testing before publishing
* Better governance

---

# 8.13 Sensitivity Labels

Sensitivity labels classify content.

Examples:

* Public
* Internal
* Confidential
* Highly Confidential

Used for:

* Security
* Compliance
* Governance

---

# Common PL-300 Exam Traps

---

## Trap 1

Contributor can publish Apps.

❌ Incorrect

Contributor can publish reports to the workspace but cannot publish Apps.

---

## Trap 2

Viewer can edit reports.

❌ Incorrect

Viewer is consumption only.

---

## Trap 3

Build permission allows workspace editing.

❌ Incorrect

Build allows creating reports from a semantic model.

---

## Trap 4

RLS controls report access.

❌ Incorrect

RLS controls data visibility only.

---

## Trap 5

Certified means Microsoft approved the content.

❌ Incorrect

The organization certifies the content.

---

## Trap 6

Workspace and App are the same thing.

❌ Incorrect

Workspace = development/collaboration.

App = distribution.

---

# Chapter 8 Practice Exam Questions

---

# Question 1

A user needs to:

* Create reports
* Modify reports
* Publish reports to a workspace

The user should NOT:

* Manage workspace users

Which role should be assigned?

A. Viewer

B. Contributor

C. Member

D. Admin

## Correct Answer

✅ B. Contributor

## Explanation

Contributor can create and publish reports to the workspace but cannot manage permissions.

---

# Question 2

A user needs to distribute finalized reports to hundreds of employees through an organizational application.

Which permission is required?

A. Viewer

B. Contributor

C. Member

D. Build

## Correct Answer

✅ C. Member

## Explanation

Publishing an App requires Member or Admin privileges.

---

# Question 3

A user can view reports but needs to create new reports using an existing semantic model.

What permission is required?

A. Read

B. Build

C. Viewer

D. Contributor

## Correct Answer

✅ B. Build

---

# Question 4

A company wants each salesperson to only see their assigned customers.

What should be implemented?

A. Workspace roles

B. Row-Level Security

C. Apps

D. Deployment pipelines

## Correct Answer

✅ B. Row-Level Security

---

# Question 5

A company wants approved trusted semantic models identified for analysts.

What should be used?

A. Promoted

B. Certified

C. Viewer

D. Bookmark

## Correct Answer

✅ B. Certified

---

# Question 6

An analyst wants to understand which reports will break if a semantic model changes.

Which feature should be used?

A. Lineage view

B. Refresh schedule

C. Conditional formatting

D. Gateway

## Correct Answer

✅ A. Lineage view

---

# Chapter 8 Summary

| Requirement                        | Solution                 |
| ---------------------------------- | ------------------------ |
| Build reports                      | Contributor/Member/Admin |
| Publish reports to workspace       | Contributor+             |
| Publish Apps                       | Member/Admin             |
| Manage workspace users             | Admin                    |
| View only                          | Viewer                   |
| Create reports from semantic model | Build permission         |
| Restrict visible data              | RLS                      |
| Trusted content                    | Certified                |
| Understand dependencies            | Lineage                  |
| Move solutions safely              | Deployment Pipelines     |

---

# Next Chapter

## Chapter 9 — Storage Modes, Connectivity, and Performance

Topics:

* Import
* DirectQuery
* Live Connection
* Composite Models
* Dual Storage Mode
* Gateways
* Query Folding
* Dataflows
* Performance Optimization
* PL-300 Architecture Scenarios