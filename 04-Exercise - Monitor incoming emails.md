# 📘 Module 4 - Monitor Incoming Emails

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 5 minutes

---

# 📖 Overview

In this module, I learned how to create an **Automated Cloud Flow** that monitors an Outlook mailbox and automatically performs actions whenever an email matching specific criteria is received.

Rather than checking emails manually, Power Automate continuously monitors the mailbox and triggers a workflow whenever predefined conditions are met.

This is one of the most common automation patterns used across Microsoft 365 environments.

---

# 🎯 Learning Objectives

After completing this module I can:

- Create an Automated Cloud Flow.
- Use the **When a new email arrives (V3)** trigger.
- Filter emails using multiple conditions.
- Automatically save email attachments to SharePoint.
- Use Dynamic Content.
- Understand how Power Automate automatically creates an **Apply to each** loop for multiple attachments.

---

# 🏗️ Solution Architecture

```
New Email Arrives
        ↓
Check Email Criteria
        ↓
Email Contains Attachment?
        ↓
Apply to Each Attachment
        ↓
Create File in SharePoint
```

---

# ☁️ Flow Type

Unlike Scheduled Flows, this is an **Event-Driven Flow**.

The flow executes immediately whenever the trigger conditions are met.

No manual intervention is required.

---

# 🔑 Key Concepts Learned

## 1️⃣ Automated Trigger

Trigger:

```
When a new email arrives (V3)
```

This trigger continuously monitors a mailbox for incoming emails.

Unlike scheduled flows, it only runs when an email is received.

---

## 2️⃣ Filtering Emails

Rather than processing every email, filters can be applied.

Examples include:

- Sender
- Subject
- Importance
- Folder
- Attachments

Example:

```
From:
finance@contoso.com

Subject:
Daily Report

Has Attachment:
Yes
```

Only emails matching these criteria trigger the flow.

---

## 3️⃣ SharePoint Integration

Power Automate can automatically save attachments into SharePoint.

Action:

```
Create File
```

Destination:

```
SharePoint Document Library
```

Benefits include:

- Centralised document storage
- Version control
- Team collaboration
- Reduced manual uploads

---

## 4️⃣ Dynamic Content

Instead of manually entering values, the flow uses Dynamic Content.

Examples:

```
Attachment Name

Attachment Content

Subject

Received Time

Sender
```

Dynamic Content makes flows reusable and adaptable.

---

## 5️⃣ Apply to Each

If an email contains multiple attachments, Power Automate automatically wraps the **Create File** action inside an **Apply to each** loop.

Example:

Email contains:

```
Invoice.pdf

Report.xlsx

Photo.jpg
```

Flow executes:

```
Create Invoice.pdf

↓

Create Report.xlsx

↓

Create Photo.jpg
```

Each attachment is processed individually.

---

# 💼 Real-World Business Scenarios

## Finance

Automatically save:

- Supplier invoices
- Purchase orders
- Receipts

into SharePoint.

---

## HR

Automatically store:

- CVs
- Employment contracts
- References

inside employee document libraries.

---

## Service Desk

Automatically archive:

- Log files
- Screenshots
- Diagnostic reports

received via email.

---

## Legal

Automatically save:

- Signed agreements
- Contracts
- Compliance documents

into secure SharePoint libraries.

---

## Project Management

Automatically archive:

- Weekly reports
- Project updates
- Risk registers

without manual intervention.

---

# 💼 Real-World Applications (My Experience)

This automation pattern could support many of the business processes I work with, including:

- Automatically saving supplier documents.
- Archiving approval attachments.
- Capturing audit evidence.
- Saving onboarding documents.
- Storing completed forms.
- Processing emailed reports.
- Supporting governance and compliance requirements.

---

# ⭐ Key Takeaways

✔ Automated flows respond immediately to business events.

✔ Email filters improve efficiency by processing only relevant messages.

✔ SharePoint is an excellent destination for document storage.

✔ Dynamic Content allows reusable automation.

✔ Apply to each is automatically created when multiple attachments exist.

---

# 🚨 Important Points (Never Forget)

## Avoid Triggering on Every Email

Always apply filters where possible.

Instead of:

```
Every Email
```

Use:

- Sender
- Subject
- Folder
- Importance

This reduces unnecessary flow executions.

---

## Store Documents Centrally

Rather than leaving attachments in individual mailboxes,

store them in:

- SharePoint
- OneDrive
- Document Libraries

This improves collaboration and governance.

---

## Understand Dynamic Content

Never hardcode:

```
Invoice.pdf
```

Instead use:

```
Attachment Name
```

This allows every attachment to be handled correctly.

---

## Apply to Each is Normal

Many beginners try to remove the loop.

Don't.

Whenever multiple records exist:

- Attachments
- Excel Rows
- SharePoint Items

Power Automate processes each individually.

---

## Test Different Scenarios

Always test:

- One attachment
- Multiple attachments
- No attachment
- Incorrect sender
- Incorrect subject

---

# ⚠️ Common Mistakes

❌ Not filtering emails.

❌ Saving duplicate files.

❌ Ignoring filename conflicts.

❌ Hardcoding attachment names.

❌ Forgetting Apply to Each.

❌ Assuming every email contains attachments.

---

# 🛠 Problems This Module Helps Solve

- Manual document filing.
- Lost email attachments.
- Shared mailbox management.
- Compliance archiving.
- Invoice processing.
- HR document storage.
- Project documentation.
- Audit evidence collection.

---

# 🏆 Best Practices

✅ Use specific trigger conditions.

✅ Store documents in SharePoint.

✅ Use Dynamic Content.

✅ Handle multiple attachments.

✅ Test duplicate file scenarios.

✅ Consider error handling.

✅ Keep document libraries organised.

---

# 🚀 Engineering Tip

When designing an email automation, ask:

> **"Should every email trigger this flow?"**

If the answer is **No**, add filters.

The more specific the trigger, the more reliable and efficient the automation.

---

# 🎓 How I Would Apply This in My Organisation

Potential use cases include:

- Automatically saving emailed supplier invoices to SharePoint.
- Archiving onboarding documentation received by email.
- Storing approval attachments for audit purposes.
- Processing reports submitted via email.
- Capturing screenshots and logs sent to the Service Desk.
- Automatically organising shared mailbox attachments.
- Supporting document retention and governance policies.

---

# 💭 Reflection

This module demonstrated how event-driven automation can remove repetitive administrative work by automatically processing incoming emails and storing attachments in SharePoint.

The biggest lesson from this module is that good automation starts with a well-designed trigger. By applying the correct email filters and using Dynamic Content, organisations can build reliable, scalable document management solutions that improve efficiency, consistency, and compliance.
