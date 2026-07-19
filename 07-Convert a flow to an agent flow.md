# 📘 Module 7 - Convert a Flow to an Agent Flow

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 5 minutes

---

# 📖 Overview

Traditional cloud flows automate business processes based on predefined triggers and actions.

Agent Flows extend this capability by allowing automation to become part of an **AI-powered conversational experience** using **Microsoft Copilot Studio**.

Rather than only responding to system events, Agent Flows can be invoked by AI agents during conversations or autonomous tasks, enabling more intelligent and context-aware business automation.

This represents the next evolution of Power Automate within the Microsoft Power Platform.

---

# 🎯 Learning Objectives

After completing this module I can:

- Understand what an Agent Flow is.
- Differentiate between Cloud Flows and Agent Flows.
- Convert a Cloud Flow into an Agent Flow.
- Understand Copilot Studio integration.
- Understand Agent Flow billing and capacity.
- Identify scenarios where Agent Flows provide greater business value.

---

# 🏗️ Cloud Flow vs Agent Flow

## Traditional Cloud Flow

```
Business Event

↓

Trigger

↓

Actions

↓

Business Process
```

Example:

```
New Microsoft Form

↓

Manager Approval

↓

Send Email

↓

Update SharePoint
```

---

## Agent Flow

```
User

↓

Copilot Agent

↓

Agent Flow

↓

Business Systems

↓

Response Back to User
```

Instead of waiting for a predefined trigger, an AI agent decides when to execute the workflow based on the conversation or task.

---

# 🤖 What is an Agent Flow?

An Agent Flow is an automation managed within **Microsoft Copilot Studio** that can be called by AI agents.

It uses the same core building blocks as a cloud flow:

- Trigger
- Actions
- Conditions
- Connectors

However, it is specifically designed to support AI-driven experiences.

---

# 🔑 Key Characteristics

Agent Flows:

✅ Can be used by Copilot Studio agents.

✅ Support AI-driven automation.

✅ Can process conversational requests.

✅ Can invoke other agents.

✅ Can perform document processing.

✅ Are managed within Copilot Studio.

---

# 🔄 Converting a Cloud Flow

A Cloud Flow can be converted into an Agent Flow.

Requirements:

- Cloud Flow only
- Must belong to a Solution
- Copilot Studio capacity available

Conversion Process

```
Existing Cloud Flow

↓

Open Flow

↓

Edit

↓

Change Plan

↓

Copilot Studio

↓

Save

↓

Confirm Conversion
```

---

# ⚠️ Important Limitation

Flow conversion is **one-way only**.

```
Cloud Flow

↓

Agent Flow

✓

Agent Flow

↓

Cloud Flow

❌ Not Supported
```

Once converted, the billing model changes from Power Automate capacity to Copilot Studio capacity.

This cannot currently be reversed.

---

# 🏢 Where Agent Flows Are Managed

Cloud Flows

```
Power Automate
```

Agent Flows

```
Copilot Studio

↓

Workflows
```

Although Agent Flows remain visible in Power Automate, they are primarily managed through Copilot Studio.

---

# 💳 Capacity & Billing

Traditional Cloud Flows consume:

```
Power Automate Capacity
```

Agent Flows consume:

```
Copilot Studio Capacity
```

Important:

Testing an Agent Flow inside the designer or Copilot Studio test chat **does not consume capacity**.

Production executions do consume Copilot Studio capacity.

---

# 💼 Real-World Business Scenarios

## IT Service Desk

Employee asks:

> "Why can't I access Microsoft Teams?"

Copilot Agent:

- Checks Entra ID account.
- Reviews assigned licences.
- Verifies Conditional Access.
- Returns troubleshooting advice.
- Escalates to Service Desk if required.

---

## HR

Employee asks:

> "How many annual leave days do I have?"

Agent Flow:

- Queries HR system.
- Retrieves leave balance.
- Responds instantly.

---

## Procurement

Manager asks:

> "Has my purchase request been approved?"

Agent:

- Checks approval status.
- Retrieves comments.
- Returns current progress.

---

## Finance

Employee asks:

> "Where is my expense claim?"

Agent:

- Searches Finance system.
- Retrieves payment status.
- Responds immediately.

---

## Modern Workplace

Employee asks:

> "Can you create a Microsoft Team for Project Phoenix?"

Agent:

- Creates Team.
- Creates SharePoint site.
- Creates Planner plan.
- Adds members.
- Sends confirmation.

---

# 💼 Real-World Applications (My Experience)

As a Modern Workplace Engineer, I can see Agent Flows enhancing many of the automation scenarios I already work with by making them conversational and AI-driven.

Potential use cases include:

- Microsoft 365 self-service support.
- User access requests through Copilot.
- Password reset guidance.
- Licence assignment requests.
- Device compliance checks.
- Approval status enquiries.
- Employee onboarding assistance.
- Knowledge retrieval from SharePoint.
- Service request automation.

Instead of users completing forms or manually navigating portals, a Copilot agent could understand their request, trigger an Agent Flow, and return the outcome in natural language.

---

# ⭐ Key Takeaways

✔ Agent Flows are built on Cloud Flow technology.

✔ They integrate directly with Microsoft Copilot Studio.

✔ AI agents can trigger Agent Flows automatically.

✔ Agent Flows consume Copilot Studio capacity.

✔ Cloud Flow → Agent Flow conversion is permanent.

---

# 🚨 Important Points (Never Forget)

## Agent Flows are NOT replacements for Cloud Flows

Cloud Flows remain the best choice for:

- Scheduled tasks
- Event-driven automation
- System-to-system integrations
- Background processes

Use Agent Flows when automation needs to be initiated or guided by an AI conversation.

---

## Solutions Are Mandatory

Only flows stored inside a **Solution** can be converted.

This reinforces Microsoft's recommendation that enterprise Power Platform development should always use Solutions for deployment, version control, and lifecycle management.

---

## Understand the Billing Impact

Before converting a production flow:

- Check available Copilot Studio capacity.
- Confirm licensing.
- Assess expected usage.

Running out of Copilot Studio capacity can prevent Agent Flows from executing.

---

## Treat Conversion as Permanent

Since conversion cannot be reversed:

- Test thoroughly first.
- Confirm the business need.
- Validate governance and support requirements.

---

# ⚠️ Common Mistakes

❌ Converting a flow that isn't in a Solution.

❌ Assuming conversion can be undone.

❌ Forgetting to check Copilot Studio capacity.

❌ Converting scheduled background processes unnecessarily.

❌ Not considering the impact on licensing and billing.

---

# 🛠 Problems This Module Helps Solve

- Manual employee support.
- Slow service desk interactions.
- Repetitive HR enquiries.
- Knowledge retrieval.
- Approval status requests.
- IT self-service.
- Conversational automation.
- AI-assisted business processes.

---

# 🏆 Best Practices

✅ Build reusable Cloud Flows before considering conversion.

✅ Store enterprise flows inside Solutions.

✅ Monitor Copilot Studio capacity.

✅ Design Agent Flows with conversational users in mind.

✅ Keep business logic modular and reusable.

✅ Validate governance and security before deployment.

---

# 🚀 Enterprise Design Decision

When designing a new automation, ask:

### Is this process triggered by a system event?

Examples:

- New email.
- SharePoint item created.
- Scheduled report.
- Form submission.

➡️ Use a **Cloud Flow**.

---

### Is this process initiated through an AI conversation?

Examples:

- "Create a Team for my project."
- "Check my leave balance."
- "Approve my request."
- "Find my onboarding documents."

➡️ Use an **Agent Flow**.

Choosing the right automation model ensures better scalability, user experience, and licensing efficiency.

---

# 💭 Reflection

This module highlights Microsoft's shift towards AI-first automation. While Cloud Flows remain essential for traditional workflow automation, Agent Flows enable those same processes to become part of intelligent, conversational experiences through Microsoft Copilot Studio.

The key lesson is that automation is evolving beyond responding to system events. By integrating workflows with AI agents, organisations can provide more natural, self-service experiences that reduce manual effort, improve accessibility, and enhance productivity. Understanding when to use Cloud Flows versus Agent Flows will be an increasingly important skill as AI capabilities continue to expand across the Power Platform.
