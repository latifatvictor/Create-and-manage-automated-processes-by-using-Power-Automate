# 📘 Module 12 - Build a Flow That Uses Location or Date Information

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 7 minutes

---

# 📖 Overview

In this exercise, I learned how to build an **instant cloud flow** that uses information already available on the device running the flow.

This information is exposed through **trigger tokens**.

Trigger tokens can provide contextual data such as:

- Current date
- Current time
- User name
- User email
- City
- Country or region
- Full address
- Latitude
- Longitude
- Postal code
- State
- Street

Unlike values entered manually by a user, trigger-token values are determined automatically when the instant flow runs.

This makes it possible to build mobile and context-aware automations that reduce repetitive data entry.

---

# 🎯 Learning Objectives

After completing this exercise, I can:

- Explain what trigger tokens are.
- Build an instant cloud flow.
- Use contextual device information in flow actions.
- Add date and location information to an email.
- Run an instant flow from the Power Automate mobile app.
- Understand the permissions required to access device location.
- Troubleshoot connection-related failures.
- Identify suitable business scenarios for location-aware flows.

---

# ⚡ What Is an Instant Flow?

An instant flow is started manually by a user.

It can be launched through:

- Power Automate mobile
- Power Automate web
- A Power Apps button
- Microsoft Teams
- A manually selected flow
- Other supported Microsoft 365 experiences

Basic pattern:

```text
User Selects Run
        ↓
Instant Trigger
        ↓
Read Trigger Tokens
        ↓
Perform Actions
        ↓
Return Confirmation
```

Instant flows are useful when a person needs to start a process at a specific moment.

---

# 🔑 What Are Trigger Tokens?

Trigger tokens are contextual data values that are automatically available when an instant flow runs.

They are generated from information known by:

- The signed-in user
- The device
- The current location
- The local date and time

Example:

```text
User runs flow on mobile phone
             ↓
Device provides date and location
             ↓
Flow inserts values into an email
             ↓
Message is sent automatically
```

Trigger tokens reduce the need for users to enter information that the device already knows.

---

# 📋 Available Trigger Tokens

| Token | Description |
|---|---|
| City | City where the device is located |
| Country/Region | Country or region where the device is located |
| Full Address | Full detected address |
| Latitude | Geographic latitude |
| Longitude | Geographic longitude |
| PostalCode | Postal or ZIP code |
| State | State, county, province, or region |
| Street | Street where the device is located |
| Timestamp | Local time when the flow runs |
| Date | Local date when the flow runs |
| User Name | Name of the signed-in user |
| User Email | Email address of the signed-in user |

---

# 🏗️ Solution Architecture

The exercise used the following design:

```text
User Runs Instant Flow
           ↓
Retrieve User's Colleagues
           ↓
Apply to Each Colleague
           ↓
Create WFH Email
           ↓
Insert Date Token
           ↓
Insert Full Address Token
           ↓
Send Email
           ↓
Display Success Notification
```

---

# 💼 Scenario Built

The flow sends a message to colleagues confirming that the user is working from home.

The flow automatically includes:

- The current date
- The device's detected address

Example subject:

```text
WFH Today - 18 July 2026
```

Example body:

```text
I am working from home today.

Current location:
[Full Address]
```

The user does not need to type the date or location manually each time the flow runs.

---

# 🛠️ Main Components

## 1. Instant Trigger

The flow starts when the user manually selects it.

```text
Manually Trigger a Flow
```

The trigger makes contextual tokens available to subsequent actions.

---

## 2. User Information

The template can use the Microsoft 365 Users connector to retrieve information about colleagues or people associated with the signed-in user.

This may be used to determine who should receive the notification.

---

## 3. Apply to Each

Where the flow returns multiple recipients, Power Automate creates an:

```text
Apply to Each
```

loop.

The email action then runs once for every recipient in the collection.

---

## 4. Send an Email

The email action uses dynamic content and trigger tokens.

Example configuration:

| Field | Value |
|---|---|
| Subject | WFH Today + Date |
| Body | Default message + Full Address |
| Recipient | Colleague email from previous action |

---

## 5. Mobile Notification

After the flow completes successfully, Power Automate can display a mobile notification confirming that the message was sent.

Example:

```text
WFH email was sent successfully.
```

---

# 📱 Power Automate Mobile

The flow was edited and run using the Power Automate mobile app.

Typical workflow:

```text
Create Flow in Browser
        ↓
Save Flow
        ↓
Open Power Automate Mobile
        ↓
Select Correct Environment
        ↓
Open Flow
        ↓
Edit Trigger Tokens
        ↓
Save
        ↓
Run Flow
```

The browser version remains useful for:

- Creating flows
- Managing connections
- Viewing run history
- Troubleshooting failures
- Reviewing detailed action configuration

---

# 🌍 Location Permissions

The flow can only retrieve location information when the device permits Power Automate to access location services.

The user may need to grant:

```text
Power Automate
      ↓
Location Permission
      ↓
Allow While Using App
```

Without this permission, location tokens may:

- Be blank
- Return incomplete information
- Use an approximate location
- Cause an action to fail
- Produce inaccurate results

---

# 📅 Date and Time Behaviour

The Date and Timestamp tokens use information from the device at the moment the flow runs.

This means the values can change based on:

- Current geographic location
- Device timezone
- Daylight-saving rules
- Device time settings
- Whether the device location is available

For global or enterprise workflows, timezone handling should be considered carefully.

---

# 🔍 Date vs Timestamp

## Date

Represents the local calendar date.

Example:

```text
18 July 2026
```

## Timestamp

Represents a specific date and time.

Example:

```text
18 July 2026 09:35
```

Timestamp values are better where the exact time of the action matters.

---

# 💼 Real-World Business Scenarios

## Field Service Check-In

A field engineer starts a flow when arriving at a customer site.

```text
Run Flow
   ↓
Capture User
   ↓
Capture Timestamp
   ↓
Capture Location
   ↓
Create Visit Record
```

The record can show:

- Engineer name
- Arrival time
- Location
- Customer
- Service reference

---

## Lone Worker Check-In

A worker sends a check-in notification.

```text
Manual Check-In
      ↓
Capture Location
      ↓
Capture Date and Time
      ↓
Notify Manager
      ↓
Record Check-In
```

This can support a wider safety process, although it should not be treated as a replacement for an approved emergency or lone-worker system.

---

## Site Visit Tracking

An employee records when they arrive at a project site.

```text
Run Site Visit Flow
        ↓
Capture Location
        ↓
Capture Timestamp
        ↓
Update SharePoint
        ↓
Notify Project Team
```

---

## Travel Status Notification

A travelling employee sends an update.

```text
Run Flow
   ↓
Capture City and Country
   ↓
Send Status to Team
```

---

## Working Location Notification

An employee records whether they are working remotely, at a site, or in an office.

The flow could:

- Send a Teams message.
- Update a SharePoint list.
- Notify a manager.
- Record the date.
- Update a team attendance dashboard.

---

## Mobile Expense Recording

An employee starts a flow after incurring an expense.

The flow could capture:

- Date
- Location
- User
- Expense category
- Amount
- Receipt photograph

---

# 💼 Real-Life Work Applications

## Project Site Visit Requests

A mobile instant flow could support approved site visits by allowing an employee to record:

- Arrival date and time
- Current location
- Site visited
- Request reference
- Visit status

Example:

```text
Approved Site Visit
        ↓
Employee Arrives
        ↓
Runs Check-In Flow
        ↓
Location and Time Recorded
        ↓
SharePoint Request Updated
```

This could supplement the existing approval process with an operational attendance record.

---

## International Travel

A traveller could use a flow to provide a simple status update during an approved trip.

```text
Run Travel Check-In
        ↓
Capture City
        ↓
Capture Country
        ↓
Capture Timestamp
        ↓
Notify Travel Coordinator
```

Location collection would need to be justified, transparent, and governed appropriately.

---

## IT Site Support

An engineer visiting an office or warehouse could record:

- Technician name
- Site
- Arrival time
- Departure time
- Service request number
- Work completed

This could help document support activity without manually completing a separate timesheet.

---

## Device Collection and Delivery

An engineer could run a flow when:

- Collecting a device
- Delivering equipment
- Visiting a user
- Completing a replacement
- Attending a remote office

The flow could capture the date, user, location, and asset number.

---

## Major Incident Attendance

An on-site engineer could use an instant flow to notify the incident team that they have arrived.

Example:

```text
Engineer Arrived
      ↓
Timestamp Captured
      ↓
Site Captured
      ↓
Teams Notification Sent
      ↓
Incident Record Updated
```

---

# ⭐ Key Takeaways

- Instant flows are started manually.
- Trigger tokens provide contextual device and user information.
- Date and location values can be added without manual entry.
- Mobile flows can support field-based business processes.
- The user must grant location permission.
- Connections should be checked when the flow fails.
- Location and identity data require appropriate governance.
- Trigger tokens should enhance a process, not replace proper validation.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Location Data Is Sensitive

Location data can reveal:

- Where an employee lives
- Where they work
- Where they travel
- When they are present at a location
- Behavioural or movement patterns

Before using location tokens in a workplace solution, consider:

- Business necessity
- Data protection
- User awareness
- Consent or another valid lawful basis
- Retention period
- Access controls
- Security
- Organisational policy

Do not collect more location information than the process genuinely requires.

---

## 2. Full Address Might Be Too Precise

A process may only need:

```text
City
```

or:

```text
Site Name
```

rather than:

```text
Full Address
```

Use the least precise location token that still meets the business requirement.

---

## 3. Location Accuracy Is Not Guaranteed

Device location may be:

- Approximate
- Delayed
- Unavailable
- Based on network location
- Affected by device settings
- Incorrect indoors
- Incorrect when using a VPN

Do not rely on location tokens as the only evidence for critical decisions.

---

## 4. Date and Time Need Timezone Consideration

A timestamp from a mobile device may not match:

- UTC
- The organisation's standard timezone
- SharePoint regional settings
- Dataverse timezone settings
- The timezone expected by reporting systems

For enterprise use, store both:

```text
UTC Timestamp
```

and, where useful:

```text
Local Display Time
```

---

## 5. Trigger Tokens Depend on the Device

The result may differ depending on whether the flow is run from:

- Mobile phone
- Desktop browser
- Tablet
- Teams
- Another supported interface

Test the flow on every intended device type.

---

## 6. Users Must Be Authenticated

The User Name and User Email tokens depend on the signed-in account.

Production flows should use organisational accounts where required.

Do not rely only on manually entered identity information when the signed-in user token is available.

---

## 7. A Manual Trigger Does Not Prove Physical Presence

A user can sometimes run a flow from somewhere other than the expected location.

Location tokens can support a record but should not automatically be treated as indisputable proof of attendance.

---

## 8. Connection Problems Are Common

If the flow fails, check:

- Office 365 Users connection
- Outlook connection
- Notifications connection
- Signed-in account
- Selected environment
- Location permission

The browser version of Power Automate is normally better for repairing connections and reviewing detailed run history.

---

## 9. Templates Must Be Reviewed

A template gives a starting structure.

It may still contain:

- Unnecessary actions
- Broad recipient selection
- Hardcoded values
- Incorrect connections
- Inappropriate permissions
- Logic that does not match the business requirement

Always inspect and test every generated or template-based flow.

---

## 10. Avoid Sending Private Addresses Unnecessarily

The training exercise sends a full address by email.

In a real workplace scenario, sending an employee's home address to colleagues may be unnecessary and inappropriate.

A safer notification may say:

```text
I am working remotely today.
```

or:

```text
My working location today is London.
```

The flow should not disclose a home address unless there is a clear and approved business reason.

---

# ⚠️ Common Mistakes

- Using Full Address when only City is needed.
- Forgetting to enable location permission.
- Assuming mobile GPS is always exact.
- Sending sensitive location data to a large group.
- Ignoring timezone conversion.
- Using a personal account for a work process.
- Building the flow in the wrong environment.
- Failing to review connections.
- Not testing the Apply to Each loop.
- Sending duplicate notifications.
- Assuming the mobile app and browser behave identically.
- Not documenting why location data is collected.
- Retaining location records indefinitely.
- Using location as the only approval or attendance control.

---

# 🔐 Privacy and Governance Checklist

Before deploying a location-aware flow, ask:

- Why is location required?
- Which location token is the minimum necessary?
- Who will receive the location?
- Where will the information be stored?
- How long will it be retained?
- Can users see what is being collected?
- Is there an organisational policy covering this use?
- Is the data encrypted and access-controlled?
- Does the flow expose a home address?
- Is location being used for employee monitoring?
- Has the privacy or legal team reviewed the design where necessary?
- What happens when location is unavailable?
- Can the user correct an inaccurate value?

---

# 🧪 Testing Checklist

Test the flow with:

- Location permission enabled
- Location permission denied
- Precise location disabled
- Mobile data
- Wi-Fi
- Different timezones
- Different devices
- Different users
- Missing recipient data
- Broken connections
- Multiple colleagues
- No colleagues returned
- Approximate location
- A duplicate flow run
- A failed notification
- A failed email action

---

# 🏆 Best Practices

- Use the minimum necessary location detail.
- Prefer City or Site over Full Address.
- Explain clearly what the flow collects.
- Use organisational accounts.
- Validate the signed-in user.
- Store UTC where accurate reporting is required.
- Add error handling.
- Confirm that connections are healthy.
- Avoid exposing personal addresses.
- Use structured storage for business records.
- Set an appropriate retention period.
- Test on mobile and desktop.
- Use descriptive action names.
- Include a confirmation message.
- Document ownership and support arrangements.

---

# 🧱 Recommended Production Design

The training exercise uses:

```text
Instant Trigger
      ↓
Read Date and Address
      ↓
Send Email
```

A more controlled enterprise design might be:

```text
User Runs Flow
       ↓
Capture Signed-In User
       ↓
Ask for Business Purpose
       ↓
Capture City or Approved Site
       ↓
Capture UTC Timestamp
       ↓
Validate Required Values
       ↓
Create SharePoint or Dataverse Record
       ↓
Send Limited Notification
       ↓
Return Success Confirmation
```

This provides better auditability and reduces unnecessary disclosure.

---

# 📊 Suggested Data Fields

A structured record could contain:

| Field | Purpose |
|---|---|
| User Name | Identifies the person |
| User Email | Stores organisational identity |
| Local Date | User-friendly date |
| UTC Timestamp | Reliable reporting timestamp |
| City | General location |
| Site Name | Approved business location |
| Latitude | Only where genuinely required |
| Longitude | Only where genuinely required |
| Activity Type | Check-in, site visit, delivery, support |
| Reference Number | Links to the related request |
| Notes | Additional context |
| Created By | Audit field |
| Flow Run ID | Troubleshooting reference |
| Status | Successful, failed, incomplete |

---

# 🚀 How I Would Improve This Solution

For a workplace implementation, I would:

1. Remove the Full Address token unless it is essential.
2. Use City or an approved Site selection instead.
3. Capture the signed-in user's email automatically.
4. Save the record in SharePoint or Dataverse.
5. Store a UTC timestamp.
6. Add a business-reference field.
7. Send a Teams notification instead of a broad email where appropriate.
8. Add error handling for unavailable location.
9. Add a privacy notice.
10. Define retention and access controls.
11. Test the flow across different devices.
12. Avoid using the flow as the sole proof of attendance.

---

# 🧠 Engineering Design Questions

Before building a context-aware instant flow, ask:

- Why must the user start this manually?
- Which trigger tokens are genuinely required?
- Is location necessary?
- What level of location precision is appropriate?
- Could the same result be achieved by selecting an approved site?
- Who should receive the data?
- Should the data be emailed or stored?
- What happens if location permission is denied?
- How should timezone differences be handled?
- Is the signed-in identity sufficient?
- Could a user run the flow more than once?
- Does the process need duplicate prevention?
- How will failures be monitored?
- What is the retention period?
- Who owns and supports the flow?
- Does the design comply with organisational privacy policies?

---

# 💭 Reflection

This exercise demonstrated how instant flows can use contextual information already available on a user's device.

The basic pattern is:

```text
User Starts Flow
       ↓
Device Supplies Context
       ↓
Flow Uses Context
       ↓
Business Action Completes
```

Trigger tokens can make mobile automation faster and easier because users do not need to repeatedly enter their name, date, time, or location.

However, location-aware automation requires careful design. The most important technical lesson is not simply how to insert a Full Address token into an email. It is understanding when location data is appropriate, how accurate it is, who can see it, and how to avoid collecting more information than the process needs.

A strong enterprise solution should balance:

```text
Convenience
     +
Accuracy
     +
Privacy
     +
Security
     +
Governance
```

Context-aware flows are powerful when they reduce manual effort without creating unnecessary privacy or operational risk.
