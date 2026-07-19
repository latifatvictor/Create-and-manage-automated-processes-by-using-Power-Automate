# 📘 Module 16 - Build a Flow That Uses SQL

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 12 minutes

---

# 📖 Overview

In this exercise, I learned how to build an automated cloud flow that monitors one data source and synchronises new or changed records into another system.

The scenario uses:

- **Microsoft Lists / SharePoint** as the source
- **Azure SQL Database** as the destination
- **Power Automate** as the integration layer

The flow checks whether a corresponding SQL record already exists.

If the record exists, the flow updates it.

If the record does not exist, the flow inserts a new row.

This is commonly described as an **upsert pattern**:

```text
Source Record Created or Modified
              ↓
Search Destination
              ↓
Does Matching Record Exist?
          /              \
        Yes               No
         ↓                 ↓
   Update Record      Insert Record
```

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Build a flow that connects Microsoft Lists and SQL.
- Monitor a SharePoint list for new or changed records.
- Query an Azure SQL Database table.
- Use a unique identifier to match records.
- Check whether a destination record exists.
- Insert a new SQL row.
- Update an existing SQL row.
- Use expressions to access query results.
- Understand one-way synchronisation.
- Recognise the risk of infinite synchronisation loops.
- Handle required fields and SQL data types.
- Identify limitations around deleted source records.

---

# 🏗️ Solution Architecture

```text
Microsoft List Item
Created or Modified
          ↓
SharePoint Trigger
          ↓
Query SQL Table
Using Customer ID
          ↓
Count Matching Rows
          ↓
Matching Row Found?
      /              \
    Yes               No
     ↓                 ↓
Update SQL Row     Insert SQL Row
```

---

# 🔑 Core Integration Pattern

The flow follows four main stages.

## 1. Monitor the Source

Power Automate watches the source system for changes.

```text
When an item is created or modified
```

## 2. Search the Destination

The flow queries SQL using a unique business key.

```text
CustomerID = Source CustomerID
```

## 3. Determine Whether the Record Exists

The number of matching SQL rows is evaluated.

```text
length(SQL results)
```

## 4. Insert or Update

```text
Exists → Update

Does not exist → Insert
```

---

# 🔄 What Is an Upsert?

An upsert combines two operations:

```text
Update
   +
Insert
```

The flow first checks whether a matching destination record exists.

If it exists:

```text
Update existing row
```

If it does not exist:

```text
Insert new row
```

This prevents a new SQL row from being created every time a source item is modified.

---

# 📋 Source and Destination

## Source

```text
Microsoft Lists
```

The list contains the business data entered or maintained by users.

Example columns:

- CustomerID
- CustomerName
- Email
- Telephone
- Status
- Address

## Destination

```text
Azure SQL Database
```

The SQL table stores a copy of the source data for:

- Reporting
- Integration
- Analytics
- Application use
- Centralised data processing

---

# 🆔 Unique Record Identifier

A reliable synchronisation process needs a field that uniquely identifies the same record in both systems.

In the exercise:

```text
CustomerID
```

is used as the matching key.

Example:

| Source CustomerID | SQL CustomerID | Action |
|---|---|---|
| CUST-001 | CUST-001 | Update |
| CUST-002 | Not found | Insert |

Without a stable unique identifier, the flow may:

- Create duplicates
- Update the wrong record
- Fail to find an existing row
- Produce inconsistent data

---

# ⚙️ Main Flow Components

## 1️⃣ SharePoint Trigger

The source trigger is:

```text
When an item is created or modified
```

Configuration includes:

- Site Address
- List Name

The flow runs whenever a new item is added or an existing item is changed.

---

## 2️⃣ SQL Get Rows

The SQL action searches the destination table.

```text
Get rows
```

Configuration includes:

- Server name
- Database name
- Table name
- Filter Query

Example filter:

```text
CustomerID eq [Source CustomerID]
```

This checks whether SQL already contains the current source record.

---

# 🔎 SQL Filter Query

The filter uses the source identifier as dynamic content.

Conceptually:

```text
CustomerID eq 'CUST-001'
```

The exact syntax depends on the SQL connector, column type, and generated query.

The filter should return:

- Zero rows when the record does not exist
- One row when the record exists

A unique key should never normally return multiple rows.

---

# 🧮 Checking Whether a Record Exists

The SQL Get rows action returns a collection.

The condition checks the size of that collection.

```text
length(body/value)
```

Conceptually:

```text
length(SQL rows) is equal to 1
```

Result:

```text
1 → Record exists

0 → Record does not exist
```

A more defensive design may check:

```text
length(SQL rows) is greater than 0
```

This avoids treating more than one returned row as a missing record.

---

# 🌿 Condition Branches

## True Branch

A matching SQL record exists.

```text
Update Row
```

## False Branch

No matching SQL record exists.

```text
Insert Row
```

The branches must be checked carefully because an incorrect condition can reverse the intended logic.

---

# ➕ Insert SQL Row

The Insert Row action creates a new SQL record.

Configuration includes:

- Server
- Database
- Table
- Required columns
- Optional columns

Example mapping:

| SQL Column | Source Value |
|---|---|
| CustomerID | Microsoft List CustomerID |
| CustomerName | Microsoft List Title |
| EmailAddress | Microsoft List Email |
| Status | Microsoft List Status |
| LastModified | Modified timestamp |

Every SQL column marked as required must receive a value.

---

# ✏️ Update SQL Row

The Update Row action modifies an existing SQL record.

The action requires the destination row identifier.

In the exercise, the primary key is retrieved from the first SQL row returned.

Example expression:

```text
outputs('Get_Rows')?['body/value'][0]?['customerid']
```

This means:

```text
Get SQL results
      ↓
Open body/value collection
      ↓
Select first item
      ↓
Read customerid
```

---

# 🧩 Expression Breakdown

```text
outputs('Get_Rows')
```

Returns the complete output of the SQL Get Rows action.

```text
?['body/value']
```

Accesses the collection of returned rows.

```text
[0]
```

Selects the first row.

```text
?['customerid']
```

Retrieves the CustomerID property from that row.

The action name and column schema name must match the actual flow.

---

# 🔁 Why Power Automate May Add Apply to Each

Get rows returns a collection, even when only one record is expected.

Power Automate may therefore add:

```text
Apply to each
```

when dynamic content from the result is selected.

In this exercise, the unique CustomerID guarantees that only one row should be returned, so the first item can be accessed directly through an expression.

This avoids an unnecessary loop.

---

# ⚠️ One-Way Synchronisation

The flow copies changes from:

```text
Microsoft Lists
        ↓
Azure SQL Database
```

It does not copy SQL changes back into the list.

This is intentional.

```text
Source → Destination
```

not:

```text
Source ↔ Destination
```

---

# 🚨 Infinite Loop Risk

Attempting to build two independent flows that update each other can create an endless loop.

Example:

```text
List changes
    ↓
Update SQL
    ↓
SQL changes
    ↓
Update List
    ↓
List changes again
    ↓
Repeat indefinitely
```

This can cause:

- Excessive flow runs
- API throttling
- Duplicate updates
- Data conflicts
- Increased costs
- Difficult troubleshooting

True bidirectional synchronisation requires deliberate architecture, change tracking, conflict resolution, and loop prevention.

---

# 🗑️ Delete Behaviour

The SharePoint trigger only handles:

```text
Created
or
Modified
```

It does not run when a source item is deleted.

As a result, deleting an item from Microsoft Lists does not automatically delete the SQL row.

A safer design may use a soft-delete field:

```text
Active = No
```

or:

```text
Record Status = Retired
```

The flow can then update SQL without physically deleting the source item.

---

# 🧱 Data Type Considerations

Source and destination column names do not need to match.

However, their data types must be compatible.

| Source Type | SQL Type | Consideration |
|---|---|---|
| Single line text | nvarchar | Usually direct mapping |
| Number | int or decimal | Check precision |
| Yes/No | bit | Convert to true/false or 1/0 |
| Date and time | datetime2 | Check timezone |
| Choice | text or code | Map labels carefully |
| Person | nvarchar or ID | Decide what value to store |
| Lookup | ID or text | Resolve related value |
| Multiple choice | JSON or delimited text | Requires transformation |

---

# 📌 Choice Column Warning

Choice columns require careful mapping.

The source may provide:

- Display label
- Internal value
- Array
- Object

The destination may expect:

- Text
- Integer code
- Foreign key

Do not assume that a SharePoint choice value can be inserted directly into any SQL column without transformation.

---

# 🔐 Required SQL Columns

When inserting a row, every required SQL column must receive a valid value.

Possible failures include:

- Null inserted into a non-null column
- Text sent to an integer field
- Invalid date format
- Value too long for the column
- Missing foreign key
- Duplicate primary key

Review the SQL table schema before mapping fields.

---

# 🤖 Using Copilot

The exercise used a Copilot prompt similar to:

```text
When an item is created or modified in SharePoint,
get rows from SQL.

If the item exists, update it in SQL.
Otherwise, create a new SQL row.
```

Copilot can generate the initial flow structure:

- SharePoint trigger
- SQL Get rows
- Condition
- Update Row
- Insert Row

However, the generated flow still needs manual review.

Check:

- Connections
- Source list
- SQL server
- Database
- Table
- Filter query
- Condition logic
- Row ID
- Column mappings

---

# 💼 Real-World Business Scenarios

## Customer Data Integration

```text
Customer Updated in List
         ↓
Synchronise SQL Customer Table
         ↓
Reporting System Uses Updated Data
```

---

## Service Request Reporting

```text
Request Created in SharePoint
          ↓
Copy to SQL
          ↓
Power BI Reports Against SQL
```

---

## Asset Management

```text
Asset Record Updated
        ↓
Update Central SQL Asset Table
        ↓
Downstream Application Reads Data
```

---

## HR Reference Data

```text
Employee Reference List Updated
           ↓
Synchronise SQL Reporting Table
           ↓
Analytics Dataset Refreshes
```

---

## Governance Reporting

```text
Licence Review Record Updated
           ↓
Copy to SQL
           ↓
Central Governance Dashboard
```

---

# 💼 Real-Life Work Applications

## Microsoft 365 Licence Governance

A SharePoint list could contain reviewed licensing decisions.

```text
Licence Review Updated
          ↓
SQL Record Checked
          ↓
Insert or Update
          ↓
Power BI Dashboard Refreshes
```

Possible fields:

- User Principal Name
- Account status
- Licence type
- Review decision
- Business justification
- Review date
- Reviewer
- Resource-mailbox category
- Final action

---

## Joiner, Mover and Leaver Reporting

JML records maintained in SharePoint could be synchronised into SQL for consolidated reporting.

```text
JML Item Changed
       ↓
Match on Request Reference
       ↓
Insert or Update SQL
       ↓
Enterprise Reporting
```

---

## Copilot Usage Governance

A Microsoft List containing survey or licence-review outcomes could feed a SQL reporting table.

Example fields:

- User
- Licence assigned
- Activity level
- Survey response
- Business need
- Review outcome
- Last reviewed

---

## Site Visit Requests

Approved site-visit records could be copied into SQL for:

- Cross-project reporting
- Cost analysis
- Travel trends
- Business-unit reporting
- Audit history

---

## Service Desk Analytics

A SharePoint-based operational tracker could synchronise to SQL for:

- Power BI dashboards
- Trend analysis
- SLA reporting
- Ticket-volume reporting
- Root-cause analysis

---

# ⭐ Key Takeaways

- Power Automate can synchronise data between Microsoft Lists and SQL.
- A unique identifier is required for reliable matching.
- Get rows checks whether the destination record exists.
- A condition decides whether to insert or update.
- Get rows returns a collection.
- The first returned item can be accessed through an expression.
- All required SQL columns must be populated.
- Data types must be compatible.
- The design is one-way only.
- Deletions need a separate strategy.
- Bidirectional flows can create infinite loops.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Use a True Unique Identifier

Do not use a field such as a customer name unless it is guaranteed to be unique and stable.

Better examples:

- Customer ID
- Request reference
- Employee ID
- Asset ID
- GUID
- SQL primary key

Names can change and can be duplicated.

---

## 2. Enforce Uniqueness in SQL

The destination should ideally enforce uniqueness through:

- Primary key
- Unique constraint
- Unique index

Power Automate checks alone do not guarantee data integrity under concurrent processing.

---

## 3. Use Greater Than Zero Where Appropriate

The exercise checks whether the result length equals one.

A more resilient check may be:

```text
length(SQL rows) > 0
```

If duplicate rows accidentally exist, `equals 1` could route the flow to Insert and create further duplication.

Duplicates should still be investigated and corrected.

---

## 4. Do Not Build Two-Way Sync Casually

Bidirectional synchronisation needs:

- Source-of-truth rules
- Conflict resolution
- Last-modified comparison
- Change origin tracking
- Loop prevention
- Error recovery
- Transaction design

Two simple opposing flows are not a safe synchronisation strategy.

---

## 5. Filter Queries Must Match the Data Type

Text values may require quotation handling.

Numeric values should not be treated as text.

Dates require valid formatting.

Malformed filter queries can return no records or fail completely.

---

## 6. Protect SQL Credentials and Connections

The SQL connection may have significant access.

Use:

- Least-privilege database accounts
- Entra authentication where supported
- Approved connection references
- Secure gateway configuration where required
- Separate development and production connections

Do not use an unrestricted database administrator account for routine automation.

---

## 7. SQL Connector Licensing Must Be Confirmed

SQL is commonly treated as a Premium connector in Power Automate.

Before deployment, confirm:

- User licensing
- Process licensing
- Service-account licensing
- Environment policy
- Capacity
- Gateway requirements

---

## 8. Use an On-Premises Gateway Where Required

Azure SQL can often be reached directly.

An on-premises SQL Server usually requires an on-premises data gateway.

The gateway introduces dependencies such as:

- Host availability
- Network access
- Gateway service health
- Credentials
- Cluster configuration
- Ownership
- Patch management

---

## 9. Avoid Selecting Every SQL Row

Get rows should use a restrictive filter.

Retrieving the entire table for every SharePoint change is inefficient and can cause:

- Slow flows
- Large API consumption
- Memory pressure
- Timeouts
- Throttling

Query only the matching record.

---

## 10. Handle Concurrent Updates

Two rapid source changes may run simultaneously.

Possible outcomes include:

- Both runs see no SQL record.
- Both attempt an insert.
- One insert fails because of a duplicate key.
- Updates are applied out of order.

Use unique constraints and consider concurrency controls.

---

## 11. Deletion Must Be Designed Explicitly

Possible strategies include:

- Soft delete
- Separate deletion flow
- Scheduled reconciliation
- Retention status
- Archive table
- Event log

Do not assume removed SharePoint items disappear automatically from SQL.

---

## 12. SQL Is Not Automatically the Source of Truth

The business must define which system is authoritative.

In this exercise:

```text
Microsoft Lists = Source of Truth

SQL = Destination Copy
```

Changing SQL directly may be overwritten by the next source update.

---

# ⚠️ Common Mistakes

- Matching on a non-unique field.
- Checking the wrong SQL column.
- Selecting the wrong dynamic content.
- Reversing the true and false branches.
- Using `equals 1` without considering duplicates.
- Mapping incompatible data types.
- Missing required SQL fields.
- Using the source ID instead of SQL Row ID.
- Hardcoding server and database values.
- Using unrestricted SQL credentials.
- Retrieving the entire SQL table.
- Forgetting SQL connector licensing.
- Ignoring gateway requirements.
- Attempting simple two-way synchronisation.
- Forgetting deletion handling.
- Not adding duplicate prevention.
- Not testing concurrent changes.

---

# 🧪 Testing Checklist

Test the flow for:

- New source item
- Modified source item
- Existing SQL row
- Missing SQL row
- Duplicate SQL rows
- Invalid CustomerID
- Missing required field
- Text too long for SQL column
- Invalid date
- Choice value mapping
- SQL connection failure
- SharePoint connection failure
- SQL permission failure
- Gateway unavailable
- Two rapid updates
- Two simultaneous inserts
- Deleted source item
- SQL row manually changed
- High-volume changes
- Copilot-generated logic errors

---

# 🏆 Best Practices

- Define a clear source of truth.
- Use a stable unique identifier.
- Enforce uniqueness in SQL.
- Filter SQL queries at the source.
- Map data types explicitly.
- Use connection references.
- Store flows inside Solutions.
- Use environment variables.
- Apply least-privilege SQL access.
- Add error-handling Scopes.
- Log integration status.
- Store last-synchronised timestamps.
- Prevent duplicate inserts.
- Design deletion handling.
- Test concurrency.
- Monitor failures and performance.
- Document source-to-destination mappings.

---

# 🧱 Recommended Production Design

The training design is:

```text
SharePoint Trigger
        ↓
Get SQL Rows
        ↓
Condition
     /       \
Update      Insert
```

A stronger enterprise design could be:

```text
Source Item Created or Modified
            ↓
Validate Required Fields
            ↓
Generate Correlation ID
            ↓
Query SQL by Unique Key
            ↓
Matching Rows?
      /         |          \
     0          1          More Than 1
     ↓          ↓               ↓
Insert       Update         Log Data Error
     ↓          ↓               ↓
Store Sync Result        Notify Support
      \         /
       \       /
     Update Source Sync Status
              ↓
         Write Audit Log
```

---

# 🛡️ Error-Handling Pattern

```text
Scope - Try
    ↓
Validate Source
    ↓
Query SQL
    ↓
Insert or Update
```

```text
Scope - Catch
    ↓
Capture Error
    ↓
Update Source Status to Failed
    ↓
Notify Support
```

```text
Scope - Finally
    ↓
Write Integration Audit Entry
```

---

# 📊 Suggested Source Tracking Fields

The SharePoint list could contain:

| Field | Purpose |
|---|---|
| Sync Status | Pending, successful, failed |
| Last Synced | Records completion time |
| SQL Record ID | Links to destination |
| Retry Count | Tracks repeated attempts |
| Last Error | Stores failure details |
| Correlation ID | Connects source and destination |
| Source Modified | Stores source update time |
| Destination Updated | Stores SQL update time |
| Deleted or Inactive | Supports soft deletion |

---

# 🗄️ Suggested SQL Audit Fields

The SQL table could include:

| Field | Purpose |
|---|---|
| SourceSystem | Identifies Microsoft Lists |
| SourceRecordID | Stores SharePoint item ID |
| CorrelationID | Supports tracing |
| CreatedFromSource | First synchronisation time |
| LastSyncedFromSource | Most recent sync |
| IsActive | Supports soft deletion |
| SourceModifiedDate | Enables version comparison |
| IntegrationStatus | Records processing state |
| LastFlowRunID | Supports troubleshooting |

---

# 🔁 Concurrency and Duplicate Prevention

A safer insert process should rely on SQL uniqueness.

Example:

```text
Unique Index on CustomerID
```

Then:

```text
Flow A checks SQL → Not found
Flow B checks SQL → Not found
Flow A inserts successfully
Flow B insert fails with duplicate key
```

The failure can then be handled by retrying the operation as an update.

This is safer than assuming two flows will never run at the same time.

---

# 🧠 Better Existence Check

Conceptual expression:

```text
length(outputs('Get_Rows')?['body/value'])
```

Recommended condition:

```text
is greater than 0
```

Branching:

```text
0 rows → Insert

1 row → Update

More than 1 row → Data-quality exception
```

A separate branch or validation action can detect duplicates.

---

# 🚀 How I Would Improve This Solution

For production use, I would:

1. Define Microsoft Lists as the documented source of truth.
2. Use a stable CustomerID with a SQL unique constraint.
3. Use a restrictive SQL filter query.
4. Check for zero, one, or multiple rows.
5. Add validation before SQL actions.
6. Store the SQL record ID in the source.
7. Add integration-status columns.
8. Add Try, Catch, and Finally Scopes.
9. Notify support when duplicate records are found.
10. Handle source deletion through soft-delete logic.
11. Use environment variables for server, database, and table configuration.
12. Use a least-privilege SQL connection.
13. Confirm Premium connector licensing.
14. Test simultaneous updates.
15. Add a reconciliation process to compare source and destination periodically.

---

# 🧠 Engineering Design Questions

Before creating a source-to-SQL integration, ask:

- Which system is the source of truth?
- Which events should trigger synchronisation?
- What uniquely identifies a record?
- Is uniqueness enforced in both systems?
- What happens when no destination row exists?
- What happens when one row exists?
- What happens when multiple rows exist?
- Which columns are required?
- Are data types compatible?
- Are choice values mapped correctly?
- How are lookups represented?
- What happens when a source item is deleted?
- Could two runs process the same record concurrently?
- Is SQL Premium licensing available?
- Is a data gateway required?
- Which database permissions are necessary?
- How will credentials be managed?
- How will errors be logged?
- How will failed records be retried?
- How will data consistency be checked over time?
- Who owns and supports the integration?

---

# 💭 Reflection

This exercise demonstrated how Power Automate can connect a user-friendly Microsoft Lists interface with a structured Azure SQL Database.

The core integration pattern is:

```text
Detect Change
      ↓
Find Matching Record
      ↓
Insert or Update
      ↓
Confirm Synchronisation
```

The technical steps are relatively straightforward, but a production-grade integration requires much more than copying fields.

A reliable design must account for:

```text
Unique Keys
    +
Data Types
    +
Source of Truth
    +
Duplicate Prevention
    +
Concurrency
    +
Security
    +
Licensing
    +
Deletion Handling
    +
Error Recovery
```

The most important lesson is that synchronisation is a data-governance problem as much as it is an automation problem.

Power Automate can move the data, but the solution designer must define how records are identified, how conflicts are handled, which system is authoritative, and how failures are detected and corrected.
