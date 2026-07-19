# 📘 Module 14 - Create a Flow That Blocks Time on Your Calendar

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 5 minutes

---

# 📖 Overview

In this exercise, I learned how to create an instant cloud flow that blocks one hour in my Microsoft 365 calendar and automatically notifies my manager by email.

The flow is designed for situations where a user needs to step away from work unexpectedly and wants to update their availability quickly from a mobile device.

The solution combines:

- A manual trigger
- Outlook calendar integration
- Date and time expressions
- Microsoft 365 user profile information
- Manager lookup
- Email notification
- Power Automate mobile execution

The core pattern is:

```text
User Runs Flow
      ↓
Capture Current Timestamp
      ↓
Create One-Hour Calendar Event
      ↓
Retrieve User Profile
      ↓
Retrieve Manager
      ↓
Send Manager Notification
      ↓
Flow Completes
```

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Create an instant flow from a template.
- Create an Outlook calendar event.
- Use the trigger timestamp as an event start time.
- Use an expression to calculate an end time.
- configure the correct calendar timezone.
- Retrieve the signed-in user's profile.
- Retrieve the user's manager dynamically.
- Send an email to the manager.
- Make manual-trigger inputs optional.
- Run an instant flow from Power Automate mobile.

---

# 🏗️ Solution Architecture

```text
User Selects Instant Flow
           ↓
Manual Trigger Runs
           ↓
Current Timestamp Retrieved
           ↓
Calendar Event Created
Start = Current Time
End = Current Time + 1 Hour
           ↓
Get My Profile
           ↓
Get My Manager
           ↓
Send Notification Email
           ↓
Calendar Is Blocked
```

---

# 💼 Business Scenario

The user is unexpectedly unavailable for one hour.

Instead of manually opening Outlook, creating an event, finding their manager's email address, and sending a separate message, the user starts one Power Automate flow.

The flow then:

1. Creates a one-hour calendar event.
2. Marks the user as unavailable.
3. Looks up the user's manager.
4. Sends the manager an email notification.

This reduces repetitive administration and provides a fast mobile self-service option.

---

# 🔑 Key Concepts Learned

## 1️⃣ Instant Cloud Flow

The flow uses a manual trigger.

```text
Manually trigger a flow
```

This allows the user to run the automation when needed through:

- Power Automate mobile
- Power Automate web
- Other supported Microsoft 365 entry points

---

## 2️⃣ Trigger Timestamp

The trigger provides a timestamp representing the time at which the user starts the flow.

This value is used as the calendar event's start time.

```text
Start Time = Trigger Timestamp
```

Because the value is captured at runtime, the event begins from the time the flow is executed.

---

## 3️⃣ Expressions

The event must finish one hour after it starts.

The following expression adds one hour to the trigger timestamp:

```text
addHours(
    triggerOutputs()['headers']['x-ms-user-timestamp'],
    1
)
```

The logic is:

```text
Current Trigger Time
        +
      1 Hour
        =
Calendar Event End Time
```

---

## 4️⃣ Dynamic Content

The flow uses dynamic content to pass data between actions.

Examples include:

- Timestamp from the trigger
- User Principal Name from Get my profile
- Manager email from Get manager
- Optional message from the manual trigger

Dynamic content allows the flow to work for different users without hardcoding their identities.

---

## 5️⃣ User Profile Lookup

The action:

```text
Get my profile (V2)
```

retrieves information about the person running the flow.

Useful values include:

- Display name
- User Principal Name
- Email
- Department
- Job title

In this exercise, the User Principal Name is passed into the manager lookup action.

---

## 6️⃣ Manager Lookup

The action:

```text
Get manager (V2)
```

uses the signed-in user's User Principal Name to retrieve their manager from Microsoft Entra ID.

```text
Signed-In User
      ↓
User Principal Name
      ↓
Manager Lookup
      ↓
Manager Email
```

The flow can therefore notify each user's own manager dynamically.

---

# 🛠️ Main Flow Components

## Step 1: Manual Trigger

```text
Manually trigger a flow
```

The trigger begins the process.

The original template may include a text input. This input can be:

- Used in the notification
- Made optional
- Deleted if unnecessary

---

## Step 2: Create Event

The Outlook action creates an event in the selected calendar.

Example configuration:

| Field | Value |
|---|---|
| Calendar ID | Calendar |
| Subject | Away from work |
| Start Time | Trigger Timestamp |
| End Time | Trigger Timestamp + 1 hour |
| Time Zone | User's correct timezone |
| Show As | Busy or Out of Office |

---

## Step 3: Get My Profile

```text
Office 365 Users - Get my profile (V2)
```

This identifies the person running the flow.

The action provides the User Principal Name needed for the next step.

---

## Step 4: Get Manager

```text
Office 365 Users - Get manager (V2)
```

Configuration:

```text
User (UPN) = User Principal Name
```

This retrieves the manager assigned to the user in Microsoft Entra ID.

---

## Step 5: Send Email

```text
Office 365 Outlook - Send an email (V2)
```

The recipient is:

```text
Mail from Get manager (V2)
```

Example subject:

```text
Temporary unavailability notification
```

Example body:

```text
Hello,

I am unexpectedly unavailable for approximately one hour.

I have blocked the time in my calendar and will return as soon as possible.

Kind regards
```

---

# 🕒 Date and Time Expression

The key expression in the flow is:

```text
addHours(triggerOutputs()['headers']['x-ms-user-timestamp'],1)
```

## Expression Breakdown

```text
triggerOutputs()
```

Returns information from the manual trigger.

```text
['headers']
```

Accesses the trigger's header values.

```text
['x-ms-user-timestamp']
```

Retrieves the timestamp associated with the user running the flow.

```text
addHours(..., 1)
```

Adds one hour to the timestamp.

---

# 🌍 Timezone Configuration

The calendar event must use the correct timezone.

If the timezone is incorrect:

- The event may appear at the wrong time.
- The event may start in the past or future.
- The one-hour block may not match the user's actual availability.
- Daylight-saving changes may create unexpected results.

For a UK-based user, the selected timezone should reflect the appropriate Microsoft timezone setting for the United Kingdom.

The flow should be tested during both:

- Greenwich Mean Time
- British Summer Time

---

# 📅 Calendar Availability

The event should normally set the user as:

```text
Busy
```

or:

```text
Out of Office
```

The choice depends on the purpose.

## Busy

Use when the user is temporarily occupied but may still be contactable.

## Out of Office

Use when the user is unavailable and should not be expected to respond.

The event status affects how colleagues see the user in:

- Outlook Scheduling Assistant
- Microsoft Teams
- Calendar availability
- Meeting scheduling

---

# 📱 Running the Flow from Mobile

The flow can be triggered through Power Automate mobile.

```text
Open Power Automate Mobile
          ↓
Select Correct Environment
          ↓
Open Instant Flows
          ↓
Select Calendar Blocking Flow
          ↓
Select Run Flow
          ↓
Calendar Event Created
          ↓
Manager Notified
```

If the flow does not appear:

- Refresh the list.
- Pull down to reload.
- Confirm the correct environment.
- Confirm the flow is enabled.
- Check that the signed-in account owns or can run the flow.

---

# 💼 Real-World Business Scenarios

## Unexpected Personal Emergency

A user needs to leave their workstation unexpectedly.

The flow can:

- Block their calendar.
- Notify their manager.
- Set their status to unavailable.
- Record the time they left.

---

## School or Childcare Emergency

A working parent needs to step away for an unplanned childcare issue.

The flow reduces the time needed to update availability and inform management.

---

## Medical Appointment Overrun

An appointment takes longer than expected.

The user can quickly block additional calendar time and notify their manager from a mobile device.

---

## Travel Delay

An employee is delayed while travelling between sites.

The flow can block time and inform the relevant manager.

---

## Temporary Technical Issue

A user experiences:

- Internet failure
- Laptop issue
- Power outage
- Device failure

They can run the flow from a mobile device to update their availability.

---

## Focus Time

The same architecture could be adapted to create:

- One-hour focus blocks
- Lunch breaks
- Training time
- Documentation time
- Project work sessions
- No-meeting periods

---

# 💼 Real-Life Work Applications

## Service Delivery Focus Time

The flow could allow analysts to reserve time for:

- Ticket backlog reduction
- Documentation
- Training
- Root-cause investigation
- Licence reviews
- Process improvement

Runtime inputs could include:

- Duration
- Reason
- Availability status
- Whether the manager should be notified

---

## Maternity Handover Preparation

A customised version could block calendar time for:

- Handover documentation
- JML training
- Licence-management training
- Automation walkthroughs
- Knowledge-transfer sessions
- Process recording

---

## Incident Response

An engineer starting work on a high-priority incident could run a flow that:

- Blocks their calendar.
- Sets the event subject to the incident reference.
- Notifies their manager.
- Posts a message to an incident channel.
- Records the start time.

---

## Site Visit Travel

A flow could block travel time automatically when an approved site visit begins.

```text
Run Travel Flow
      ↓
Enter Travel Duration
      ↓
Block Calendar
      ↓
Notify Manager
      ↓
Update Visit Record
```

---

## Training and Certification

A user could select a predefined duration and create a protected learning block for:

- Microsoft Learn
- Applied Skills
- Certification preparation
- Internal training
- Technical labs

---

# ⭐ Key Takeaways

- Instant flows can create calendar events on demand.
- Trigger timestamps can represent the current execution time.
- Expressions can calculate new date and time values.
- Outlook calendar events require correct timezone configuration.
- The user's manager can be retrieved dynamically.
- Dynamic lookups avoid hardcoded recipient addresses.
- Power Automate mobile makes the flow available away from a work device.
- Templates provide a useful starting point but must be reviewed and customised.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. The Timezone Must Be Correct

The template may default to an unrelated timezone.

Never assume the default setting is suitable.

Check:

- User location
- Calendar timezone
- Device timezone
- Daylight-saving behaviour
- Organisation-wide settings

---

## 2. Manager Information Depends on Entra ID

The Get manager action depends on the user's manager attribute being populated correctly.

The action may fail when:

- No manager is assigned.
- The manager account is disabled.
- The manager object cannot be accessed.
- The user is a service account.
- Directory data is incomplete.

Production flows need a fallback path.

---

## 3. Avoid Hardcoding Manager Addresses

Dynamic manager lookup supports reuse.

Hardcoding a manager email means the flow may send notifications to the wrong person after an organisational change.

---

## 4. Use the Correct Event Status

Creating an event does not automatically guarantee that the user's availability is represented correctly.

Check:

- Show As
- Busy
- Free
- Tentative
- Out of Office

The selected status should match the business scenario.

---

## 5. The Flow Creates an Event Immediately

Every time the flow runs, a new calendar event is created.

Repeated taps may create duplicate events.

Consider adding:

- Confirmation before execution
- Duplicate detection
- A unique reference
- A check for an existing overlapping event

---

## 6. The Default One-Hour Duration May Not Suit Every Situation

The training flow always blocks one hour.

A production version should consider runtime input such as:

```text
Duration:
- 30 minutes
- 1 hour
- 2 hours
- Rest of day
```

---

## 7. The User Needs Permission to Create Events

The Outlook connection must have access to the selected calendar.

The flow may fail if:

- The connection has expired.
- The mailbox is disabled.
- The selected calendar is unavailable.
- The account lacks permission.
- The connection belongs to a different user.

---

## 8. Manager Notification May Contain Personal Information

The email should include only the necessary information.

The user should not be required to disclose private medical or family details.

A suitable message may simply state:

```text
I am unexpectedly unavailable for approximately one hour.
```

---

## 9. Personal Availability Is Not the Same as Formal Leave

This flow blocks calendar time and sends a notification.

It does not replace:

- Annual-leave requests
- Sickness reporting
- HR absence procedures
- Emergency-leave processes
- Time recording
- Manager approval

The flow should be used only within the organisation's established policies.

---

## 10. Templates Must Be Fully Reviewed

Before using a template, inspect:

- Trigger inputs
- Calendar selection
- Timezone
- Start and end times
- Connections
- Event subject
- Event status
- Notification recipient
- Email wording

---

# ⚠️ Common Mistakes

- Leaving the default timezone unchanged.
- Using the wrong calendar.
- Leaving a fixed Date value in the Start Time field.
- Using the same timestamp for both start and end.
- Typing the expression into the wrong field.
- Forgetting to add one hour to the end time.
- Selecting the wrong dynamic content.
- Hardcoding the manager's address.
- Not handling users without managers.
- Creating the event as Free instead of Busy.
- Forgetting to save the flow.
- Running the flow multiple times accidentally.
- Sending excessive personal detail in the manager email.
- Assuming calendar blocking replaces formal absence reporting.

---

# 🧪 Testing Checklist

Test the flow for:

- Correct start time
- Correct end time
- One-hour duration
- Correct timezone
- Daylight-saving behaviour
- Calendar event subject
- Calendar availability status
- Manager lookup
- Manager email delivery
- User with no assigned manager
- Disabled manager account
- Broken Outlook connection
- Broken Office 365 Users connection
- Flow run from web
- Flow run from mobile
- Multiple consecutive runs
- Optional trigger field left blank
- Notification while device is offline

---

# 🏆 Best Practices

- Select the correct calendar explicitly.
- Use the trigger timestamp dynamically.
- Calculate the end time with an expression.
- Configure the correct timezone.
- Set the appropriate availability status.
- Use dynamic manager lookup.
- Add a fallback recipient.
- Keep the notification concise.
- Allow users to select the duration.
- Prevent duplicate calendar events.
- Add error handling.
- Rename actions clearly.
- Test through the mobile app.
- Document that the flow does not replace formal absence procedures.
- Store enterprise flows inside Solutions.

---

# 🧱 Recommended Production Design

The training solution uses:

```text
Manual Trigger
      ↓
Create One-Hour Event
      ↓
Get User Profile
      ↓
Get Manager
      ↓
Send Email
```

A stronger production design could be:

```text
User Starts Flow
       ↓
Select Duration
       ↓
Select Availability Type
       ↓
Enter Optional Short Message
       ↓
Validate Inputs
       ↓
Check for Existing Calendar Block
       ↓
Create Calendar Event
       ↓
Retrieve Manager
       ↓
Manager Found?
    /            \
  Yes             No
   ↓               ↓
Notify Manager   Notify Fallback Contact
       \          /
        \        /
     Send Confirmation to User
              ↓
         Record Flow Result
```

---

# 📋 Improved Runtime Inputs

| Input | Type | Purpose |
|---|---|---|
| Duration | Choice | Determines calendar block length |
| Availability Status | Choice | Busy or Out of Office |
| Reason Category | Choice | Personal, technical issue, travel, focus time |
| Short Message | Text | Optional context |
| Notify Manager | Yes/No | Controls notification |
| Return Time | Date and Time | Alternative to a duration |
| Related Reference | Text | Incident, ticket, or request number |

---

# 🛡️ Error-Handling Design

A production version should include Scopes.

```text
Scope - Try
    ↓
Create Event
    ↓
Retrieve Manager
    ↓
Send Notification
```

```text
Scope - Catch
    ↓
Capture Error
    ↓
Notify User
    ↓
Log Failure
```

```text
Scope - Finally
    ↓
Record Completion Status
```

Possible failures include:

- Calendar unavailable
- Manager missing
- Connection expired
- Invalid timestamp
- Mail action failure
- Duplicate event
- Permission issue

---

# 🔄 Handling a Missing Manager

Recommended logic:

```text
Get Manager
     ↓
Manager Email Available?
    /                 \
  Yes                  No
   ↓                    ↓
Send to Manager      Send to Team Mailbox
```

Possible fallback recipients include:

- Service Delivery shared mailbox
- HR contact
- Department mailbox
- Configured support address
- A manually selected recipient

The fallback should be agreed with the business.

---

# 🕐 Improved Duration Expression

For a user-provided number of hours:

```text
addHours(
    triggerOutputs()['headers']['x-ms-user-timestamp'],
    int(triggerBody()?['Duration'])
)
```

For minutes:

```text
addMinutes(
    triggerOutputs()['headers']['x-ms-user-timestamp'],
    int(triggerBody()?['DurationInMinutes'])
)
```

The exact property name depends on the trigger input's internal name.

---

# 📊 Suggested Audit Fields

Where logging is required, a SharePoint list or Dataverse table could contain:

| Field | Purpose |
|---|---|
| User Name | Identifies who ran the flow |
| User Email | Stores organisational identity |
| Start Time | Calendar block start |
| End Time | Calendar block end |
| Duration | Records selected length |
| Availability Type | Busy or Out of Office |
| Manager | Records notification recipient |
| Notification Sent | Yes or No |
| Calendar Event ID | Supports later updates or cancellation |
| Flow Run ID | Supports troubleshooting |
| Status | Completed, partially completed, failed |
| Error Details | Stores technical failure information |

---

# 🚀 How I Would Improve This Solution

For organisational use, I would:

1. Allow the user to choose the duration.
2. Allow Busy or Out of Office selection.
3. Add a simple reason category.
4. Make personal details optional.
5. Handle users with no manager configured.
6. Add a fallback notification address.
7. Check for duplicate or overlapping events.
8. Store the created event ID.
9. Add error handling.
10. Send a confirmation to the user.
11. Include a link to the created event.
12. Place the flow inside a Solution.
13. Document that it does not replace formal absence reporting.
14. Test across timezones and daylight-saving periods.

---

# 🧠 Engineering Design Questions

Before building a calendar-blocking flow, ask:

- Who will run the flow?
- What should trigger it?
- How long should the calendar be blocked?
- Should the duration be fixed or user-selected?
- Should the event show as Busy or Out of Office?
- Which calendar should be updated?
- Is manager data reliable in Entra ID?
- What happens if no manager is found?
- Should the manager always be notified?
- What personal information is appropriate to include?
- Could the flow create duplicate events?
- Should the user be able to cancel or extend the block?
- Does the process need an audit record?
- Does it comply with HR absence procedures?
- Which timezone should be used?
- Who owns and supports the flow?
- How will failures be monitored?

---

# 💭 Reflection

This exercise demonstrated how a simple instant flow can combine calendar automation, directory data, date expressions, and email notification into one useful mobile process.

The core technical pattern is:

```text
Capture Current Time
        ↓
Calculate End Time
        ↓
Create Calendar Event
        ↓
Retrieve Organisational Relationship
        ↓
Send Notification
```

The exercise also reinforced several important engineering principles:

```text
Dynamic Data
      +
Correct Timezone
      +
Reliable Directory Information
      +
Clear Communication
      +
Error Handling
```

The template provides a useful starting point, but an enterprise-ready version should also consider variable durations, duplicate prevention, missing-manager handling, privacy, HR policy, auditability, and long-term support.
