# 📘 Module 18 - Monitor Flows

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 5 minutes

---

# 📖 Overview

Building an automation is only the first step.

In a production environment, a flow must also be **monitored**, **supported**, and **maintained** to ensure it continues to deliver value.

Power Automate provides monitoring capabilities that allow administrators and developers to:

- View run history
- Identify failed executions
- Investigate errors
- Measure execution times
- Analyse performance
- Troubleshoot issues
- Confirm successful processing

Monitoring is one of the most important responsibilities of a Modern Workplace Engineer because even the best-designed automation can fail due to changes in connectors, permissions, external systems, or business data.

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Monitor cloud flow executions.
- View flow run history.
- Identify successful and failed runs.
- Investigate individual flow actions.
- Analyse execution times.
- Review flow notifications.
- Troubleshoot failed actions.
- Understand the importance of operational monitoring.
- Apply monitoring best practices in enterprise environments.

---

# 🏗️ Flow Monitoring Architecture

```text
Flow Executes
      │
      ▼
Power Automate Logs Run
      │
      ▼
Run History
      │
      ▼
Developer / Administrator
      │
      ▼
Review Results
      │
      ├──────────────┐
      ▼              ▼
 Success         Failure
      │              │
      ▼              ▼
 Close      Investigate & Fix
```

Monitoring is an ongoing operational activity rather than a one-time task.

---

# 🔄 Why Monitoring Matters

A flow may fail even when:

- The logic is correct.
- The automation worked yesterday.
- No changes were made to the flow.

Failures may occur because:

- Passwords expire.
- Connections expire.
- Permissions change.
- SharePoint lists change.
- SQL tables change.
- APIs become unavailable.
- Microsoft services experience temporary outages.
- Users enter unexpected data.

Monitoring helps detect these issues quickly before they impact business users.

---

# 📱 Power Automate Mobile Monitoring

The Power Automate mobile app allows administrators and makers to review flows from anywhere.

Typical workflow:

```text
Open Mobile App
        ↓
Flows
        ↓
Select Flow
        ↓
Run History
        ↓
Review Execution
```

This enables support engineers to investigate issues without needing access to a desktop computer.

---

# 🔔 Notifications

Power Automate provides notifications for important events.

Examples include:

- Failed flows
- Connection issues
- Approval notifications
- Trigger failures
- Action failures

The Notification Centre can be accessed using:

```text
Bell Icon
```

Notifications help identify problems before users report them.

---

# 📊 Flow Summary

Each flow provides a summary showing:

- Successful runs
- Failed runs
- Today's activity
- Yesterday's activity
- Historical runs

This gives an immediate indication of the flow's health.

Example:

```text
Today

Successful: 25

Failed: 2
```

A sudden increase in failures often indicates a new issue requiring investigation.

---

# 📜 Run History

Every execution of a flow is stored in its run history.

Example:

```text
Run 1
Successful

Run 2
Successful

Run 3
Failed

Run 4
Successful
```

Selecting a run opens the detailed execution information.

---

# 🔍 Run Details

The run details page provides information for every action.

Typical information includes:

- Action name
- Status
- Start time
- Finish time
- Duration
- Inputs
- Outputs
- Error messages

Example:

```text
Trigger
✔ Success

Get Items
✔ Success

Condition
✔ Success

Send Email
❌ Failed
```

Each action can be expanded to inspect its execution.

---

# ⏱️ Execution Time

Each action records how long it took to execute.

Example:

| Action | Duration |
|---------|----------|
| Trigger | 0.2 sec |
| Get Items | 1.5 sec |
| Condition | 0.1 sec |
| Send Email | 2.3 sec |

Long execution times may indicate:

- Network latency
- Slow APIs
- Large datasets
- Connector throttling
- Performance bottlenecks

Monitoring duration helps optimise flows over time.

---

# ✅ Successful Actions

Successful actions display:

```text
✔
```

A successful action indicates that:

- The action completed.
- Required outputs were produced.
- The next action continued.

However, a successful action does not always mean the business outcome was correct.

Example:

```text
Email Sent ✔

Sent to Wrong Person ❌
```

Always validate business results, not just technical success.

---

# ❌ Failed Actions

Failed actions display:

```text
❌
```

Expanding the action typically reveals:

- Error code
- Error message
- HTTP status
- Connector response
- Request details
- Input values

These details are essential for troubleshooting.

---

# 🔍 Common Failure Categories

## Authentication

Examples:

- Expired credentials
- Revoked access
- Incorrect password
- Expired OAuth token

---

## Permissions

Examples:

- Missing SharePoint permissions
- SQL access denied
- Planner permissions removed
- Mailbox access revoked

---

## Data Errors

Examples:

- Required field missing
- Invalid email address
- Invalid date
- Incorrect data type
- Duplicate key

---

## Connectivity

Examples:

- Gateway unavailable
- SQL offline
- Internet issue
- Microsoft service interruption

---

## Logic Errors

Examples:

- Wrong condition
- Null values
- Missing variables
- Incorrect expression
- Unexpected branch

---

# 🧩 Run Analysis Process

A structured troubleshooting process:

```text
Flow Failed
      ↓
Identify Failed Action
      ↓
Read Error Message
      ↓
Review Inputs
      ↓
Review Outputs
      ↓
Identify Root Cause
      ↓
Fix Flow
      ↓
Retest
```

Avoid changing multiple parts of a flow before identifying the actual cause.

---

# 📈 Performance Monitoring

Beyond failures, monitoring should also consider:

- Average execution time
- Peak execution time
- Flow frequency
- Success percentage
- Connector response times
- API usage
- Long-running actions

Performance trends often reveal problems before failures occur.

---

# 🧠 Operational Metrics

Useful operational metrics include:

- Success rate
- Failure rate
- Average duration
- Longest execution
- Number of daily runs
- Trigger frequency
- Retry count
- Connector failures

Example:

```text
Runs: 500

Success: 498

Failures: 2

Success Rate: 99.6%
```

---

# 🔄 Enterprise Monitoring Lifecycle

```text
Deploy Flow
      ↓
Monitor
      ↓
Identify Issues
      ↓
Investigate
      ↓
Improve
      ↓
Deploy Updated Version
      ↓
Continue Monitoring
```

Monitoring never stops after deployment.

---

# 💼 Real-World Business Scenarios

## Travel Request Solution

Monitor:

- Approval failures
- Email failures
- SharePoint updates
- Manager lookup
- CEO approval
- Notification delivery

---

## Joiner, Mover and Leaver

Monitor:

- Account creation
- Licence assignment
- Group membership
- Mailbox conversion
- Notification emails

---

## Licence Management

Monitor:

- SQL updates
- SharePoint synchronisation
- Approval outcomes
- Scheduled reviews

---

## Service Desk Automation

Monitor:

- Ticket creation
- Planner updates
- Teams notifications
- Escalations

---

## Asset Management

Monitor:

- Device requests
- Asset updates
- Manager approvals
- Inventory synchronisation

---

# 💼 Real-Life Work Applications

## Project Site Visit Solution

Monitor:

```text
Submission
      ↓
Manager Approval
      ↓
Head Approval
      ↓
SharePoint Update
      ↓
Employee Notification
```

Each stage should be reviewed if users report delays.

---

## International Travel Workflow

Monitor:

- Request submission
- Approval timing
- Notification failures
- Calendar updates
- Final decision

---

## Copilot Licence Reviews

Monitor:

- Scheduled reminders
- Survey emails
- SQL updates
- Dashboard refreshes

---

## Service Delivery Reporting

Monitor:

- Daily scheduled flows
- SQL synchronisation
- SharePoint updates
- Power BI refresh triggers

---

# ⭐ Key Takeaways

- Every flow has run history.
- Every action has execution details.
- Failed actions provide diagnostic information.
- Monitoring should continue after deployment.
- Mobile monitoring enables faster support.
- Success does not always equal business success.
- Performance should be monitored alongside failures.
- Operational monitoring improves reliability.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Successful Does Not Always Mean Correct

A flow may complete successfully while producing the wrong business result.

Example:

```text
Email Sent ✔

Wrong Recipient ❌
```

Always verify business outcomes.

---

## 2. Review Individual Actions

Do not stop after seeing:

```text
Flow Failed
```

Identify exactly:

- Which action failed.
- Why it failed.
- What inputs were received.
- What outputs were produced.

---

## 3. Connections Expire

Many production failures occur because:

- OAuth tokens expire.
- Passwords change.
- Service accounts are disabled.
- Permissions change.

Connection health should be monitored regularly.

---

## 4. Flow Owners Leave Organisations

If flows are owned by personal accounts:

```text
Employee Leaves
      ↓
Account Disabled
      ↓
Flow Stops
```

Production solutions should use:

- Service Accounts
- Connection References
- Managed Solutions

---

## 5. Long Execution Times Matter

A flow may succeed but become increasingly slow.

Investigate:

- Connector latency
- Large datasets
- Inefficient loops
- Unfiltered queries
- Nested Apply to Each actions

---

## 6. Run History Has Retention Limits

Run history is not retained forever.

Organisations needing long-term audit should consider:

- Dataverse
- Log Analytics
- Azure Monitor
- SharePoint audit logs
- Custom logging

---

## 7. Monitor Trends, Not Just Individual Failures

One failed run may be insignificant.

Ten failures after a deployment indicate a pattern.

Trend analysis is more valuable than isolated events.

---

## 8. Error Messages Are Valuable

Avoid immediately editing the flow.

First understand:

- Error code
- Connector response
- Failed action
- Request payload
- Response payload

The error usually points directly to the problem.

---

## 9. Production Flows Need Operational Ownership

Every enterprise flow should have:

- Owner
- Support team
- Monitoring process
- Escalation path
- Documentation

Automation without operational ownership becomes difficult to support.

---

## 10. Monitoring Is Part of the Solution

A flow is not complete when it is published.

It is complete when:

- Monitoring exists.
- Support procedures exist.
- Documentation exists.
- Alerts exist.
- Recovery procedures exist.

---

# ⚠️ Common Mistakes

- Only checking overall flow status.
- Ignoring successful-but-incorrect outcomes.
- Not expanding failed actions.
- Ignoring execution duration.
- Using personal accounts.
- Never reviewing run history.
- Waiting for users to report failures.
- Ignoring connector warnings.
- Not documenting recurring failures.
- Changing multiple things before troubleshooting.
- Ignoring trends.
- Not testing after fixes.
- Not enabling monitoring for production flows.

---

# 🧪 Monitoring Checklist

Review:

- Trigger status
- Action status
- Failed actions
- Duration
- Inputs
- Outputs
- Error messages
- Retry attempts
- Connector health
- Authentication
- Permissions
- Notification delivery
- Performance
- Success trends
- Failure trends
- Recent deployments

---

# 🏆 Best Practices

- Review production flows regularly.
- Monitor after deployments.
- Use service accounts.
- Document known failures.
- Investigate root causes.
- Track recurring issues.
- Optimise slow actions.
- Filter unnecessary data.
- Build error handling.
- Notify administrators of failures.
- Log important events.
- Test fixes before production.
- Review connector health.
- Maintain support documentation.
- Monitor business outcomes.

---

# 🧱 Recommended Enterprise Monitoring Architecture

```text
Power Automate Flow
        │
        ▼
Run History
        │
        ▼
Monitoring Dashboard
        │
        ├──────────────┐
        ▼              ▼
Success Logs      Failure Logs
        │              │
        ▼              ▼
Operational Review
        │
        ▼
Continuous Improvement
```

---

# 🛡️ Recommended Error-Handling Pattern

```text
Main Flow
     │
     ▼
Try Scope
     │
     ▼
Business Actions
     │
     ▼
Catch Scope
     │
     ▼
Capture Error
     │
     ▼
Notify Support
     │
     ▼
Log Failure
     │
     ▼
Finally Scope
     │
     ▼
Record Completion Status
```

---

# 📊 Suggested Monitoring Dashboard

| Metric | Purpose |
|----------|----------|
| Total Runs | Activity level |
| Successful Runs | Reliability |
| Failed Runs | Operational health |
| Success Rate | KPI |
| Average Duration | Performance |
| Slowest Action | Optimisation |
| Connector Failures | Integration health |
| Retry Count | Stability |
| Active Owners | Governance |
| Last Successful Run | Availability |

---

# 🚀 How I Would Improve Production Monitoring

For enterprise solutions, I would:

1. Create a monitoring dashboard in Power BI.
2. Log failures to Dataverse or SharePoint.
3. Send Teams alerts for critical failures.
4. Use service accounts.
5. Monitor connector health.
6. Create operational runbooks.
7. Capture Flow Run IDs.
8. Record retry attempts.
9. Track performance trends.
10. Review flows after deployments.
11. Create support ownership documentation.
12. Build automated health checks.

---

# 🧠 Engineering Design Questions

Before deploying any production flow, ask:

- Who monitors this flow?
- Who receives failure alerts?
- What happens if the flow stops?
- What recovery procedures exist?
- Which actions are most critical?
- What is the acceptable failure rate?
- What performance is acceptable?
- Are service accounts being used?
- How long is run history retained?
- Are audit logs required?
- What business KPIs depend on this flow?
- How will recurring issues be identified?
- Is there a support runbook?
- Who owns the automation after deployment?

---

# 💭 Reflection

This exercise highlighted that **building an automation is only half of the job**.

A production-quality solution must also be observable, supportable, and maintainable.

The operational lifecycle is:

```text
Design
   ↓
Build
   ↓
Test
   ↓
Deploy
   ↓
Monitor
   ↓
Improve
```

Monitoring transforms automation from a simple workflow into a reliable business service. By reviewing run history, analysing execution times, investigating failures, and monitoring trends, organisations can ensure their Power Automate solutions continue to deliver value long after they are deployed.

For a Modern Workplace Engineer, effective monitoring is just as important as designing the flow itself.
