# 📘 Module 8 - Introduction to Approval Flows

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 1 minute

---

# 📖 Overview

Approval Flows enable organisations to automate decision-making processes by routing requests to one or more reviewers, collecting their responses, and automatically performing the next business action.

Instead of relying on lengthy email chains, manual follow-ups, or verbal approvals, Power Automate provides a structured, traceable, and auditable approval process.

Approval workflows improve governance, accountability, and operational efficiency while ensuring every decision is properly recorded.

---

# 🎯 Learning Objectives

After completing this module I can:

- Understand how Approval Flows work.
- Understand the purpose of the Approvals connector.
- Differentiate between approval actions.
- Understand approval response types.
- Use approval outcomes to drive business logic.
- Recognise common enterprise approval scenarios.

---

# 🏗️ Approval Flow Architecture

```
Business Event
        │
        ▼
Trigger
        │
        ▼
Start Approval
        │
        ▼
Approver Reviews Request
        │
        ▼
Decision
 ┌───────────────┐
 │               │
 ▼               ▼
Approved      Rejected
 │               │
 ▼               ▼
Continue     Alternative Action
```

---

# 🔑 Key Concepts Learned

## 1️⃣ Approval Flows

Approval Flows automate decision-making processes.

Instead of manually asking someone to approve a request,

Power Automate:

- Sends the approval.
- Waits for a decision.
- Records the response.
- Continues automatically.

---

## 2️⃣ The Approvals Connector

Power Automate includes a built-in **Approvals connector**.

Unlike most connectors, it **cannot trigger a flow**.

Instead, it works as part of an existing flow.

Typical flow structure:

```
Trigger

↓

Approval Action

↓

Decision

↓

Next Business Process
```

---

# ⚙️ Approval Actions

## Create an Approval

Creates the approval request.

The flow **continues immediately**.

Useful when other processing can happen while waiting for a decision.

---

## Wait for an Approval

Waits until a previously created approval has been completed.

Usually paired with:

```
Create an Approval

↓

Wait for an Approval
```

---

## Start and Wait for an Approval

The most commonly used approval action.

It:

- Creates the approval.
- Waits for the response.
- Returns the outcome.

Ideal for straightforward approval workflows.

---

## Start and Wait for an Approval of Text

Similar to the previous action,

but allows approvers to review and edit text before responding.

Useful for:

- Document reviews.
- Draft policies.
- Procedure updates.
- Content approvals.

---

# 📋 Approval Types

## Approve / Reject

Standard approval.

Approver selects:

```
Approve

or

Reject
```

---

### Everyone Must Approve

Every assigned approver must approve.

Example:

```
Manager

↓

Finance

↓

Director
```

One rejection causes the overall approval to fail.

---

### First to Respond

The first approver to respond determines the outcome.

Useful when:

- Multiple support engineers.
- Shared mailboxes.
- Duty managers.

Fastest response wins.

---

## Custom Responses

Instead of:

```
Approve

Reject
```

You define your own options.

Examples:

- Needs Revision
- Escalate
- More Information Required
- Approved with Conditions
- Send Back

This provides greater flexibility and supports more complex business processes.

---

# 📊 Dynamic Content

Once an approval is completed,

Power Automate exposes:

```
Outcome
```

Examples:

```
Approved

Rejected

Needs Revision

Escalated
```

This value can be used in Conditions to determine the next step in the process.

---

# 💼 Real-World Business Scenarios

## Annual Leave Request

Employee submits request.

↓

Manager approval.

↓

Employee notified.

---

## Purchase Request

Employee submits purchase request.

↓

Manager approval.

↓

Finance approval.

↓

Purchase Order created.

---

## Document Review

New document uploaded.

↓

Reviewer approval.

↓

Publish document.

or

↓

Move to Rejected folder.

---

## New Starter Request

Manager submits onboarding request.

↓

HR approval.

↓

IT provisioning.

↓

Equipment ordered.

---

## Software Request

Employee requests software.

↓

Manager approval.

↓

IT approval.

↓

Licence assigned.

---

# 💼 Real-World Applications (My Experience)

Approval workflows are highly relevant to the solutions I build and support.

Examples include:

- Travel request approvals.
- Site visit approval workflows.
- Microsoft Forms approval processes.
- Service request approvals.
- Governance and compliance workflows.
- Document review and sign-off.
- Business process automation across Microsoft 365.

These solutions demonstrate how structured approvals can replace manual email chains while providing full visibility and auditability.

---

# ⭐ Key Takeaways

✔ Approval Flows automate decision-making.

✔ The Approvals connector is an action—not a trigger.

✔ Approval outcomes drive the next stage of the business process.

✔ Different approval types support different business requirements.

✔ Every approval creates an auditable record.

---

# 🚨 Important Points (Never Forget)

## An Approval Cannot Start a Flow

This is one of the most common misunderstandings.

Incorrect:

```
Approval

↓

Trigger
```

Correct:

```
Trigger

↓

Approval
```

A flow always starts with another trigger, such as:

- Microsoft Forms
- SharePoint
- Outlook
- Dataverse
- Recurrence

---

## Choose the Right Approval Type

Ask:

Do multiple people need to approve?

If yes:

```
Everyone Must Approve
```

If only one response is needed:

```
First to Respond
```

Choosing the wrong approval type can delay business processes unnecessarily.

---

## Think Beyond Approve / Reject

Many organisations require richer outcomes.

Examples:

- Needs Revision
- Escalated
- Deferred
- More Information Required

Custom responses create more flexible workflows.

---

## Always Plan for Rejections

Never build only the "Approved" path.

Every production approval should define:

- Approved
- Rejected
- Cancelled
- Timed Out (where applicable)

Good automation considers every possible outcome.

---

## Capture an Audit Trail

Approval flows naturally record:

- Who approved.
- When they approved.
- Their response.
- Comments.
- Decision history.

This supports compliance, governance, and future audits.

---

# ⚠️ Common Mistakes

❌ Assuming approvals can trigger flows.

❌ Choosing the wrong approval type.

❌ Ignoring rejection paths.

❌ Not recording approval comments.

❌ Hardcoding approvers instead of using dynamic values.

❌ Forgetting to notify requesters of the final decision.

---

# 🛠 Problems This Module Helps Solve

- Manual approval emails.
- Lost approval requests.
- Slow decision-making.
- Lack of audit history.
- Inconsistent business processes.
- Compliance challenges.
- Approval bottlenecks.
- Manual follow-ups.

---

# 🏆 Best Practices

✅ Use **Start and Wait for an Approval** for most approval scenarios.

✅ Choose the appropriate approval type based on business requirements.

✅ Notify requesters of the outcome.

✅ Record approval comments where possible.

✅ Use dynamic approvers rather than hardcoding email addresses.

✅ Include rejection and exception paths.

✅ Test all approval outcomes before production deployment.

---

# 🚀 Enterprise Design Checklist

Before deploying an approval workflow, ask:

- What starts the approval?
- Who should approve?
- Is one approval enough, or must everyone approve?
- What happens if the request is rejected?
- What happens if no one responds?
- How will the requester be notified?
- Is the approval history retained for audit purposes?
- Are approvers determined dynamically where possible?

Designing with these questions in mind helps create resilient, scalable, and compliant approval processes.

---

# 💭 Reflection

This module reinforced that approval workflows are far more than simple "Approve" or "Reject" buttons. They provide a structured framework for business decision-making, ensuring requests are processed consistently, transparently, and with a complete audit trail.

The most important lesson is that a successful approval process doesn't end with collecting a decision—it must also define what happens after every possible outcome. Well-designed approval flows improve governance, reduce manual effort, and ensure organisations can confidently automate critical business processes.
