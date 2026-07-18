# 📘 Module 6 - Troubleshoot Flows

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 8 minutes

---

# 📖 Overview

No automation is perfect.

Even well-designed Power Automate flows can fail due to authentication issues, configuration errors, service outages, connector limitations, or licensing restrictions.

A skilled Power Platform Engineer doesn't just build flows—they know how to quickly identify, diagnose, and resolve failures while minimising business disruption.

This module introduces common causes of flow failures, how to investigate them, and best practices for maintaining reliable automations.

---

# 🎯 Learning Objectives

After completing this module I can:

- Investigate failed cloud flows.
- Use Run History to diagnose issues.
- Identify authentication failures.
- Troubleshoot connector configuration problems.
- Recognise temporary Microsoft service issues.
- Understand licensing and API limitations.
- Apply troubleshooting best practices.

---

# 🏗️ Troubleshooting Workflow

```
Flow Failed
      │
      ▼
Check Run History
      │
      ▼
Identify Failed Step
      │
      ▼
Read Error Message
      │
      ▼
Determine Root Cause
      │
      ▼
Fix Issue
      │
      ▼
Resubmit Flow
      │
      ▼
Verify Success
```

---

# 🔑 Key Concepts Learned

## 1️⃣ Run History

Every cloud flow records its execution history.

Run History provides:

- Successes
- Failures
- Duration
- Inputs
- Outputs
- Error messages

This should always be your first troubleshooting stop.

---

## 2️⃣ Error Messages

Every failed action provides useful diagnostic information.

Typical information includes:

- Error Code
- Error Description
- Failed Action
- Suggested Resolution

Always investigate the first failed action, as later failures are often just a consequence of the initial problem.

---

# 🚨 Common Error Types

## 🔐 Authentication Errors

### Common Error Codes

```
401 Unauthorized

403 Forbidden
```

### Typical Causes

- Expired credentials
- Password changed
- Account disabled
- Connection revoked
- MFA changes

### Resolution

- Reauthenticate the connection.
- Update credentials.
- Verify account permissions.
- Test the connection.
- Resubmit the flow.

---

## ⚙️ Configuration Errors

### Common Error Codes

```
400 Bad Request

404 Not Found
```

### Typical Causes

- Incorrect field mapping
- Missing SharePoint column
- Renamed Excel table
- Deleted file
- Invalid path
- Missing dynamic content

### Resolution

- Edit the flow.
- Correct the configuration.
- Save the flow.
- Test again.

---

## 🌐 Temporary Service Issues

### Common Error Codes

```
500 Internal Server Error

502 Bad Gateway
```

These usually indicate temporary Microsoft service or connector issues.

### Resolution

- Wait a few minutes.
- Resubmit the flow.
- Check Microsoft 365 Service Health if widespread issues are suspected.

---

## 💳 Licensing Issues

Flows may stop working because of licensing restrictions.

Examples include:

- Incorrect Power Automate licence
- Premium connector usage without the appropriate licence
- Expired trial licence

Always verify your licence before troubleshooting complex issues.

---

## 📊 API and Usage Limits

Power Automate enforces API request limits.

If these limits are exceeded:

- Flows may be throttled.
- Runs may be delayed.
- Actions may temporarily fail.

High-volume automations should be designed with these limits in mind.

---

## ⏱️ Trigger Frequency

Some plans restrict how often flows are evaluated.

For example:

```
Free Plan

↓

Checks every 15 minutes
```

A trigger occurring more frequently may be queued rather than executed immediately.

---

# 💼 Real-World Business Scenarios

## Microsoft Forms

Problem

A new form submission doesn't trigger the flow.

Possible causes:

- Incorrect trigger
- Wrong environment
- Broken connection
- Form moved or deleted

---

## SharePoint

Problem

Flow cannot update a list item.

Possible causes:

- Column renamed
- Column deleted
- Permissions changed
- List moved

---

## Outlook

Problem

Email isn't sent.

Possible causes:

- Expired Outlook connection
- Invalid recipient
- Mailbox permission changes

---

## Excel

Problem

Rows cannot be retrieved.

Possible causes:

- File moved
- Table deleted
- Table renamed
- File locked

---

## Teams

Problem

Message isn't posted.

Possible causes:

- Deleted Team
- Deleted Channel
- Permission changes
- Connector authentication failure

---

# 💼 Real-World Applications (My Experience)

Reliable troubleshooting is just as important as building automation.

The troubleshooting techniques in this module would be valuable when supporting:

- Microsoft Forms integrations
- SharePoint approval workflows
- Service request automations
- Licence governance reporting
- Email notification workflows
- Microsoft Teams notifications
- Business approval processes
- Scheduled governance reporting

---

# ⭐ Key Takeaways

✔ Always start with Run History.

✔ Identify the **first** failed action.

✔ Read the complete error message.

✔ Understand the error code.

✔ Fix the root cause—not just the symptom.

✔ Test after every change.

---

# 🚨 Important Points (Never Forget)

## Never Guess

Do not randomly modify actions.

Instead:

```
Read Error

↓

Understand Cause

↓

Apply Fix

↓

Test Again
```

Good troubleshooting is evidence-based.

---

## The First Failure Matters Most

If Action 5 fails,

Actions 6–20 may also fail.

Focus on the **first red action**, as later failures are often a knock-on effect.

---

## Connections Are a Common Cause

Many production failures result from:

- Expired passwords
- Disabled accounts
- MFA changes
- Revoked permissions

Always verify connections early in your investigation.

---

## Test Before Returning to Users

Never assume the issue is resolved.

Always:

- Save the flow.
- Run a manual test.
- Verify expected results.
- Confirm with the requester if appropriate.

---

## Document the Root Cause

After resolving an issue, document:

- What failed.
- Why it failed.
- How it was fixed.
- How it can be prevented in future.

This builds organisational knowledge and speeds up future support.

---

# ⚠️ Common Mistakes

❌ Ignoring Run History.

❌ Only reading the last failed action.

❌ Rebuilding the flow instead of diagnosing it.

❌ Ignoring authentication issues.

❌ Testing with production data only.

❌ Not checking connector permissions.

❌ Forgetting to save after making changes.

---

# 🛠 Problems This Module Helps Solve

- Failed approvals.
- Email delivery issues.
- SharePoint update failures.
- Excel connection problems.
- Authentication failures.
- Connector outages.
- Licensing restrictions.
- API throttling.
- Scheduled flow failures.
- Trigger issues.

---

# 🏆 Best Practices

✅ Review Run History regularly.

✅ Build meaningful action names.

✅ Use descriptive error messages.

✅ Add Scope actions for grouping.

✅ Implement error handling where appropriate.

✅ Monitor production flows proactively.

✅ Document recurring issues and resolutions.

---

# 🚀 Enterprise Troubleshooting Checklist

When a production flow fails, ask:

- Did the trigger fire?
- Which action failed first?
- What is the error code?
- Has anything changed in the source system?
- Are the connections healthy?
- Does the account still have the required permissions?
- Has the data structure changed?
- Is Microsoft experiencing a service issue?
- Have API or licensing limits been reached?
- Has the fix been tested successfully?

Following this sequence helps avoid unnecessary changes and speeds up root cause analysis.

---

# 💭 Reflection

This module reinforced that troubleshooting is a core skill for any Power Platform professional. Effective support starts with understanding the evidence provided by Run History, interpreting error codes, and identifying the true root cause rather than making assumptions.

Building reliable automations is only part of the job. Maintaining, monitoring, documenting, and continuously improving those automations is what keeps business processes running successfully in production environments.
