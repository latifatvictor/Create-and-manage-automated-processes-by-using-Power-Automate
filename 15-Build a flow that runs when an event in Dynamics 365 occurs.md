# 📘 Module 15 - Build a Flow That Runs When an Event Occurs in Dynamics 365

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 14 minutes

---

# 📖 Overview

In this exercise, I learned how to create automated cloud flows that respond to events in Microsoft Dataverse.

These flows use a Dataverse trigger to detect when a row is added, modified, or deleted, and then perform actions in Dataverse or another Microsoft 365 service.

The module covered two examples:

1. Create a Dataverse task when a new Account record is created.
2. Create a Microsoft Planner task when a Dataverse task is created.

This demonstrates a common integration pattern:

```text
Business Event in Dataverse
            ↓
Automated Cloud Flow Trigger
            ↓
Read Record Data
            ↓
Create or Update Related Record
            ↓
Continue Business Process
```

Power Automate can use Dataverse events to connect business applications, synchronise records, create work items, and notify users automatically. :contentReference[oaicite:0]{index=0}

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Create an automated cloud flow using a Dataverse trigger.
- Use the **When a row is added, modified, or deleted** trigger.
- Configure the Dataverse change type.
- Select the appropriate Dataverse table.
- Understand trigger scope.
- Create a related Dataverse row.
- Create a Planner task from Dataverse data.
- Use dynamic content between systems.
- Understand Dataverse change tracking.
- Recognise trigger timing limitations.
- Use advanced filtering and sorting options.
- Match dynamic content to Dataverse column types.

---

# 🔑 Core Automation Pattern

Dataverse-driven flows follow an event-based pattern.

```text
Dataverse Row Changes
          ↓
Trigger Evaluates Event
          ↓
Flow Retrieves Row Data
          ↓
Actions Use Dynamic Content
          ↓
Related Business Action Completes
```

Unlike an instant flow, no user needs to manually select **Run**.

The automation starts automatically when the configured Dataverse event occurs.

---

# 🏗️ Solutions Built

## Example 1

```text
New Account Created in Dataverse
              ↓
Dataverse Trigger Runs
              ↓
Create New Task Row
              ↓
Task Subject Uses Account Name
```

## Example 2

```text
New Task Created in Dataverse
              ↓
Dataverse Trigger Runs
              ↓
Create Planner Task
              ↓
Planner Title Uses Dataverse Subject
```

---

# ⚙️ Dataverse Trigger

The trigger used in both flows is:

```text
Microsoft Dataverse
When a row is added, modified, or deleted
```

The main settings are:

| Setting | Purpose |
|---|---|
| Change type | Determines which record event starts the flow |
| Table name | Defines which Dataverse table is monitored |
| Scope | Defines which users or business units can trigger the flow |
| Filter rows | Optionally limits the records that qualify |
| Select columns | Optionally limits which changed fields matter |

---

# 🔄 Change Types

The Dataverse trigger can respond to:

```text
Added
Modified
Deleted
```

## Added

Runs when a new row is created.

Example:

```text
New employee request created
```

## Modified

Runs when an existing row changes.

Example:

```text
Request status changes to Approved
```

## Deleted

Runs when a row is removed.

Example:

```text
Temporary access record deleted
```

The selected change type should match the actual business event.

---

# 🌐 Trigger Scope

The scope controls which record changes can start the flow.

In the exercise, the scope was:

```text
Organization
```

This means the flow can run when an eligible record is created by any user in the environment.

The scope is important because it determines whether a flow responds to events created:

- By the flow owner
- Inside a business unit
- Inside a parent-child business-unit structure
- Anywhere in the organisation

The Dataverse trigger requires a scope to be selected. :contentReference[oaicite:1]{index=1}

---

# 🧭 Common Scope Options

Depending on the connector and environment, scope may include:

- User
- Business Unit
- Parent: Child Business Units
- Organization

## User

Runs only for records owned or changed within the user's scope.

## Business Unit

Runs for records associated with the user's business unit.

## Parent: Child Business Units

Includes the parent business unit and its child units.

## Organization

Runs across the whole environment.

The broadest scope is not always the best choice.

Use the smallest scope that meets the business requirement.

---

# 🛠️ Example 1 - Create a Task from a New Account

## Business Requirement

Whenever a new Account is created in Dataverse, create a related task automatically.

---

## Flow Architecture

```text
Account Row Added
       ↓
Dataverse Trigger
       ↓
Create New Task Row
       ↓
Task Subject = Account Name
```

---

## Trigger Configuration

```text
Change Type: Added
Table Name: Accounts
Scope: Organization
```

---

## Action Configuration

Action:

```text
Microsoft Dataverse
Add a new row
```

Target table:

```text
Tasks
```

Field mapping:

```text
Subject = Account Name
```

The Account Name is retrieved as dynamic content from the trigger.

---

## Result

Each time an Account is created, Power Automate creates a corresponding Task row.

Example:

```text
Account:
Contoso Ltd
```

Resulting task:

```text
Subject:
Contoso Ltd
```

The exercise confirms that the new task uses the new account's name as its subject. :contentReference[oaicite:2]{index=2}

---

# 🛠️ Example 2 - Create a Planner Task from a Dataverse Task

## Business Requirement

Whenever a new task is created in Dataverse, create a corresponding Microsoft Planner task.

---

## Flow Architecture

```text
Dataverse Task Created
          ↓
Dataverse Trigger
          ↓
Create Planner Task
          ↓
Map Dataverse Subject to Planner Title
```

---

## Trigger Configuration

```text
Change Type: Added
Table Name: Tasks
Scope: Organization
```

---

## Planner Action

Action:

```text
Microsoft Planner
Create a task
```

Typical configuration:

| Field | Value |
|---|---|
| Group ID | Microsoft 365 group that owns the plan |
| Plan ID | Target Planner plan |
| Title | Static text plus Dataverse Subject |
| Bucket ID | Optional target bucket |
| Due Date Time | Optional Dataverse due date |

Example title:

```text
Begin onboarding process for: [Subject]
```

---

## Result

When a Dataverse task is created, a corresponding Planner task is added to the selected plan.

This connects structured Dataverse data with a collaborative task-management experience.

---

# ⚡ Dynamic Content

Dynamic content passes values from the Dataverse trigger into later actions.

Examples include:

- Account name
- Task subject
- Due date
- Record owner
- Description
- Priority
- Record ID
- Status

Example:

```text
Dataverse Task Subject
          ↓
Planner Task Title
```

The value should be mapped only where the destination field supports the same type of data.

---

# 🔍 Dataverse Change Tracking

The relevant Dataverse table must have change tracking enabled for trigger-based flows to work correctly.

Change tracking allows Dataverse to identify changes that need to be surfaced to synchronisation and automation services. :contentReference[oaicite:3]{index=3}

Before troubleshooting a Dataverse trigger, verify:

- The table supports change tracking.
- Change tracking is enabled.
- The connection has access to the table.
- The flow is running in the correct environment.
- The correct change type is selected.

---

# 🤖 Using Copilot During Flow Creation

The exercise used Copilot to add actions based on a natural-language prompt.

Example prompt:

```text
When a new row is added to a Dataverse table,
add a new row to another Dataverse table.
```

Copilot can accelerate initial design, but generated actions must still be checked.

Copilot may:

- Remove an existing trigger setting.
- Leave required fields incomplete.
- Use the wrong table.
- Produce invalid parameter warnings.
- Select the wrong connection.
- Add actions that do not fully meet the requirement.

Always recheck the flow after Copilot modifies it.

---

# 🚨 Trigger Timing Behaviour

Dataverse triggers do not always run at the exact instant the row changes.

Normally, they start within a few minutes.

In rare situations, a trigger can take significantly longer.

The flow also runs using the latest data available when the action executes.

Example:

```text
Record Created
    ↓
Record Updated Twice
    ↓
Flow Executes
    ↓
Flow Reads Latest Version
```

The flow may run once using the most recent row data rather than separately processing every intermediate state. :contentReference[oaicite:4]{index=4}

This is important for processes that depend on exact event sequencing.

---

# 📋 Advanced Parameters

Advanced parameters can improve performance and reduce unnecessary flow runs.

Common options include:

- Filter rows
- Select columns
- Sort by
- Row count
- Expand query
- Trigger conditions

---

# 🔎 Filter Rows

A filter query restricts which records are returned or processed.

Example:

```text
statuscode eq 1
```

This could restrict processing to active records.

Other examples:

```text
prioritycode eq 1
```

```text
statecode eq 0
```

```text
estimatedvalue gt 10000
```

Filtering at the connector level is usually more efficient than retrieving every row and filtering later.

---

# ↕️ Sort By

Sort By controls the order of returned records.

Example:

```text
emailaddress1 asc
```

This sorts records by email address in ascending order.

---

# 🧩 OData Queries

Dataverse advanced filtering commonly uses OData syntax.

Examples:

```text
statecode eq 0
```

```text
createdon ge 2026-01-01
```

```text
contains(name,'Agri')
```

Queries must use Dataverse schema names rather than only display names.

---

# 🔢 Dataverse Data Types

Destination fields must receive compatible data.

| Dataverse Column Type | Expected Value |
|---|---|
| Text | String or text dynamic content |
| Whole Number | Integer |
| Decimal | Decimal number |
| Date and Time | Valid date-time value |
| Yes/No | Boolean |
| Choice | Valid option value |
| Lookup | Related record reference |
| Currency | Numeric value with currency context |

The exercise emphasises that the value supplied to a Dataverse column must match its underlying type. :contentReference[oaicite:5]{index=5}

---

# 🔗 Lookup Columns

Lookup fields reference another Dataverse row.

They usually require:

- The target record ID
- The correct related table type

A lookup cannot normally be populated reliably using only a display name.

Example:

```text
Account Lookup
      ↓
Requires Account GUID
```

Use the unique record identifier wherever possible.

---

# 💼 Real-World Business Scenarios

## Customer Onboarding

```text
New Customer Added
       ↓
Create Onboarding Task
       ↓
Assign Account Owner
       ↓
Create Planner Work Item
       ↓
Notify Delivery Team
```

---

## Service Case Management

```text
New Case Created
       ↓
Create Investigation Task
       ↓
Notify Support Team
       ↓
Add Planner Task
```

---

## Sales Follow-Up

```text
New Lead Created
       ↓
Create Follow-Up Activity
       ↓
Assign Sales Representative
       ↓
Set Due Date
```

---

## Project Delivery

```text
New Project Record Created
          ↓
Create Planner Task
          ↓
Create SharePoint Folder
          ↓
Notify Project Team
```

---

## Document Governance

```text
Document Review Record Created
            ↓
Create Review Task
            ↓
Assign Reviewer
            ↓
Track Completion
```

---

# 💼 Real-Life Work Applications

## Joiner, Mover and Leaver Automation

A Dataverse table could store JML requests.

```text
New JML Request Added
        ↓
Create Service Delivery Task
        ↓
Create Planner Checklist
        ↓
Notify Assigned Analyst
        ↓
Track Completion
```

Possible mappings:

| Dataverse Field | Planner Field |
|---|---|
| Request Reference | Task Title |
| Start or Leave Date | Due Date |
| Assigned Analyst | Assignment |
| Request Type | Bucket |
| Notes | Task Description |

---

## Licence Governance

A new licence-review record could trigger:

```text
Licence Exception Added
          ↓
Create Review Task
          ↓
Assign Licence Administrator
          ↓
Set Review Date
          ↓
Notify Process Owner
```

A modified record could also trigger when:

```text
Status = Approved
```

or:

```text
Review Date Reached
```

---

## Site Visit Requests

When a site-visit request reaches an approved status:

```text
Dataverse Status Updated
          ↓
Create Planner Preparation Task
          ↓
Assign Travel Coordinator
          ↓
Create Calendar Reminder
          ↓
Notify Requestor
```

---

## Copilot and AI Adoption

A Dataverse table could capture Copilot support or training requests.

```text
New Request Created
       ↓
Create Planner Task
       ↓
Assign Adoption Owner
       ↓
Notify Requestor
```

---

## Asset Management

When a new asset record is created:

```text
Asset Added
    ↓
Create Validation Task
    ↓
Assign Asset Team
    ↓
Notify Site Contact
```

---

# ⭐ Key Takeaways

- Dataverse events can start automated cloud flows.
- The trigger can respond to added, modified, or deleted rows.
- Scope determines which events the flow can respond to.
- Dynamic content can be passed into Dataverse, Planner, and other services.
- Change tracking must be enabled.
- Trigger execution may not be immediate.
- Copilot-generated actions must be reviewed.
- Advanced filters reduce unnecessary processing.
- Dataverse field types must be respected.
- Lookup fields require proper record references.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Confirm the Correct Environment

Power Platform environments can contain different:

- Dataverse databases
- Tables
- Connections
- Solutions
- Security roles
- Planner references

A flow created in the wrong environment may use the wrong data or fail completely.

---

## 2. Change Tracking Must Be Enabled

A Dataverse-triggered flow may not behave correctly if change tracking is disabled on the relevant table.

Always verify table configuration during troubleshooting.

---

## 3. Use the Smallest Appropriate Scope

Using Organization scope means every qualifying event across the environment can trigger the flow.

This may cause:

- Excessive runs
- Duplicate tasks
- Unnecessary API usage
- Processing of unrelated business-unit data

Choose scope deliberately.

---

## 4. Avoid Unfiltered Modified Triggers

A trigger configured for every modification can run whenever any field changes.

This can cause:

- Repeated task creation
- Flow loops
- Excessive API requests
- Duplicate notifications

Use:

- Filter rows
- Select columns
- Trigger conditions
- Status checks

---

## 5. Prevent Automation Loops

A flow may update the same table that triggered it.

Example:

```text
Task Modified
      ↓
Flow Updates Task
      ↓
Trigger Runs Again
```

Prevent this by checking:

- Which columns changed
- Current status
- Processing flag
- Source of update
- Whether the action is already complete

---

## 6. Do Not Assume Immediate Execution

A Dataverse trigger can be delayed.

Do not use it where second-by-second execution is a strict requirement without assessing platform behaviour and business tolerance.

---

## 7. The Flow May Use the Latest Record State

If a row changes several times before the flow processes it, the flow may receive the latest data.

This matters where intermediate changes must be recorded separately.

For strict event history, consider:

- Audit history
- Dedicated event records
- Plug-ins
- Azure Service Bus
- Event-driven integration architecture

---

## 8. Validate Data Types

Do not send:

- Text into a Whole Number field
- An invalid date into a Date field
- A display name into a Lookup
- A label instead of a Choice value
- A decimal into a restricted integer field

Type mismatches commonly cause Bad Request failures.

---

## 9. Planner Connections Have Their Own Dependencies

Planner task creation depends on:

- Microsoft 365 group membership
- Plan availability
- Bucket availability
- Valid Planner connection
- User permissions

If a plan or bucket is renamed or deleted, the flow may fail.

---

## 10. Copilot Can Change Existing Configuration

After using Copilot, recheck:

- Table name
- Change type
- Scope
- Connection
- Dynamic content
- Action placement
- Required parameters

Copilot supports development but does not replace validation.

---

# ⚠️ Common Mistakes

- Building the flow in the wrong environment.
- Selecting the wrong Dataverse table.
- Leaving scope unconfigured.
- Choosing Modified when Added was intended.
- Using Organization scope without assessing volume.
- Forgetting change tracking.
- Creating duplicate Planner tasks.
- Not filtering modified events.
- Mapping incompatible data types.
- Using display values instead of record IDs.
- Ignoring invalid connection warnings.
- Assuming Copilot preserved trigger settings.
- Selecting the wrong Planner group or plan.
- Hardcoding environment-specific identifiers.
- Not testing trigger delays.
- Failing to consider loops.

---

# 🧪 Testing Checklist

Test the flow for:

- New Dataverse row
- Modified Dataverse row
- Deleted Dataverse row, where applicable
- Correct scope
- User inside the business unit
- User outside the business unit
- Valid dynamic content
- Missing required field
- Invalid data type
- Missing lookup record
- Disabled change tracking
- Broken Dataverse connection
- Broken Planner connection
- Deleted Planner plan
- Deleted Planner bucket
- Duplicate record creation
- Multiple rapid updates
- Trigger delay
- Flow loop
- Copilot-generated parameter changes

---

# 🏆 Best Practices

- Build enterprise flows inside Solutions.
- Use environment variables for configurable values.
- Select the smallest appropriate scope.
- Use Filter rows where possible.
- Use Select columns for modified triggers.
- Prevent recursive updates.
- Rename every action clearly.
- Use unique record IDs for lookups.
- Validate data types.
- Log external-system identifiers.
- Add error-handling Scopes.
- Monitor failed runs.
- Document Dataverse and Planner dependencies.
- Test in a non-production environment.
- Use connection references.
- Review Copilot-generated changes carefully.

---

# 🧱 Recommended Production Design

The training flow uses:

```text
Dataverse Trigger
        ↓
Create Related Record
```

A stronger production design might be:

```text
Dataverse Row Added
        ↓
Validate Required Data
        ↓
Check Processing Status
        ↓
Check for Existing Related Task
        ↓
Create Planner or Dataverse Task
        ↓
Store External Task ID
        ↓
Update Source Record
        ↓
Notify Assigned Owner
        ↓
Log Success
```

Failure path:

```text
Action Fails
    ↓
Capture Error
    ↓
Update Source Status to Failed
    ↓
Notify Support Team
    ↓
Record Diagnostic Information
```

---

# 🔁 Duplicate Prevention

Before creating a Planner task, the flow could check whether one already exists.

Possible methods:

- Store the Planner Task ID in Dataverse.
- Create a unique integration key.
- Query Planner or an audit table.
- Add a Processed Yes/No column.
- Add a Processing Status choice.

Example:

```text
Planner Task ID is empty?
       /            \
     Yes             No
      ↓               ↓
Create Task        Do Nothing
```

---

# 🛡️ Error-Handling Pattern

```text
Scope - Try
    ↓
Validate Dataverse Data
    ↓
Create Related Task
    ↓
Update Source Record
```

```text
Scope - Catch
    ↓
Capture Action Error
    ↓
Update Integration Status
    ↓
Notify Support
```

```text
Scope - Finally
    ↓
Write Audit Entry
```

---

# 📊 Suggested Integration Fields

A Dataverse table could contain:

| Field | Purpose |
|---|---|
| Integration Status | Pending, completed, failed |
| Planner Task ID | Stores the created task identifier |
| Planner Plan ID | Records the target plan |
| Processing Date | Records execution time |
| Processed By Flow | Indicates automated processing |
| Retry Count | Tracks recovery attempts |
| Error Message | Stores failure details |
| Last Attempt | Records most recent attempt |
| Flow Run ID | Supports troubleshooting |
| Source Record ID | Links the integration record |
| Correlation ID | Connects records across systems |

---

# 🚀 How I Would Improve the Exercise Solutions

For enterprise use, I would:

1. Place both flows inside a Solution.
2. Use connection references.
3. Use environment variables for plan and group identifiers.
4. Add filters to limit eligible Dataverse records.
5. Add duplicate prevention.
6. Store the created Planner Task ID.
7. Add error-handling Scopes.
8. Notify a support mailbox on failure.
9. Add meaningful Planner task descriptions.
10. Map due dates and priority values.
11. Validate that the Dataverse fields are populated.
12. Test rapid record updates.
13. Document scope and security assumptions.
14. Monitor trigger and API consumption.

---

# 🧠 Engineering Design Questions

Before building a Dataverse event-driven flow, ask:

- Which business event should trigger the process?
- Should the flow respond to Added, Modified, or Deleted?
- Which Dataverse table should be monitored?
- Is change tracking enabled?
- What scope is appropriate?
- Which columns matter?
- Can the event occur more than once?
- How will duplicate actions be prevented?
- Could the flow update its own trigger record?
- What is the expected event volume?
- Is trigger latency acceptable?
- Which destination system is involved?
- Are destination identifiers environment-specific?
- Which connection owns the action?
- What happens if the destination is unavailable?
- How will failures be retried?
- What data must be logged?
- Who supports the integration?

---

# 💭 Reflection

This exercise demonstrated how Dataverse can act as the event source for business automation across Microsoft Power Platform and Microsoft 365.

The core pattern is:

```text
Business Record Changes
          ↓
Dataverse Detects Event
          ↓
Power Automate Responds
          ↓
Related Work Is Created
          ↓
Business Process Continues
```

The most important lesson is that event-driven automation requires more than selecting a trigger.

A reliable design must also consider:

```text
Change Tracking
      +
Scope
      +
Filtering
      +
Data Types
      +
Duplicate Prevention
      +
Error Handling
      +
Cross-System Governance
```

Dataverse triggers are powerful because they allow business data to initiate action automatically. However, production-ready integrations must be designed carefully to avoid loops, duplicated work, broad triggering, invalid mappings, and hidden operational dependencies.
