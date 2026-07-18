# 📘 Module 5 - Share Flows

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 7 minutes

---

# 📖 Overview

Building a flow is only the beginning of the automation lifecycle.

In enterprise environments, flows should rarely be owned by a single individual. Business continuity depends on multiple people being able to maintain, update, and troubleshoot automations.

This module introduces **Shared Flows**, allowing multiple users to co-own and manage a Power Automate solution.

Sharing flows improves collaboration, reduces operational risk, and ensures automation continues even if the original creator is unavailable.

---

# 🎯 Learning Objectives

After completing this module I can:

- Share cloud flows with other users.
- Add and remove co-owners.
- Understand shared ownership.
- Understand connection ownership.
- Manage flow permissions.
- Apply governance best practices for production automations.

---

# 🏗️ Shared Flow Architecture

```
Flow Creator
       │
       │
Add Co-Owners
       │
       ▼
───────────────────────────

Owner A

Owner B

Owner C

───────────────────────────

↓

Shared Maintenance

↓

Business Continuity
```

---

# 🔑 Key Concepts Learned

## 1️⃣ Shared Flows

A shared flow is simply a cloud flow with multiple owners.

Instead of relying on one person, several authorised users can manage the automation.

Benefits include:

- Business continuity
- Shared administration
- Easier maintenance
- Reduced operational risk

---

## 2️⃣ Co-Owners

Co-owners can:

✅ Edit the flow

✅ View run history

✅ Start or stop the flow

✅ Add actions

✅ Remove actions

✅ Update properties

✅ Add additional owners

✅ Remove other owners

✅ Delete the flow

However,

❌ They cannot remove the original creator.

---

## 3️⃣ Shared with Me

When a flow is shared:

The creator continues to see it under:

```
My Flows
```

Co-owners see it under:

```
Shared with Me
```

---

## 4️⃣ Connections

Every flow depends on one or more connections.

Examples:

- Outlook
- SharePoint
- Teams
- Excel
- OneDrive
- SQL

Connections authenticate the flow to external services.

---

## 5️⃣ Embedded Connections

Embedded connections are actively being used by the flow.

Example:

```
Outlook

↓

Send Email
```

---

## 6️⃣ Other Connections

Sometimes connections remain attached even though no action currently uses them.

These appear as:

```
Other Connections
```

Unused connections can usually be cleaned up to simplify maintenance.

---

# 💼 Real-World Business Scenarios

## IT Service Desk

A workflow processes user requests.

If one administrator leaves the company,

another administrator can continue maintaining the flow.

---

## HR

Employee onboarding automation.

Multiple HR administrators can:

- update approvals
- change emails
- modify notifications

without rebuilding the solution.

---

## Finance

Invoice approval flow.

Finance Managers can maintain the workflow without depending on the original developer.

---

## Compliance

Governance automation.

Multiple administrators can review run history and investigate failures.

---

# 💼 Real-World Applications (My Experience)

One of the biggest lessons from this module relates directly to enterprise solution design.

Rather than building production automations under an individual user account, I would recommend:

- Using a dedicated service account where appropriate.
- Assigning multiple co-owners to business-critical flows.
- Documenting ownership and responsibilities.
- Ensuring knowledge transfer before planned absences.

This approach improves resilience, supports governance, and reduces the risk of automation becoming dependent on a single individual.

---

# ⭐ Key Takeaways

✔ Production flows should never rely on one person.

✔ Multiple owners improve business continuity.

✔ Connections belong to the user who created them.

✔ Shared ownership improves supportability.

✔ Governance is just as important as automation.

---

# 🚨 Important Points (Never Forget)

## Never Build Business-Critical Flows Under a Personal Account

Imagine:

```
Developer leaves company

↓

Account disabled

↓

Critical business automation stops
```

This is one of the most common enterprise mistakes.

Whenever possible:

- Use a Service Account.
- Use a Shared Mailbox.
- Use a Managed Service Identity (where supported).
- Assign multiple owners.

---

## Co-Owners Do NOT Own Connections

This is extremely important.

Even if another administrator owns the flow,

they **cannot change credentials** created by another owner.

Connections remain tied to the original account unless they are updated.

---

## Removing Owners Can Break Flows

If you remove someone whose credentials are being used,

the flow may fail.

Always:

```
Update Connections

↓

Test Flow

↓

Remove Owner
```

Never remove the owner first.

---

## Share With Teams, Not Individuals

Instead of:

```
John Smith
```

consider sharing with:

```
IT Automation Team

Service Delivery Team

Modern Workplace Team
```

This simplifies long-term maintenance.

---

## Document Every Production Flow

Every production flow should include documentation covering:

- Purpose
- Trigger
- Actions
- Dependencies
- Owners
- Service Accounts
- Connection Owners
- Business Owner
- Support Contact

Good documentation reduces support effort and speeds up troubleshooting.

---

# ⚠️ Common Mistakes

❌ Only one owner.

❌ Personal account owns production flow.

❌ No documentation.

❌ Removing owners before updating connections.

❌ Sharing with too many people.

❌ Using personal email connections.

❌ Forgetting to test after ownership changes.

---

# 🛠 Problems This Module Helps Solve

- Key-person dependency.
- Poor business continuity.
- Unsupported automations.
- Governance issues.
- Knowledge loss.
- Maintenance bottlenecks.
- Staff turnover.
- Operational risk.

---

# 🏆 Best Practices

✅ Use Service Accounts for production.

✅ Add multiple co-owners.

✅ Review ownership regularly.

✅ Document connection ownership.

✅ Keep flow documentation up to date.

✅ Test after permission changes.

✅ Remove unused connections.

---

# 🚀 Enterprise Governance Checklist

Before deploying any production flow, ask:

- Who owns this flow?
- Who supports this flow?
- What account owns the connections?
- What happens if the creator leaves?
- Is the flow documented?
- Is there a backup owner?
- Has the flow been tested after sharing?
- Are unused connections removed?

If you cannot answer these questions, the solution is not production-ready.

---

# 💭 Reflection

This module highlighted that successful automation extends beyond building workflows—it also requires designing for long-term support, governance, and business continuity.

One of the most valuable lessons is understanding that ownership of a flow is different from ownership of its connections. Production-ready solutions should be built with resilience in mind by using shared ownership, appropriate service accounts, documented responsibilities, and regular governance reviews. These practices help ensure automations remain reliable, maintainable, and sustainable as teams and organisations evolve.
