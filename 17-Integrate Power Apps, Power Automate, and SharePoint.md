# 📘 Module 17 - Integrate Power Apps, Power Automate, and SharePoint

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 8 minutes

---

# 📖 Overview

One of the biggest challenges organisations face is that business data is often spread across multiple systems. Information may exist in:

- Microsoft Lists
- SharePoint
- SQL Databases
- Excel
- Microsoft Dataverse
- CRM systems
- Third-party applications

When these systems don't communicate with one another, business processes become slower, more manual, and more prone to human error.

Microsoft Power Platform solves this problem by enabling:

- **Power Apps** to provide the user interface.
- **Power Automate** to automate business processes.
- **SharePoint / Microsoft Lists** to store business data.
- **Power BI** to analyse and visualise information.

Together, they create low-code business applications that are secure, scalable, and integrated across Microsoft 365.

The module demonstrates how these technologies work together to create connected business solutions. :contentReference[oaicite:0]{index=0}

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Explain how Power Apps, Power Automate, and SharePoint integrate.
- Create a Power Automate flow from Power Apps.
- Add Power Apps to an existing Power Automate flow.
- Build SharePoint-integrated automation.
- Create business applications directly from Microsoft Lists.
- Understand the common connector framework.
- Identify enterprise use cases for Microsoft Power Platform integration.
- Apply best practices for scalable low-code solutions.

---

# 🏗️ Microsoft Power Platform Architecture

The three core technologies each have a distinct responsibility.

```text
              USER
                │
                ▼
        Power Apps (UI)
                │
                ▼
      Power Automate (Logic)
                │
                ▼
 SharePoint / Dataverse / SQL
                │
                ▼
         Business Data
```

Each component has a dedicated role.

| Component | Primary Purpose |
|------------|----------------|
| Power Apps | User Interface |
| Power Automate | Workflow & Business Logic |
| SharePoint / Lists | Data Storage |
| Dataverse | Enterprise Data Platform |
| SQL | Relational Database |
| Power BI | Reporting & Analytics |

---

# 🧩 Understanding Each Component

## Power Apps

Power Apps provides the interface users interact with.

Examples include:

- Mobile applications
- Tablet applications
- Desktop web applications
- Inspection forms
- Approval forms
- Data entry forms

Power Apps focuses on collecting and displaying business data.

---

## Power Automate

Power Automate performs the processing behind the scenes.

Examples:

- Approvals
- Notifications
- Data synchronisation
- Email automation
- Document generation
- Record creation
- Integration with external systems

Power Apps asks Power Automate to perform business operations.

---

## SharePoint / Microsoft Lists

SharePoint commonly acts as the business data repository.

Typical data includes:

- Requests
- Projects
- Travel forms
- Assets
- Employees
- Tickets
- Approvals

Power Apps reads and writes data while Power Automate reacts to changes.

---

# 🔄 Overall Integration Pattern

```text
User Opens App
        │
        ▼
Power Apps Collects Data
        │
        ▼
Power Automate Executes Logic
        │
        ▼
SharePoint Stores Data
        │
        ▼
Emails
Approvals
Teams Notifications
SQL
Dataverse
Planner
```

Each service specialises in what it does best.

---

# 📱 Integration 1 - Adding a Flow to Power Apps

Power Apps can directly create or call Power Automate flows.

Architecture:

```text
Power Apps
     │
     ▼
Power Automate
     │
     ▼
Business Process
```

Typical workflow:

```text
Open App
     ↓
Select Power Automate
     ↓
Create New Flow
     ↓
Choose Template
     ↓
Configure Flow
     ↓
Save
```

The flow becomes available directly inside the application.

---

# 🔄 Passing Data from Power Apps

Power Apps can send information to Power Automate.

Example:

```text
Employee Name
Request Type
Department
Cost
Manager
Comments
```

Power Automate receives these parameters and continues processing.

```text
Power Apps
      ↓
Submit Request
      ↓
Power Automate
      ↓
Approval
      ↓
SharePoint
```

---

# 🔄 Returning Data to Power Apps

Power Automate can also return information back.

Examples:

```text
Request Number

Approval Status

Generated PDF

Success Message

Tracking Number
```

This creates a responsive user experience.

---

# 🔄 Integration 2 - Starting from Power Automate

Development can also begin inside Power Automate.

Architecture:

```text
Power Automate
      │
      ▼
Power Apps Trigger
      │
      ▼
Canvas App
```

Typical approach:

```text
Power Automate
      ↓
Templates
      ↓
Power Apps
      ↓
Generate Flow
```

This allows developers to build automation first and connect the app later.

---

# 📋 Power Apps Trigger

One common trigger is:

```text
Power Apps (V2)
```

This trigger waits for Power Apps to provide information.

Example:

```text
Power Apps
       ↓
Submit Form
       ↓
Power Apps Trigger
       ↓
Automation Starts
```

---

# 📄 Integration 3 - SharePoint with Power Automate

SharePoint integrates directly with Power Automate.

Architecture:

```text
SharePoint List
        │
        ▼
Power Automate
        │
        ▼
Business Process
```

A flow can be created directly from a SharePoint list.

Typical process:

```text
SharePoint List
      ↓
Integrate
      ↓
Power Automate
      ↓
Create Flow
```

The list becomes the trigger or data source for automation.

---

# 📄 SharePoint Trigger Examples

Common triggers include:

```text
Item Created
```

```text
Item Modified
```

```text
File Created
```

```text
File Modified
```

```text
Selected Item
```

Each supports different business scenarios.

---

# 📱 Integration 4 - SharePoint with Power Apps

Power Apps can also be created directly from Microsoft Lists.

Architecture:

```text
SharePoint List
       │
       ▼
Power Apps
       │
       ▼
Mobile Business Application
```

Users can quickly generate:

- Data entry forms
- Mobile applications
- Approval interfaces
- Inspection apps

without writing code.

---

# 🌐 Common Connector Framework

One of the biggest strengths of Power Platform is the connector framework.

Every application uses the same connector model.

Examples include:

- SharePoint
- SQL Server
- Dataverse
- Outlook
- Exchange
- Planner
- Teams
- Salesforce
- ServiceNow
- Google
- Twitter
- MailChimp

This enables one Power App to interact with dozens of business systems.

---

# 🔄 Complete Enterprise Architecture

```text
               User
                 │
                 ▼
          Power Apps
                 │
                 ▼
        Power Automate
                 │
      ┌──────────┼───────────┐
      ▼          ▼           ▼
 SharePoint   Dataverse     SQL
      │          │           │
      └──────────┼───────────┘
                 ▼
            Power BI
```

---

# 💼 Real-World Business Scenarios

## Employee Onboarding

```text
Power App
     ↓
Employee Form
     ↓
Power Automate
     ↓
Approvals
     ↓
SharePoint
     ↓
Create Accounts
```

---

## Travel Requests

```text
Power App
      ↓
Travel Request
      ↓
Power Automate
      ↓
Manager Approval
      ↓
SharePoint
      ↓
Notification
```

---

## Asset Requests

```text
Power App
      ↓
Request Device
      ↓
Power Automate
      ↓
Approval
      ↓
Asset Register
```

---

## Site Visit Requests

```text
Power App
      ↓
Visit Form
      ↓
Power Automate
      ↓
Approvals
      ↓
SharePoint
      ↓
Planner
```

---

## Leave Requests

```text
Employee App
      ↓
Leave Request
      ↓
Approval
      ↓
SharePoint
      ↓
Calendar Update
```

---

# 💼 Real-Life Work Applications

## International Travel Solution

The travel approval solution could be redesigned as:

```text
Power Apps
        ↓
Travel Form
        ↓
Power Automate
        ↓
Line Manager Approval
        ↓
EA Approval
        ↓
CEO Approval
        ↓
SharePoint
        ↓
Email Notifications
```

Advantages:

- Better mobile experience
- Easier data validation
- Fewer manual forms
- Richer user interface

---

## Project Site Visit Requests

Rather than Microsoft Forms:

```text
Power Apps
       ↓
Project Visit Form
       ↓
Power Automate
       ↓
Approvals
       ↓
SharePoint
```

Benefits include:

- Searchable lookups
- Validation
- Conditional controls
- Attachment support
- Offline capability
- Better user experience

---

## Joiner, Mover and Leaver

```text
HR App
      ↓
Submit JML Request
      ↓
Power Automate
      ↓
Provision Accounts
      ↓
SharePoint Tracking
```

---

## Licence Management

```text
Reviewer App
      ↓
Licence Decision
      ↓
Power Automate
      ↓
Update SharePoint
      ↓
Notify Team
```

---

## IT Service Requests

```text
Support App
      ↓
Raise Request
      ↓
Power Automate
      ↓
Create Ticket
      ↓
SharePoint
      ↓
Manager Notification
```

---

# ⭐ Benefits of Integration

Power Platform integration provides:

- Faster processes
- Reduced manual work
- Better user experience
- Mobile capability
- Centralised data
- Reusable automation
- Better reporting
- Improved governance
- Reduced development effort
- Easier maintenance

---

# ⭐ Key Takeaways

- Power Apps provides the user interface.
- Power Automate provides workflow automation.
- SharePoint commonly stores business data.
- Microsoft Lists integrates directly with both services.
- Power Apps can call Power Automate.
- Power Automate can receive information from Power Apps.
- SharePoint supports direct creation of Power Apps and flows.
- The connector framework enables integration with hundreds of systems.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Separate the Responsibilities

Avoid placing all business logic inside Power Apps.

A better architecture is:

```text
Power Apps
     ↓
Collect Data

Power Automate
     ↓
Business Logic

SharePoint
     ↓
Storage
```

This improves maintainability.

---

## 2. Avoid Hardcoding Values

Do not hardcode:

- Manager emails
- SharePoint URLs
- IDs
- Site names
- Departments

Use:

- Environment Variables
- SharePoint Lists
- Dataverse Tables
- Configuration Lists

---

## 3. SharePoint Is Not Always the Best Database

SharePoint works well for many business solutions but is not intended for every scenario.

Consider Dataverse or SQL when:

- Complex relationships exist.
- Large data volumes are expected.
- High transaction rates are required.
- Advanced security is needed.

---

## 4. Power Apps Should Validate Data

Validate:

- Required fields
- Dates
- Numbers
- Email addresses
- Business rules

before calling Power Automate.

This reduces failed flows.

---

## 5. Keep Flows Reusable

Instead of:

```text
Travel App Only
```

Design:

```text
Approval Flow

Notification Flow

Document Flow

Logging Flow
```

Reusable components reduce maintenance.

---

## 6. SharePoint Lists Need Governance

Without governance:

- Duplicate lists appear.
- Permissions become inconsistent.
- Naming conventions disappear.
- Reporting becomes difficult.

Treat SharePoint as a managed business platform.

---

## 7. Minimise Connector Permissions

Only grant the permissions the application genuinely requires.

Avoid unnecessary access to:

- SharePoint sites
- Mailboxes
- Dataverse tables
- SQL databases

Follow the principle of least privilege.

---

## 8. Think Mobile First

Many users will use:

- Phones
- Tablets
- Field devices

Design Power Apps with responsive layouts and touch-friendly controls.

---

## 9. Monitor Flow Ownership

Production flows should not depend on a single employee's personal account.

Prefer:

- Service Accounts
- Connection References
- Solutions

This improves continuity.

---

## 10. Integration Does Not Replace Governance

Automation should follow:

- Security policies
- Data retention
- Information classification
- Audit requirements
- Change management

Technology alone is not governance.

---

# ⚠️ Common Mistakes

- Putting business logic inside Power Apps.
- Hardcoding email addresses.
- Using SharePoint as a relational database.
- Ignoring delegation warnings.
- Using personal connections.
- Building very large flows.
- Not validating user input.
- Giving excessive permissions.
- Forgetting error handling.
- Creating duplicate SharePoint lists.
- Ignoring connector licensing.
- Not documenting integrations.
- Not testing mobile layouts.
- Mixing development and production environments.

---

# 🧪 Testing Checklist

Test:

- App launches.
- Flow starts.
- Data passes correctly.
- SharePoint updates.
- Required fields.
- Invalid input.
- Mobile layout.
- Tablet layout.
- Desktop layout.
- Offline behaviour (where applicable).
- Permissions.
- Error messages.
- Flow failures.
- Notifications.
- Performance under load.
- Different user roles.

---

# 🏆 Best Practices

- Build inside Solutions.
- Use Connection References.
- Use Environment Variables.
- Separate UI from business logic.
- Use reusable flows.
- Use reusable components.
- Validate before submitting.
- Handle errors gracefully.
- Minimise permissions.
- Document architecture.
- Monitor usage.
- Test across devices.
- Use meaningful naming conventions.
- Version your applications.
- Design for scalability.

---

# 🧱 Recommended Enterprise Architecture

```text
User
 │
 ▼
Power Apps
 │
 ▼
Validation Layer
 │
 ▼
Power Automate
 │
 ├──────────────┐
 ▼              ▼
SharePoint   Dataverse
 │              │
 └──────┬───────┘
        ▼
 Notifications
 │
 ▼
Teams
Email
Planner
Approvals
 │
 ▼
Power BI
```

This layered approach separates presentation, business logic, data storage, and reporting, making solutions easier to maintain and extend.

---

# 🛡️ Error-Handling Pattern

```text
Power Apps
     ↓
Validate Input
     ↓
Run Flow
     ↓
Try
     ↓
Business Actions
     ↓
Catch
     ↓
Notify User
     ↓
Log Error
     ↓
Finally
     ↓
Return Success/Failure
```

---

# 📊 Suggested Architecture Documentation

For every enterprise solution, document:

| Component | Description |
|------------|-------------|
| Power App | User interface |
| Trigger | How automation starts |
| Flow | Business logic |
| Data Source | SharePoint / Dataverse / SQL |
| Notifications | Email / Teams |
| Approvals | Approval process |
| Security | Roles and permissions |
| Owner | Solution owner |
| Support | Support team |
| Version | Current release |

---

# 🚀 How I Would Improve This Solution

For a production-ready implementation, I would:

1. Build the solution inside a Solution.
2. Use Connection References.
3. Store configuration in Environment Variables.
4. Use responsive Power Apps layouts.
5. Validate all inputs before submission.
6. Create reusable child flows.
7. Implement structured error handling.
8. Add audit logging.
9. Implement role-based security.
10. Use service accounts for shared automations.
11. Build dashboards in Power BI.
12. Document the complete architecture and support model.

---

# 🧠 Engineering Design Questions

Before integrating Power Apps, Power Automate, and SharePoint, ask:

- What problem is the app solving?
- Which data source is the system of record?
- Should SharePoint, Dataverse, or SQL be used?
- What business logic belongs in the app versus the flow?
- Which users need access?
- Which permissions are required?
- Will the app work on mobile devices?
- How will errors be communicated?
- Should the flow be reusable?
- How will the solution be monitored?
- Who owns the application?
- How will future changes be managed?
- Does the solution comply with organisational governance?
- Can it scale as usage grows?

---

# 💭 Reflection

This exercise demonstrated that the real strength of Microsoft Power Platform lies not in any single product but in **how the products work together**.

The integration model is simple:

```text
Power Apps
    +
Power Automate
    +
SharePoint
    =
Complete Business Solution
```

Power Apps provides an intuitive interface for users, Power Automate orchestrates business processes, and SharePoint (or another data source such as Dataverse or SQL) stores and manages the data.

The most important lesson is that well-designed solutions separate **presentation**, **business logic**, and **data storage**. This layered architecture results in applications that are easier to maintain, more secure, more scalable, and better aligned with enterprise governance and long-term support.
