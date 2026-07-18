# 📘 Module 2 - Create a Cloud Flow

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 10 minutes

---

# 📖 Overview

Cloud flows are the foundation of Microsoft Power Automate.

Every cloud flow follows the same fundamental architecture:

```
Trigger
      ↓
Actions
      ↓
Conditions (Optional)
      ↓
Outputs
```

A cloud flow waits for a trigger to occur before executing one or more actions.

Microsoft Copilot can now accelerate this process by generating flows using natural language, significantly reducing development time and lowering the barrier to entry for automation.

---

# 🎯 Learning Objectives

After completing this module I can:

- Understand the structure of a cloud flow.
- Create a cloud flow using Copilot.
- Generate automation using natural language prompts.
- Refine Copilot-generated flows.
- Edit existing flows using Copilot.
- Understand how prompt quality affects flow quality.

---

# ☁️ What is a Cloud Flow?

A cloud flow is an automated workflow that runs within Microsoft's cloud environment.

Unlike Desktop Flows, cloud flows do not require a local machine to remain powered on.

They are event-driven and execute automatically whenever their trigger conditions are met.

---

# 🏗️ Anatomy of a Cloud Flow

Every flow contains four key components:

## 1️⃣ Trigger

The event that starts the automation.

Examples:

- New Microsoft Form submitted
- Email received
- SharePoint item created
- File uploaded
- Scheduled time reached

Without a trigger, the flow never runs.

---

## 2️⃣ Actions

Actions define what the flow does after it starts.

Examples:

- Send an email
- Create a SharePoint item
- Update Excel
- Post a Teams message
- Create Planner task
- Start an approval

A flow may contain one action or hundreds.

---

## 3️⃣ Conditions (Optional)

Conditions allow the flow to make decisions.

Example:

```
If Priority = High

↓

Notify Manager

Else

Notify Team
```

Conditions introduce logic into automation.

---

## 4️⃣ Output

The completed business process.

Examples:

- Approval completed
- Notification sent
- Document archived
- Ticket created

---

# 🤖 Microsoft Copilot

Copilot allows users to build Power Automate flows using natural language.

Instead of manually building every action, users simply describe the desired automation.

Example:

```
When an email arrives from my manager,
post the subject into Microsoft Teams.
```

Copilot automatically generates:

- Trigger
- Actions
- Connections
- Parameters

---

# ✨ What Copilot Can Do

Copilot can:

- Generate new flows
- Configure connectors
- Suggest triggers
- Configure parameters
- Replace actions
- Explain existing flows
- Summarise flows
- Suggest flow descriptions

---

# ✍️ Writing Good Prompts

Prompt quality directly affects the generated flow.

## Good Prompt

```
When an item is created in SharePoint,
send an approval to the Finance Manager
and notify me in Microsoft Teams.
```

---

## Poor Prompt

```
Create approval.
```

Too vague.

---

## Best Practice

Always describe:

- Trigger
- Source system
- Destination system
- Expected outcome

---

# 💼 Real-World Business Scenarios

## Employee Onboarding

Trigger

New starter created.

Actions

- Create Microsoft 365 account
- Assign licence
- Notify manager
- Create Teams welcome message
- Create Planner tasks

---

## Service Desk

Trigger

ServiceNow ticket created.

Actions

- Notify engineer
- Create Teams message
- Update SharePoint
- Send confirmation email

---

## Travel Approval

Trigger

Microsoft Form submitted.

Actions

- Manager approval
- Director approval
- Update SharePoint List
- Notify requester
- Generate audit trail

---

## Invoice Processing

Trigger

Invoice uploaded.

Actions

- Extract details
- Manager approval
- Notify Finance
- Archive document

---

# 💼 Real-World Applications (My Experience)

These concepts directly relate to automation solutions I have designed, including:

- Multi-stage approval workflows
- Microsoft Forms integrations
- SharePoint List automation
- Automated notifications
- Sequential approvals
- Service request automation
- International travel approval workflows
- Joiner, Mover and Leaver (JML) automation

Although these solutions vary in complexity, they all begin with the same fundamental structure:

```
Trigger

↓

Actions

↓

Business Logic

↓

Outcome
```

---

# ⭐ Key Takeaways

✔ Every cloud flow begins with a trigger.

✔ A trigger only starts the flow—it does not perform work.

✔ Actions perform the work.

✔ Conditions introduce business logic.

✔ Copilot accelerates development but still requires human validation.

---

# 🚨 Important Points (Never Forget)

## Copilot is an assistant, not an architect

Always review:

- Trigger
- Actions
- Conditions
- Dynamic content
- Connections
- Security

Never assume Copilot generated the perfect flow.

---

## Validate every connection

After Copilot creates a flow:

✔ Check authentication

✔ Verify permissions

✔ Confirm connector ownership

---

## Be specific when prompting

Poor prompts produce poor flows.

Good prompts include:

- Trigger
- Source
- Destination
- Expected action

---

## Review generated actions

Copilot may:

- select incorrect connectors
- configure wrong parameters
- miss business logic

Always review before deployment.

---

## Save frequently

Power Automate does not automatically save every change.

Save regularly during development.

---

# ⚠️ Common Mistakes

❌ Starting development before understanding the business process.

❌ Using vague prompts.

❌ Forgetting to verify connections.

❌ Assuming Copilot understands company-specific processes.

❌ Deploying flows without testing.

❌ Ignoring error handling.

---

# 🛠 Problems This Module Helps Solve

- Manual email processing
- Manual approvals
- Delayed notifications
- Repetitive administration
- Missed tasks
- Poor communication between systems
- Human error
- Slow business processes

---

# 🏆 Best Practices

✅ Understand the business process first.

✅ Design the trigger carefully.

✅ Use descriptive flow names.

✅ Test every branch.

✅ Validate every connector.

✅ Keep prompts specific.

✅ Save frequently.

✅ Always perform end-to-end testing before production deployment.

---

# 💭 Reflection

This module reinforces that successful automation is not simply about building flows—it begins with understanding the business process and selecting the correct trigger.

Copilot is an excellent productivity tool that can dramatically reduce development time, but it should always be treated as an assistant rather than a replacement for good solution design. Effective prompts, thorough validation, and comprehensive testing remain essential to building reliable, production-ready automations.

# 🚀 How I Could Apply This at Work

After completing this module, I identified several opportunities where these concepts could improve existing business processes:

- Standardising approval workflows.
- Automating ServiceNow notifications.
- Improving Joiner, Mover and Leaver processes.
- Enhancing Microsoft Forms integrations.
- Automating SharePoint document processing.
- Reducing manual email handling.

