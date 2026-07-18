# 📘 Module 1 - Introducing Power Automate

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 10 minutes

---

# 📖 Overview

Power Automate is Microsoft's cloud-based workflow automation platform that enables users to automate repetitive tasks and business processes across hundreds of Microsoft and third-party applications.

Rather than performing manual, repetitive activities, Power Automate allows workflows ("Flows") to execute automatically based on predefined triggers and actions.

It acts as the automation engine within the Microsoft Power Platform.

---

# 🎯 Learning Objectives

After completing this module I can:

- Explain what Power Automate is.
- Describe common business scenarios where automation adds value.
- Understand the different ways flows can be triggered.
- Create scheduled flows.
- Create flows that automatically save email attachments.
- Share flows with other users.
- Troubleshoot failed flows.

---

# 💡 What is Power Automate?

Power Automate is an online workflow automation service that allows different systems, applications and services to communicate with one another.

Instead of performing manual actions repeatedly, Power Automate performs those actions automatically based on business rules.

It supports automation across:

- Microsoft 365
- SharePoint
- Microsoft Teams
- Outlook
- OneDrive
- Excel
- SQL Server
- Dataverse
- Dynamics 365
- Salesforce
- Jira
- Dropbox
- Hundreds of additional connectors

---

# ⚙️ Core Concept

Every Power Automate solution is built around the same principle:

```
Trigger
      ↓
Action
      ↓
Condition (Optional)
      ↓
More Actions
      ↓
Output
```

Everything begins with a **Trigger**.

Without a trigger, nothing happens.

---

# 🔑 Key Concepts Learned

## 1. Automation saves time

Instead of users performing repetitive manual work:

- Sending emails
- Copying files
- Updating spreadsheets
- Requesting approvals
- Sending reminders

Power Automate performs these tasks automatically.

---

## 2. Power Automate connects systems together

One of its greatest strengths is integration.

Example:

```
Microsoft Forms
      ↓
SharePoint List
      ↓
Approval
      ↓
Email Notification
      ↓
Microsoft Teams
```

Instead of users moving information manually between systems, Power Automate becomes the bridge.

---

## 3. Automation improves consistency

Humans:

- forget
- make mistakes
- delay actions

Flows execute exactly the same process every time.

---

## 4. Cloud-based automation

Flows run online.

They do not require your computer to remain switched on (for cloud flows).

---

# 🏢 Real-World Business Scenarios

Examples from typical organisations:

### Employee Onboarding

Trigger:

New employee added.

Automation:

- Create Microsoft 365 account
- Notify IT
- Assign licences
- Notify manager
- Create welcome email

---

### Leave Request

Trigger:

Employee submits Microsoft Form.

Automation:

- Manager Approval
- HR Notification
- Calendar Update
- Employee Notification

---

### Invoice Approval

Trigger:

Invoice uploaded.

Automation:

- Send approval
- Wait for response
- Notify Finance
- Archive invoice

---

### Customer Support

Trigger:

Support ticket created.

Automation:

- Assign priority
- Notify engineer
- Create Teams message
- Update CRM

---

### Document Management

Trigger:

File uploaded.

Automation:

- Rename document
- Save to SharePoint
- Notify team

---

# 💼 Real-World Applications (My Experience)

Throughout my role as a Senior Modern Workplace Engineer I have already applied many of these concepts, including:

- Multi-stage travel approval workflows
- Microsoft Forms integrations
- SharePoint List automation
- Automated email notifications
- Sequential approval processes
- Service request automation
- User provisioning support
- Governance workflows

This module reinforces the design principles behind those solutions.

---

# ⭐ Key Takeaways

✔ Every flow starts with a Trigger.

✔ Connectors are what allow Power Automate to communicate with other systems.

✔ Automation should remove repetitive manual work.

✔ Good automation should improve consistency and reduce human error.

✔ Cloud flows run in Microsoft's cloud rather than on a local machine.

---

# 🚨 Important Points (Never Forget)

## Always identify the trigger first

When designing a solution, never begin with the actions.

First ask:

> **What event starts this process?**

Everything else depends on the trigger.

---

## Understand the business process before building

Don't automate a bad process.

Always map:

```
Current Process

↓

Pain Points

↓

Improved Process

↓

Automation
```

Automation should improve a process—not simply digitise an inefficient one.

---

## Keep flows simple

Small, modular flows are easier to:

- maintain
- troubleshoot
- improve

Avoid building one enormous flow when several smaller flows are more appropriate.

---

## Naming standards matter

Avoid names such as:

```
Flow 1

Test Flow

New Flow
```

Instead use descriptive names.

Example:

```
Employee Onboarding Approval

Travel Request Approval

Automatic Licence Notification
```

---

## Build for failure

Every production flow should consider:

- missing data
- failed approvals
- unavailable systems
- connector failures
- timeout scenarios

Never assume everything succeeds.

---

# 🛠 Common Problems Power Automate Solves

- Manual approvals
- Repetitive emails
- File movement
- Reminder emails
- Data synchronisation
- Notification delays
- Human error
- Missed requests
- Duplicate work
- Slow business processes

---

# 📱 Administration Features

Power Automate allows administrators to:

- Enable or disable flows
- Review run history
- Monitor failures
- Share flows
- Manage approvals
- Manage solutions
- Monitor desktop flows

---

# 📍 Useful Areas of the Portal

| Area | Purpose |
|---------|---------|
| Home | Dashboard and Copilot |
| Create | Build new flows |
| Templates | Ready-made flow templates |
| My Flows | Manage existing flows |
| Approvals | Approval management |
| Solutions | Package and manage components |
| Process Mining | Analyse business processes |
| AI Models | AI Builder |
| Desktop Flow Activity | Monitor desktop automations |

---

# 📚 Helpful Resources

- Microsoft Learn
- Microsoft Power Automate Documentation
- Power Automate Community
- Microsoft Power Platform Documentation

---

# 🧠 Reflection

This module reinforces that Power Automate is far more than an automation tool—it is an integration platform that enables organisations to standardise business processes, reduce manual effort, improve consistency, and connect systems that would otherwise operate independently.

The most important lesson from this module is that successful automation begins with understanding the business process before writing a single flow.
