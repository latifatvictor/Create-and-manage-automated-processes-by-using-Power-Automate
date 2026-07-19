# 📘 Module 13 - Build a Flow That Accepts User Input When Run

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 3 minutes

---

# 📖 Overview

In this exercise, I learned how to customise an instant cloud flow so that the person running it can provide information at runtime.

Instead of using a fixed value, the flow asks the user for input when it starts and then uses that value in later actions.

The exercise began with a reminder template and replaced the fixed delay with a number entered by the user.

This created a reusable instant flow that can send a reminder after a user-defined number of minutes.

The core pattern is:

```text
User Runs Flow
      ↓
Flow Requests Input
      ↓
User Enters a Value
      ↓
Flow Uses the Value
      ↓
Action Completes
```

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Create or customise an instant cloud flow.
- Add user-input fields to a manual trigger.
- Configure a Number input.
- Use trigger input as dynamic content.
- Replace a hardcoded value with a runtime value.
- Run an instant flow from Power Automate mobile.
- Troubleshoot mobile notification issues.
- Identify suitable business scenarios for user-input flows.

---

# ⚡ What Is Runtime User Input?

Runtime input is information supplied by the user when the flow is started.

The value is not permanently fixed inside the flow.

Example:

```text
How many minutes before the reminder?
```

The user can enter:

```text
1
10
30
60
```

The same flow then behaves differently based on the selected value.

---

# 🏗️ Solution Architecture

```text
User Selects Instant Flow
          ↓
Manual Trigger Opens
          ↓
User Enters Reminder Time
          ↓
Delay Uses Entered Number
          ↓
Reminder Notification Is Created
          ↓
User Receives Notification
```

---

# 🔑 Key Concepts Learned

## 1️⃣ Manual Trigger

The instant flow uses:

```text
Manually trigger a flow
```

This trigger allows the flow designer to define fields that users must complete before the flow starts.

---

## 2️⃣ Trigger Inputs

Inputs can be added directly to the manual trigger.

Examples include:

- Text
- Yes/No
- File
- Email
- Number
- Date
- Choice

These values become available as dynamic content throughout the flow.

---

## 3️⃣ Number Input

The exercise added a Number input named:

```text
Time
```

Its user-facing instruction was:

```text
Enter time
```

The value represents how many minutes the flow should wait before sending the reminder.

---

## 4️⃣ Dynamic Content

The Time input is passed from the trigger into the Delay action.

Instead of:

```text
Delay Count = 10
```

the flow uses:

```text
Delay Count = Time
```

This changes the flow from fixed behaviour to user-controlled behaviour.

---

## 5️⃣ Delay Action

The Delay action pauses the flow for a specified period.

Basic configuration:

| Property | Value |
|---|---|
| Count | Time input |
| Unit | Minute |

Example:

```text
Time = 5
```

Result:

```text
Wait 5 minutes
```

---

# 🛠️ Flow Design

## Original Template

```text
Manual Trigger
      ↓
Delay for 10 Minutes
      ↓
Send Reminder
```

The delay was hardcoded.

---

## Customised Flow

```text
Manual Trigger
      ↓
Ask User for Time
      ↓
Delay for Entered Time
      ↓
Send Reminder
```

The revised version is more flexible because the same flow supports different reminder periods.

---

# 📋 Trigger Configuration

Example trigger:

```text
Manually trigger a flow
```

Input:

| Setting | Value |
|---|---|
| Type | Number |
| Name | Time |
| Description | Enter time |

This input appears when the user starts the flow.

---

# ⚙️ Delay Configuration

The original Count value is removed and replaced with the Time dynamic content.

```text
Count: Time
Unit: Minute
```

The Delay action now depends on the value supplied at runtime.

---

# 📱 Running the Flow

The flow can be started through Power Automate mobile.

Typical sequence:

```text
Open Power Automate Mobile
          ↓
Confirm Correct Environment
          ↓
Select Instant Flows
          ↓
Choose Reminder Flow
          ↓
Enter Time
          ↓
Select Run Flow
          ↓
Receive Notification
```

Example test:

```text
Time = 1
```

Expected outcome:

```text
Reminder received after approximately one minute
```

---

# 📲 Mobile Notification Requirements

For the reminder to appear, the device must allow Power Automate notifications.

Check:

- Power Automate is installed.
- The user is signed in.
- The correct environment is selected.
- App notifications are enabled.
- Background activity is permitted where required.
- Focus or Do Not Disturb settings are not suppressing alerts.

A successful flow run does not always guarantee that the device displays the notification visibly.

---

# 💼 Real-World Business Scenarios

## Personal Follow-Up Reminder

A user starts the flow and enters:

- Number of minutes
- Reminder text
- Related task
- Priority

Example:

```text
Remind me in 30 minutes to contact the supplier.
```

---

## Service Desk Follow-Up

An analyst starts a reminder after speaking with a user.

Inputs could include:

- Ticket reference
- Follow-up time
- User name
- Follow-up action

```text
Run Flow
   ↓
Enter Ticket Number
   ↓
Enter Delay
   ↓
Receive Follow-Up Reminder
```

---

## Meeting Preparation

A user creates a reminder before an upcoming meeting.

Inputs:

- Meeting name
- Preparation task
- Reminder time
- Notes

---

## Temporary Access Review

An administrator grants temporary access and starts a reminder flow.

Inputs:

- User email
- Access type
- Review time
- Request reference

```text
Temporary Access Granted
          ↓
Start Reminder Flow
          ↓
Enter Review Period
          ↓
Reminder Issued
          ↓
Access Reviewed
```

---

## Equipment Collection

A support analyst schedules a reminder to:

- Contact a leaver
- Collect a device
- Check delivery status
- Follow up with a site contact

---

## Approval Follow-Up

A requestor or support analyst starts a reminder to check an outstanding approval after a selected period.

```text
Enter Approval Reference
          ↓
Enter Follow-Up Time
          ↓
Wait
          ↓
Send Reminder
```

---

# 💼 Real-Life Work Applications

## ServiceNow Ticket Management

An instant flow could help analysts create a follow-up reminder while working on a ticket.

Runtime inputs might include:

- ServiceNow ticket number
- Follow-up delay
- User name
- Next action
- Priority

Example:

```text
Ticket Reviewed
      ↓
Run Follow-Up Flow
      ↓
Enter 60 Minutes
      ↓
Receive Reminder
      ↓
Update Ticket
```

---

## Joiner, Mover and Leaver Checks

A user could start a reminder for a later validation step.

Examples:

- Recheck licence removal.
- Confirm mailbox conversion.
- Verify account disablement.
- Confirm device return.
- Review group membership removal.

---

## Licence Governance

A reminder flow could be used for accounts that require temporary licence retention.

Inputs:

- Account email
- Licence type
- Review period
- Business justification
- Request reference

This reduces the risk of temporary exceptions being forgotten.

---

## Approval Workflow Testing

During testing, a developer could enter how long to wait before checking:

- Approval delivery
- Reminder behaviour
- Escalation
- Timeout logic
- SharePoint updates

---

## Maternity Handover Activities

A handover coordinator could use a simple input-driven flow to create short-term reminders for:

- Training sessions
- Document reviews
- Access checks
- Outstanding process actions
- Handover deadlines

---

# ⭐ Key Takeaways

- Instant flows can collect user input when they run.
- Trigger inputs become dynamic content.
- User input removes the need for fixed values.
- The same flow can support multiple scenarios.
- Input type should match the expected data.
- Runtime values should be validated.
- Mobile app settings can affect notification delivery.
- Templates are starting points and should be adapted carefully.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Use the Correct Input Type

A reminder period should use a Number input rather than Text.

Correct:

```text
Number
```

Less suitable:

```text
Text
```

Using the correct type reduces conversion errors and improves the user experience.

---

## 2. Validate the Value

A Number input can still contain an unsuitable value.

Examples:

```text
0
-5
999999
```

Production flows should validate that the number falls within an acceptable range.

Example rule:

```text
Time must be greater than 0
AND
Time must be less than or equal to 1,440
```

---

## 3. Make the Unit Clear

The input label should tell the user whether the value represents:

- Seconds
- Minutes
- Hours
- Days

Avoid an unclear field such as:

```text
Time
```

A better label is:

```text
Reminder time in minutes
```

This prevents users from entering `2` while expecting two hours.

---

## 4. Delay Actions Keep the Flow Run Active

A Delay action pauses the current flow run.

For short personal reminders, this may be acceptable.

For long waits or high-volume business solutions, keeping many flow runs waiting may not be the best design.

Consider alternatives such as:

- Delay until
- Scheduled flows
- Dataverse records with due dates
- SharePoint reminder queues
- Planner or Outlook tasks
- Separate reminder processes

---

## 5. Runtime Input Should Not Replace Governance

Allowing users to enter values does not mean they should control every part of the process.

Avoid letting users freely enter sensitive configuration such as:

- Administrator addresses
- Production URLs
- Security group names
- Licence identifiers
- Privileged actions

Constrain inputs where possible.

---

## 6. Use Choice Inputs Where Options Are Known

Where the valid values are predetermined, a Choice input may be safer than free text or numbers.

Example:

```text
Remind me in:
- 10 minutes
- 30 minutes
- 1 hour
- 4 hours
```

This prevents invalid entries.

---

## 7. Dynamic Content Must Come from the Correct Trigger

When multiple values have similar names, confirm that the Delay action uses the input from:

```text
Manually trigger a flow
```

Selecting the wrong dynamic content can cause unexpected behaviour.

---

## 8. Test More Than One Value

Do not test only with `1`.

Test:

- Minimum value
- Normal value
- Maximum permitted value
- Zero
- Negative number
- Empty input
- Decimal value, where relevant
- Very large value

---

## 9. Notifications Depend on Device Settings

If the flow succeeds but no notification appears, check the device before changing the flow.

The issue may be:

- Notifications disabled
- Incorrect Power Automate account
- Wrong environment
- Battery optimisation
- Focus mode
- Background restrictions

---

## 10. Templates Still Require Review

A template may contain:

- Old connectors
- Unexpected actions
- Generic wording
- Fixed values
- Connections belonging to the wrong account
- Logic that does not match the business need

Always inspect the complete flow before using it.

---

# ⚠️ Common Mistakes

- Using Text instead of Number.
- Leaving the input name unclear.
- Not specifying the time unit.
- Allowing zero or negative values.
- Keeping the original hardcoded Count value.
- Selecting the wrong dynamic content.
- Forgetting to save the flow.
- Running the flow in the wrong environment.
- Assuming a successful run guarantees a visible notification.
- Not enabling mobile notifications.
- Using very long Delay actions unnecessarily.
- Trusting a template without reviewing it.
- Failing to test invalid input.
- Giving users too much control over sensitive actions.

---

# 🧪 Testing Checklist

Test the flow with:

- A value of 1 minute
- A standard value such as 10 minutes
- Zero
- A negative value
- A decimal number
- A large value
- Missing input
- Mobile notifications enabled
- Mobile notifications disabled
- Correct environment
- Incorrect environment
- Different user accounts
- Broken notification connection
- Broken Outlook connection
- Flow run from web
- Flow run from mobile

---

# 🏆 Best Practices

- Use clear input names.
- State the expected unit.
- Use the correct data type.
- Add descriptions or examples.
- Validate input values.
- Use Choice fields where suitable.
- Set sensible maximums and minimums.
- Rename actions clearly.
- Test on the intended device.
- Check connections before deployment.
- Avoid long-running delays at scale.
- Provide a success confirmation.
- Document the purpose and owner.
- Use Solutions for managed enterprise flows.
- Monitor failures through run history.

---

# 🧱 Recommended Production Design

The training solution uses:

```text
Manual Trigger
      ↓
Number Input
      ↓
Delay
      ↓
Notification
```

A more robust design could be:

```text
User Starts Flow
       ↓
Enter Reminder Message
       ↓
Choose Reminder Period
       ↓
Validate Input
       ↓
Calculate Due Date
       ↓
Create Reminder Record
       ↓
Scheduled Process Checks Due Records
       ↓
Send Notification
       ↓
Update Record as Completed
```

This design is more scalable because the original flow does not need to remain paused for a long period.

---

# 📋 Improved Input Design

A business-ready reminder flow could request:

| Input | Type | Purpose |
|---|---|---|
| Reminder Message | Text | Describes the task |
| Reminder Period | Choice | Controls the delay |
| Ticket Reference | Text | Links to a service request |
| Priority | Choice | Supports categorisation |
| Due Date | Date | Allows exact scheduling |
| Notify by Email | Yes/No | Selects the notification channel |
| Notes | Text | Adds supporting context |

---

# 🔐 Security and Governance Considerations

Before deploying a user-input flow, ask:

- Can the user manipulate a sensitive action?
- Is the input validated?
- Could the input be used to send data externally?
- Could a user enter another person's email?
- Is the flow running with elevated permissions?
- Does the action need approval?
- Are inputs recorded for audit?
- Should users select from a controlled list?
- Is personal or confidential information being collected?
- Who supports the flow?

Input-driven flows must be designed carefully when the flow owner's connection has more access than the user running the flow.

---

# 🚀 How I Would Improve This Solution

For a production-ready version, I would:

1. Rename the input to **Reminder time in minutes**.
2. Add a reminder-message input.
3. Validate that the number is greater than zero.
4. Set a reasonable maximum delay.
5. Use predefined choices for common reminder periods.
6. Add a ticket or task reference.
7. Store the request in SharePoint or Dataverse.
8. Add error handling.
9. Send a confirmation showing the calculated reminder time.
10. Consider a scheduled reminder architecture for long delays.
11. Record the signed-in user.
12. Test both web and mobile execution.

---

# 🧠 Engineering Design Questions

Before creating an input-driven instant flow, ask:

- Why must the user start the flow manually?
- What information must the user provide?
- Which input type is most appropriate?
- Can the value be constrained?
- Should the user choose from predefined options?
- What happens when input is missing?
- What happens when the value is invalid?
- Is the flow using the user's permissions or the owner's connection?
- Could the input cause a privileged action?
- Does the flow need an audit record?
- How long can the flow remain active?
- Would a scheduled architecture be more scalable?
- Which devices will users use?
- How will success and failure be communicated?
- Who owns and supports the flow?

---

# 💭 Reflection

This exercise demonstrated how runtime input makes an instant flow flexible and reusable.

The core design pattern is:

```text
Ask
  ↓
Validate
  ↓
Use
  ↓
Complete
```

Instead of creating separate flows for reminders after 1, 10, or 30 minutes, one flow can accept the required value at runtime.

The most important lesson is that flexibility must be balanced with control.

A strong user-input flow should:

```text
Collect the Right Data
          +
Use the Correct Input Type
          +
Validate the Value
          +
Protect Sensitive Actions
          +
Provide Clear Feedback
```

User input can make automation more useful, but enterprise-ready solutions must also consider validation, security, scalability, ownership, and support.
