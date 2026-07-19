# 📘 Module 9 - Build an Approval Request

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 8 minutes

---

# 📖 Overview

In this module, I built a complete approval workflow using Microsoft Power Automate, SharePoint, and the Approvals connector.

The solution automatically starts when a document is uploaded to a SharePoint document library. It sends the document to an approver, waits for the decision, and then uses a condition to determine what should happen next.

If the document is approved, it remains in the original library.

If the document is rejected, it is moved automatically to a dedicated **Rejected Documents** folder.

This exercise demonstrates one of the most reusable approval patterns in Power Automate:

```text
Trigger
    ↓
Start and Wait for Approval
    ↓
Check Approval Outcome
    ↓
Approved or Rejected Action
```

---

# 🎯 Learning Objectives

After completing this module, I can:

- Create a SharePoint document approval process.
- Use the **When a file is created (properties only)** trigger.
- Configure the **Start and wait for an approval** action.
- Use dynamic content from SharePoint.
- Evaluate an approval outcome using a Condition.
- Move rejected documents automatically.
- Test both approval and rejection paths.
- Use Copilot to generate and refine an initial flow structure.

---

# 🏗️ Solution Architecture

```text
Document Uploaded to SharePoint
              ↓
When a File Is Created
              ↓
Start and Wait for Approval
              ↓
Approver Reviews Document
              ↓
        Check Outcome
         /         \
        /           \
   Approve          Reject
      ↓                ↓
Document Remains   Move Document to
in Main Library    Rejected Documents
```

---

# 📋 SharePoint Structure

The solution uses the following SharePoint structure:

```text
Approvals Library
│
├── Approved or Pending Documents
│
└── Rejected Documents
```

The **Rejected Documents** folder is used to separate files that have not passed the approval process.

This structure improves visibility, document governance, and auditability.

---

# 🔑 Core Approval Pattern

An approval workflow usually follows three key stages.

## 1. Trigger

The trigger starts the flow.

In this exercise:

```text
When a file is created (properties only)
```

The flow runs whenever a document is added to the selected SharePoint document library.

---

## 2. Start and Wait for Approval

The approval action sends the request to the approver and pauses the flow until a response is received.

The approval request can appear through:

- Email
- Power Automate Approvals centre
- Microsoft Teams Approvals app, where enabled

The flow does not continue until the approval has been completed.

---

## 3. Condition

The Condition action checks the returned approval outcome.

```text
Outcome is equal to Approve
```

The result is split into two branches:

```text
True  → Approved
False → Rejected
```

---

# ⚙️ Main Flow Components

## SharePoint Trigger

```text
When a file is created (properties only)
```

Configuration includes:

- Site Address
- Library Name

The trigger returns useful values such as:

- File name
- Identifier
- Link to item
- Created by
- Created date
- File path

---

## Approval Action

```text
Start and wait for an approval
```

Configuration used in the exercise:

| Property | Value |
|---|---|
| Approval Type | Approve/Reject - First to respond |
| Title | Document Approval |
| Assigned To | Test approver |
| Item Link | Link to item |

The **Link to item** allows the approver to open the SharePoint document directly from the approval request.

---

## Condition

The condition evaluates:

```text
Approval Outcome = Approve
```

### True Branch

The document remains in the original SharePoint library.

No additional movement is required.

### False Branch

The SharePoint **Move file** action moves the document into:

```text
Approvals Library/Rejected Documents
```

---

# 🔁 Approval Type Used

The exercise uses:

```text
Approve/Reject - First to respond
```

This means the first approver to respond determines the overall outcome.

This is suitable when:

- Only one decision is needed.
- Multiple people are allowed to respond.
- The process should continue as soon as one authorised person responds.

It may not be suitable where every approver must formally agree.

---

# ⚡ Dynamic Content Used

The flow uses dynamic content from earlier actions.

## Link to Item

Used in the approval request so the approver can open the document.

```text
Link to item
```

## Identifier

Used by the SharePoint Move file action to identify the exact document that must be moved.

```text
Identifier
```

Dynamic content ensures that the flow works with whichever file triggered the automation.

---

# 📂 Handling Duplicate File Names

The **Move file** action is configured with:

```text
If another file is already there:
Move with a new name
```

This prevents the flow from failing when a document with the same name already exists in the destination folder.

It also prevents an existing rejected document from being overwritten.

---

# 🧪 Testing the Flow

The solution should be tested by uploading a document into the SharePoint library.

## Rejection Test

```text
Upload Document
      ↓
Receive Approval
      ↓
Select Reject
      ↓
Refresh SharePoint
      ↓
Document Appears in Rejected Documents
```

## Approval Test

```text
Upload Document
      ↓
Receive Approval
      ↓
Select Approve
      ↓
Document Remains in Main Library
```

Both branches must be tested before the flow is considered complete.

---

# 💼 Real-World Business Scenarios

## Policy Document Review

A new policy document is uploaded.

```text
Upload
  ↓
Compliance Approval
  ↓
Approved → Remains available
Rejected → Moved for revision
```

---

## Marketing Content Approval

Marketing uploads campaign material.

```text
Upload
  ↓
Brand Manager Review
  ↓
Approved → Ready for publication
Rejected → Returned for amendment
```

---

## Finance Document Approval

Finance uploads a payment or invoice document.

```text
Upload
  ↓
Finance Manager Approval
  ↓
Approved → Continue processing
Rejected → Move to exception folder
```

---

## HR Document Review

HR uploads an employment-related document.

```text
Upload
  ↓
HR Manager Review
  ↓
Approved → Retain in approved location
Rejected → Move to correction folder
```

---

## Project Governance

A project team uploads a design, risk assessment, or project plan.

```text
Upload
  ↓
Project Sponsor Approval
  ↓
Approved → Retain as accepted version
Rejected → Move for rework
```

---

# 💼 Real-Life Work Situations

This pattern can be adapted to several workplace scenarios.

## Travel Request Supporting Documents

A requestor uploads supporting travel documentation.

The flow can:

- Notify the relevant manager.
- Include a direct link to the document.
- Capture approval comments.
- Update a SharePoint request record.
- Notify the requestor.
- Move rejected documents into a review folder.

---

## Project Site Visit Requests

Supporting project documents could be reviewed before a site visit request moves to the next approval stage.

The flow could:

- Start with a SharePoint document upload.
- Request line manager review.
- Route approved documents to a GTS Head.
- Record both decisions.
- Send a final notification.
- retain a full audit trail.

---

## Joiner, Mover and Leaver Processes

Sensitive access or licence requests may require formal approval.

Examples include:

- Elevated access
- Additional licences
- Shared mailbox access
- Equipment requests
- Temporary accounts

The decision could determine whether the downstream fulfilment steps are allowed to continue.

---

## Licence Governance

A licence exception request could be submitted for review.

```text
Request Created
      ↓
Manager Approval
      ↓
Licence Administration Review
      ↓
Approved → Assign or retain licence
Rejected → Remove or decline licence
```

---

## Document Governance

Documents uploaded to SharePoint can be reviewed before they are:

- Published
- Shared externally
- Moved into a controlled library
- Marked as final
- Retained as an official business record

---

# 🛠️ Business Problems This Pattern Solves

This approval pattern helps address:

- Unstructured approval emails
- Lost requests
- Missing audit trails
- Manual document movement
- Delayed decision-making
- Unclear document status
- Rejected documents remaining mixed with approved content
- Lack of ownership
- Repeated follow-up emails
- Inconsistent business decisions

---

# ⭐ Key Takeaways

- An approval flow normally follows a trigger, approval, and condition pattern.
- **Start and wait for an approval** pauses the flow until the decision is complete.
- The approval **Outcome** becomes available as dynamic content.
- A Condition routes the flow based on the decision.
- SharePoint actions can automatically organise documents after approval.
- Both the approval and rejection paths must be tested.
- Dynamic content allows the same flow to process every new document.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. The Approval Outcome Must Match Exactly

The condition must compare the returned outcome with the expected value.

Example:

```text
Outcome is equal to Approve
```

Do not assume the result is:

```text
Approved
```

Use the actual value returned by the approval action.

A small mismatch can route every request down the wrong branch.

---

## 2. Always Test Every Branch

Testing only the approved path is not enough.

A production-ready flow must test:

- Approve
- Reject
- Missing approver
- Invalid approver
- Duplicate file name
- Deleted destination folder
- Connection failure
- Permission failure

---

## 3. Include a Direct Link for the Approver

An approver should not have to search manually for the document.

Always include:

```text
Link to item
```

A good approval request provides enough context for the approver to make a decision quickly.

---

## 4. Do Not Hardcode Approvers Without a Good Reason

Hardcoded email addresses become difficult to maintain when:

- Roles change
- Employees leave
- Responsibilities move to another team

Where possible, retrieve the approver dynamically from:

- A SharePoint Person column
- The requestor's manager
- A configuration list
- Dataverse
- An environment variable
- A Microsoft 365 group

---

## 5. Moving a File Changes Its Location

After a rejected document is moved, any previously stored link may no longer work as expected.

Consider whether downstream notifications need:

- The new file link
- The new path
- An updated SharePoint record
- A rejection email with the corrected location

---

## 6. Folder Permissions Must Be Checked

The flow connection account needs permission to:

- Read the source file
- Move the file
- Access the destination folder

The approver also needs permission to open the document.

A technically correct flow can still fail because of permissions.

---

## 7. Rejection Should Include Comments

A rejection without explanation creates more manual follow-up.

Where possible, capture and store:

- Approver name
- Decision
- Comments
- Response date
- Approval ID

The requestor should understand why the request was rejected and what must be corrected.

---

## 8. Do Not Use Approval Emails as the Only Audit Record

Approval details should also be stored in a structured system such as:

- SharePoint
- Dataverse
- SQL
- A case management platform

Emails can be deleted. Structured records are easier to report on and audit.

---

## 9. Plan for No Response

The standard approval action can wait for a long time.

Production designs should consider:

- Reminder notifications
- Escalation
- Timeout handling
- Reassignment
- Cancellation
- Delegated approvers

A flow that waits indefinitely may leave a business request permanently unresolved.

---

## 10. Copilot Output Must Be Reviewed

Copilot can create the initial structure, but it may:

- Select the wrong dynamic content
- Create the wrong condition
- Use an unsuitable approval type
- Place actions in the wrong branch
- Miss business-specific exception handling

Copilot accelerates development but does not replace solution design or testing.

---

# ⚠️ Common Mistakes

- Comparing the outcome against the wrong value.
- Placing the Move file action in the approved branch.
- Using the wrong SharePoint file property.
- Forgetting to create the rejected documents folder.
- Not giving the connection account sufficient permissions.
- Not including the document link in the approval.
- Hardcoding a test approver and forgetting to change it.
- Testing only one outcome.
- Not notifying the document owner of rejection.
- Not recording approval comments.
- Failing to handle duplicate document names.
- Allowing the flow to trigger again when moved documents are reprocessed.

---

# 🔄 Avoiding Repeated or Recursive Processing

A possible design risk is that moving a document could cause another flow to trigger, depending on the trigger and destination design.

To prevent repeated processing, consider:

- Moving rejected files to a separate library.
- Adding a document status column.
- Adding trigger conditions.
- Checking the folder path before starting approval.
- Excluding the Rejected Documents folder.
- Recording whether the file has already been reviewed.

Example logic:

```text
If Folder Path contains "Rejected Documents"
    ↓
Do not start another approval
```

---

# 🏆 Best Practices

- Use descriptive flow and action names.
- Rename actions so the run history is easy to understand.
- Use dynamic approvers where possible.
- Include meaningful approval titles and details.
- Include a direct document link.
- Record decisions and comments.
- Notify the requestor after every outcome.
- Test all decision branches.
- Add error handling.
- Use Solutions for enterprise flows.
- Use environment variables for reusable configuration.
- Document ownership and connection dependencies.
- Monitor run history after deployment.

---

# 🧱 Recommended Production Design

The training exercise uses a simple flow:

```text
Upload
  ↓
Approval
  ↓
Condition
  ↓
Move Rejected File
```

A more complete production design could be:

```text
File Uploaded
      ↓
Validate File and Metadata
      ↓
Create Approval Record
      ↓
Start and Wait for Approval
      ↓
Capture Decision, Comments and Date
      ↓
Update SharePoint Metadata
      ↓
Condition
   /           \
Approve        Reject
  ↓              ↓
Mark Approved   Move to Rejected Folder
  ↓              ↓
Notify Owner    Notify Owner with Comments
   \            /
    \          /
     Update Audit Record
            ↓
       Complete Process
```

---

# 📊 Recommended Audit Fields

A SharePoint list or Dataverse table could store:

| Field | Purpose |
|---|---|
| Document Name | Identifies the file |
| Document Link | Opens the document |
| Submitted By | Identifies the requestor |
| Submitted Date | Records when the process started |
| Approver | Records who reviewed it |
| Approval Outcome | Approve or Reject |
| Approval Comments | Records feedback |
| Approval Date | Records when the decision was made |
| Current Status | Pending, Approved, Rejected, Failed |
| Flow Run ID | Supports troubleshooting |
| Final File Location | Records where the document was stored |

---

# 🚀 How I Would Improve This Solution

For a real business implementation, I would add:

1. A SharePoint status column.
2. A requester notification.
3. Approval comments in the rejection email.
4. A reminder after a defined period.
5. An escalation route for overdue approvals.
6. Error handling using Scopes.
7. A central audit list.
8. Dynamic approver selection.
9. Trigger conditions to prevent duplicate processing.
10. Clear ownership and support documentation.

---

# 🧠 Engineering Design Questions

Before building an approval solution, I should ask:

- What starts the approval?
- Who is allowed to submit documents?
- Who should approve?
- Is one response sufficient?
- Must everyone approve?
- What information does the approver need?
- What happens after approval?
- What happens after rejection?
- Should the file be moved, copied, renamed, or deleted?
- How will comments be recorded?
- What happens if the approver does not respond?
- Who receives reminders?
- What happens if the approver is absent?
- How is the decision audited?
- Could the same document trigger the flow twice?
- Who supports the flow when the creator is unavailable?

---

# 💭 Reflection

This module demonstrated how a predictable approval pattern can turn an unstructured document review process into a controlled and auditable workflow.

The most important lesson is that the approval action is only one part of the solution. A reliable approval process must also manage document access, outcomes, comments, notifications, exceptions, file locations, permissions, and audit records.

The basic pattern is simple:

```text
Trigger
  ↓
Approval
  ↓
Condition
  ↓
Business Action
```

However, building it for real organisational use requires careful consideration of governance, error handling, ownership, security, and long-term support.
