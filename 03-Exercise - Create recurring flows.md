# 📘 Module 3 - Create Recurring (Scheduled) Flows

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 5 minutes

---

# 📖 Overview

In this module, I learned how to create **Scheduled Cloud Flows** using the **Recurrence** trigger.

Unlike event-driven flows, which wait for something to happen (such as a new email or Microsoft Form submission), recurring flows execute automatically at predefined intervals.

Examples include:

- Daily
- Weekly
- Monthly
- Every hour
- Every minute

Recurring flows are ideal for routine business processes that must run consistently without requiring user interaction.

---

# 🎯 Learning Objectives

After completing this module I can:

- Create scheduled cloud flows.
- Configure the Recurrence trigger.
- Read data from Microsoft Excel.
- Use dynamic content.
- Process multiple records using **Apply to each**.
- Send personalised emails automatically.

---

# 🏗️ Solution Architecture

```
Recurrence Trigger
        ↓
Read Excel Table
        ↓
Apply to Each Row
        ↓
Send Email
```

---

# 🔑 Key Concepts Learned

## 1️⃣ Recurrence Trigger

The **Recurrence** trigger starts a flow based on time rather than an event.

Examples:

- Every day
- Every Monday
- Every month
- Every 2 hours
- Every 15 minutes

Unlike other triggers, Recurrence does not require user activity.

---

## 2️⃣ Excel as a Data Source

Power Automate can retrieve structured data directly from Excel.

Requirements:

- Excel file stored in OneDrive or SharePoint
- Data formatted as a Table
- Table contains column headers

Example:

| ContactEmail | FirstName | LastName |
|---------------|-----------|----------|
| john@contoso.com | John | Smith |

---

## 3️⃣ List Rows Present in a Table

This action retrieves every row from the Excel table.

Each row becomes available for further processing.

---

## 4️⃣ Apply to Each

Whenever multiple records are returned, Power Automate automatically creates an **Apply to each** loop.

Example:

Excel contains:

```
John

Sarah

David
```

Flow executes:

```
Email John

↓

Email Sarah

↓

Email David
```

The loop repeats automatically for every record.

---

## 5️⃣ Dynamic Content

Dynamic Content inserts values retrieved from previous actions.

Instead of typing fixed text:

```
Dear Customer
```

Power Automate can generate:

```
Dear John

Dear Sarah

Dear David
```

using:

```
FirstName
```

from Excel.

---

# 💼 Real-World Business Scenarios

## Daily Reminder Emails

Runs every morning.

Examples:

- Outstanding approvals
- Pending invoices
- Expiring contracts
- Tasks due today

---

## Weekly Reports

Runs every Friday.

Examples:

- Service Desk KPI report
- Licence usage
- Device compliance
- Intune reports

---

## Monthly Governance

Runs automatically.

Examples:

- Inactive accounts
- Stale devices
- Guest user review
- Group membership review

---

## Scheduled Notifications

Examples:

- Maintenance reminders
- Planned outages
- Security awareness campaigns

---

## HR Communications

Automatically send:

- Welcome emails
- Induction reminders
- Benefits information
- Mandatory training reminders

---

# 💼 Real-World Applications (My Experience)

This pattern could be applied to several business processes that I support, including:

- Daily licence governance reports
- Automated Microsoft 365 health summaries
- Copilot usage reporting
- Weekly inactive account reviews
- Scheduled SharePoint reminders
- Follow-up notifications for outstanding approvals
- Compliance reporting for device management
- Automated communication with users based on scheduled events

---

# ⭐ Key Takeaways

✔ Scheduled flows do not rely on user interaction.

✔ Excel must be formatted as a Table before Power Automate can read it.

✔ Apply to each processes every record individually.

✔ Dynamic Content personalises automation.

✔ Recurring flows are ideal for routine administrative tasks.

---

# 🚨 Important Points (Never Forget)

## Excel MUST contain a Table

Power Automate cannot reliably read ordinary ranges.

Always:

```
Insert

↓

Table

↓

Save
```

before connecting Excel.

---

## Store Excel Online

Supported locations include:

- SharePoint Online

- OneDrive for Business

Avoid using local files for cloud flows.

---

## Every Row = One Loop

Whenever "List rows" returns multiple records,

Power Automate executes:

```
Apply to Each
```

once per row.

Large datasets can significantly increase run time.

---

## Dynamic Content is Your Friend

Avoid hardcoding values.

Instead use:

- Email Address
- Name
- Department
- Manager
- Status

This makes flows reusable.

---

## Test Before Scheduling

Before enabling recurrence:

✔ Run manually

✔ Verify emails

✔ Check Excel mapping

✔ Confirm dynamic content

Never schedule an untested flow.

---

# ⚠️ Common Mistakes

❌ Forgetting to format Excel as a Table.

❌ Storing Excel locally.

❌ Hardcoding recipient email addresses.

❌ Ignoring Apply to Each loops.

❌ Scheduling flows too frequently.

❌ Forgetting time zone settings.

❌ Not considering duplicate emails.

---

# 🛠 Problems This Module Helps Solve

- Manual reminder emails
- Weekly reporting
- Customer follow-ups
- Marketing campaigns
- Governance reporting
- Compliance notifications
- Administrative overhead
- Repetitive communication

---

# 🏆 Best Practices

✅ Keep Excel tables clean and structured.

✅ Use meaningful column names.

✅ Test with small datasets first.

✅ Validate dynamic content.

✅ Avoid unnecessary recurrence frequency.

✅ Monitor run history regularly.

✅ Add error handling for production flows.

---

# 🚀 Engineering Tip

Ask yourself:

> **Does this process really need a person to press a button?**

If the answer is **No**, a scheduled flow may be the better solution.

---

# 💭 Reflection

This module demonstrated how recurring cloud flows can automate routine business tasks without relying on user interaction. By combining a Recurrence trigger with structured Excel data, looping through records, and using dynamic content, it's possible to build scalable automations that save time, reduce manual effort, and improve consistency.

The biggest takeaway from this module is that many repetitive administrative tasks can be transformed into reliable scheduled automations with very little manual intervention.


# 🎓 How I Would Apply This in My Organisation

Potential opportunities:

- Daily Microsoft 365 licence reporting.
- Weekly inactive account notifications.
- Scheduled reminders for managers to complete access reviews.
- Monthly SharePoint governance reports.
- Automated Copilot usage summaries.
- Device compliance reporting from Intune.
- Weekly follow-up emails for outstanding approvals.
