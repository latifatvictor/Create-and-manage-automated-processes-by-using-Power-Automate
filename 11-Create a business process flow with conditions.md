# 📘 Module 11 - Create a Business Process Flow with Conditions

> Microsoft Learn Applied Skills  
> **Status:** ✅ Completed  
> **XP Earned:** 100 XP  
> **Estimated Duration:** 11 minutes

---

# 📖 Overview

In this module, I learned how to extend a linear Business Process Flow by adding conditional branches.

A linear Business Process Flow sends every user through the same stages in the same order.

A conditional Business Process Flow adapts the process path based on data entered in the record.

This makes it possible to design processes that respond to different business scenarios, such as:

- New versus pre-owned products
- High-value versus low-value requests
- Standard versus high-risk cases
- Approved versus declined service options
- Routine versus exceptional processing

The branch is selected automatically in real time according to the conditions defined in the process.

---

# 🎯 Learning Objectives

After completing this module, I can:

- Explain how branching works in a Business Process Flow.
- Add conditions using If-Else logic.
- Create separate true and false process paths.
- Combine multiple expressions using AND or OR.
- Merge branches back into a common stage.
- Understand branching depth and stage limitations.
- Apply branching to real business processes.
- Identify potential information-disclosure risks.
- Decide when separate Business Process Flows are safer than branches.

---

# 🔄 Linear vs Conditional Business Process Flows

## Linear Business Process Flow

Every record follows the same path.

```text
Stage 1
   ↓
Stage 2
   ↓
Stage 3
   ↓
Complete
```

This is suitable when the business process is consistent for every record.

Examples:

- Standard onboarding
- Basic case management
- Simple document review
- Routine service fulfilment

---

## Conditional Business Process Flow

The path changes according to data in the record.

```text
Initial Stage
      ↓
   Condition
   /       \
 Yes        No
  ↓          ↓
Path A     Path B
   \        /
    \      /
   Common Stage
        ↓
     Complete
```

This is useful when different records require different treatment.

---

# 🏗️ Example Architecture

```text
Qualify
   ↓
Check Car Preference
   /              \
New Car         Pre-Owned Car
   ↓                 ↓
New Car Sales   Pre-Owned Sales
       \           /
        \         /
        Deliver Quote
             ↓
          Complete
```

The process begins with a shared qualification stage, branches according to the customer's preference, and then merges back into a common quote stage.

---

# 🔑 Key Concepts Learned

## 1️⃣ Branches

Branches allow a Business Process Flow to follow different routes.

Each branch is based on a condition.

Example:

```text
Request Value > £10,000?
       /         \
     Yes          No
      ↓            ↓
Director Review  Manager Review
```

---

## 2️⃣ Real-Time Branch Selection

The process evaluates the rule using the data entered in the preceding stage.

The correct branch is selected automatically.

This gives users a process path that matches the current business scenario.

---

## 3️⃣ If-Else Logic

A condition creates two main outcomes:

```text
If condition is true
    → Follow Yes branch

Else
    → Follow No branch
```

Further conditions can be added to create additional paths.

Example:

```text
Request Type
     ↓
Is High Risk?
   /       \
 Yes        No
  ↓          ↓
Security   Standard
Review     Review
```

---

## 4️⃣ AND and OR Operators

A branching rule can contain multiple logical expressions.

### AND

All conditions must be true.

```text
Request Value > £10,000
AND
Data Classification = Confidential
```

The branch is selected only when both conditions are satisfied.

---

### OR

At least one condition must be true.

```text
Request Type = Emergency
OR
Priority = Critical
```

The branch is selected when either condition is satisfied.

---

## Important Limitation

A single branching rule can use:

```text
AND
```

or:

```text
OR
```

but not both within the same rule.

Complex logic may require an additional condition component.

---

# 📏 Branching Limits

Conditional Business Process Flows have important design limits.

| Limit | Maximum |
|---|---:|
| Dataverse tables per process | 5 |
| Stages per process | 30 |
| Steps per stage | 30 |
| Branch depth | 10 levels |

These are technical maximums, not design targets.

A process that approaches these limits may become difficult to understand, test, support, and govern.

---

# 🚦 Rules for Branching

## Branches Depend on the Previous Stage

A branching rule must use data from the stage immediately before the condition.

Example:

```text
Stage: Qualification

Fields:
- Car Preference
- Budget
- Purchase Time Frame
```

A condition placed after Qualification can use those fields.

It should not depend on unrelated data from a much earlier stage unless that data is also available in the immediately preceding stage.

---

## Both Outcomes Need a Valid Path

Each branch must lead to a valid stage.

```text
Condition
   /    \
Yes      No
 ↓        ↓
Stage A  Stage B
```

The process cannot be validated if one side has no destination.

---

## Branches Can Merge

Separate branches can later return to one common stage.

```text
Branch A
    \
     \
   Common Stage
     /
    /
Branch B
```

When branches merge, all peer branches must merge into the same stage.

---

## Branches Can End Separately

Instead of merging, every peer branch may end the process independently.

Valid:

```text
Branch A → End

Branch B → End
```

Invalid:

```text
Branch A → Merge

Branch B → End
```

Peer branches cannot partially merge while another peer branch ends.

---

# 🔗 Table Relationships

A Business Process Flow can move between Dataverse tables.

The relationship must be:

```text
One-to-Many
```

or:

```text
1:N
```

Relationships can help:

- Carry data between related records
- Reduce repeated data entry
- Reuse existing records
- Improve process navigation
- Support automation between stages

---

# 🔄 Returning to Previous Stages

Users can move the process back to a previous stage where permitted.

For example:

```text
Deliver Quote
      ↓
Move Back
      ↓
Propose
```

This can be useful when:

- Information is incomplete
- The customer changes their decision
- Additional review is required
- A proposal must be revised
- A case must return to investigation

Backward movement should be considered during process design because it may affect automation, notifications, and status reporting.

---

# 🛠️ Building the Conditional BPF

## Step 1: Create the Process

Inside a Solution:

```text
New
  ↓
Automation
  ↓
Process
  ↓
Business Process Flow
```

Example configuration:

| Property | Value |
|---|---|
| Flow Name | Car Sales Process |
| Unique Name | Generated schema name |
| Primary Table | Lead |

---

## Step 2: Configure the First Stage

Example stage:

```text
Qualify
```

Example steps:

- Purchase Time Frame
- Car Preference

These values provide the data needed for the branching rule.

---

## Step 3: Add a Condition

After the qualification stage:

```text
Car Preference = New?
```

Outcomes:

```text
Yes → New Car Sales

No → Pre-Owned Car Sales
```

---

## Step 4: Add the True Branch

Add a stage to the Yes path.

Example:

```text
New Car Sales
```

Possible steps:

- Model preference
- Specification
- Colour
- Finance requirement
- Delivery expectation
- Optional extras

---

## Step 5: Add the False Branch

Add a stage to the No path.

Example:

```text
Pre-Owned Car Sales
```

Possible steps:

- Vehicle age
- Mileage preference
- Service history
- Warranty requirement
- Budget
- Part-exchange details

---

## Step 6: Merge the Branches

After both sales paths are completed, merge them into:

```text
Deliver Quote
```

This common stage can contain steps such as:

- Final price
- Quote date
- Finance option
- Quote accepted

---

# 💼 Real-World Business Scenarios

## Procurement Approval

```text
Request Submitted
        ↓
Check Total Cost
      /          \
Over £10,000     £10,000 or Less
     ↓                  ↓
Director Review      Manager Review
        \              /
         \            /
          Procurement
               ↓
            Complete
```

---

## Access Request

```text
Access Requested
       ↓
Is Access Privileged?
      /             \
    Yes              No
     ↓                ↓
Security Review    Manager Approval
       \            /
        \          /
         Provisioning
              ↓
           Complete
```

---

## Employee Onboarding

```text
Starter Details
       ↓
Is Starter External?
      /             \
    Yes              No
     ↓                ↓
Contractor Checks  Employee Checks
       \            /
        \          /
          IT Setup
             ↓
          Complete
```

---

## Incident Management

```text
Incident Logged
       ↓
Severity Critical?
      /          \
    Yes           No
     ↓             ↓
Major Incident   Standard Support
Process          Process
       \          /
        \        /
         Resolution
             ↓
           Closure
```

---

## Travel Request

```text
Travel Request
       ↓
Cost Above Threshold?
      /              \
    Yes               No
     ↓                 ↓
Senior Approval     Manager Approval
        \            /
         \          /
       Travel Coordination
               ↓
            Complete
```

---

# 💼 Real-Life Work Applications

## Licence Governance

A conditional Business Process Flow could separate account types.

```text
Account Review
      ↓
Account Category?
   /       |        \
User    Shared    Resource
 ↓         ↓          ↓
User      Shared     Specialist
Review    Review      Review
```

This is valuable because disabled user accounts, shared mailboxes, and resource mailboxes should not automatically follow the same licence-removal process.

---

## Joiner, Mover and Leaver Management

```text
Request Received
       ↓
Request Type?
  /        |         \
Joiner    Mover      Leaver
  ↓         ↓          ↓
Onboard   Update     Offboard
Process   Process    Process
```

Each branch could contain different mandatory steps before returning to a common quality-check stage.

---

## Device Provisioning

```text
Device Request
      ↓
User Location?
   /             \
United Kingdom   International
      ↓               ↓
Standard Build    Local Support Review
        \             /
         \           /
         Provisioning
              ↓
           Dispatch
```

---

## Service Request Escalation

```text
Request Logged
      ↓
Business Impact?
   /            \
High             Normal
 ↓                ↓
Priority Review  Standard Queue
      \           /
       \         /
       Assignment
           ↓
        Resolution
```

---

# 🔐 Information Disclosure Risk

Conditional branches introduce an important security concern.

Even when a user does not have permission to open the underlying record or table, they may still be able to see:

- Stage names
- Branch names
- Process structure
- Possible actions
- The fact that a sensitive stage exists
- The route the process has taken

This can reveal confidential information.

---

# 🏦 Example: Fraud Investigation

Consider a banking process:

```text
Loan Request
      ↓
Amount > £50,000?
   /             \
 Yes              No
  ↓                ↓
Fraud Review     Standard Review
  ↓
Legal Action
```

A loan officer may not have permission to view the Investigation table.

However, if the entire process is contained in one BPF, the officer may still see:

- Fraud Investigation stage
- Legal Action stage
- The route taken by the process

This may reveal that the customer is under investigation.

---

# 🛡️ Safer Design

Instead of one large process, use two separate processes.

## Process 1: Loan Request

```text
Request Submitted
       ↓
Loan Review
       ↓
Approve or Deny
```

## Process 2: Investigation

```text
Investigation Opened
         ↓
Fraud Review
         ↓
Legal Decision
         ↓
Investigation Closed
```

A cloud flow or workflow can synchronise the final decision between the two records.

This prevents unauthorised users from seeing the existence or structure of the investigation process.

---

# 🚨 Important Points That Must Never Be Forgotten

## 1. Branch Visibility Can Reveal Sensitive Information

Table security does not necessarily hide the shape of the Business Process Flow.

Users may still see stage names even when they cannot open the underlying data.

Sensitive processes should often be separated.

---

## 2. Do Not Build One Giant Process for Everything

A technically valid BPF can still be badly designed.

One large process with many branches can become:

- Difficult to understand
- Difficult to secure
- Difficult to test
- Difficult to report on
- Difficult to maintain
- Difficult to train users on

Separate processes may be safer and clearer.

---

## 3. Conditions Must Use the Immediately Preceding Stage

Branching logic should be based on fields from the stage directly before the condition.

Plan the stage structure so the required decision data is available at the correct point.

---

## 4. Use AND or OR Carefully

A branching rule may combine conditions using one operator type.

Example:

```text
Condition A
AND
Condition B
```

or:

```text
Condition A
OR
Condition B
```

Do not assume that mixed expressions are supported in the same rule.

---

## 5. Branch Depth Is Limited

A branch can be no more than ten levels deep.

Even before reaching that limit, deeply nested branching is usually a warning that the process needs redesign.

---

## 6. Every Branch Must Be Tested

Test:

- True branch
- False branch
- Additional nested branches
- Branch merge
- Branch completion
- Backward stage movement
- Missing values
- Incorrect values
- User permissions
- Security visibility

---

## 7. Required Data Must Exist Before Evaluation

A condition can only make a reliable decision when the relevant field contains valid data.

Consider:

- Making the field required
- Adding business rules
- Setting default values carefully
- Validating data before stage progression

---

## 8. Think About Existing Records

More than one active process can run on the same record.

This may create confusion if users can choose between multiple active BPFs.

Define:

- Which process should be the default
- Which users can access each process
- Whether multiple concurrent processes are actually required

---

## 9. Branches Affect Reporting

Reports should account for:

- Which branch was selected
- Time spent in each branch
- Records that returned to earlier stages
- Records that were abandoned
- Records that never reached the common stage

---

## 10. Automation Must Understand the Branch

A cloud flow triggered by stage changes should not assume every record follows the same path.

Automation may need to check:

- Current stage
- Active path
- Branch reason
- Process status
- Related table
- Security context

---

# ⚠️ Common Mistakes

- Adding a condition before the required data has been captured.
- Creating overly complex nested branches.
- Mixing sensitive and non-sensitive stages in one process.
- Assuming table permissions hide stage names.
- Using both AND and OR in one branching rule.
- Failing to provide a stage for both outcomes.
- Merging only some peer branches.
- Not testing backward stage movement.
- Selecting the wrong primary table.
- Allowing users to access multiple confusing BPFs.
- Not documenting branch logic.
- Building branching logic that should have been separate processes.
- Ignoring reporting requirements.
- Forgetting to configure security roles.

---

# 🧪 Testing Checklist

Before activating a conditional BPF, test:

- The initial common stage
- Every required field
- Each condition
- True outcomes
- False outcomes
- Nested conditions
- Branch merges
- Separate branch endings
- Movement back to previous stages
- Multiple active process behaviour
- Table relationships
- User security roles
- Sensitive stage visibility
- Automation triggered by stage changes
- Process abandonment
- Reporting data

---

# 🏆 Best Practices

- Keep branch rules simple.
- Use meaningful condition and stage names.
- Capture decision data immediately before the branch.
- Avoid deep nesting.
- Merge branches only where the process genuinely becomes common.
- Use separate BPFs for sensitive processes.
- Apply least-privilege security.
- Test with different user roles.
- Document every branch and condition.
- Use Solutions for deployment.
- Use Dataverse relationships deliberately.
- Review the user experience before activation.
- Use cloud flows for notifications and cross-process synchronisation.
- Monitor branch usage after deployment.

---

# 📊 Suggested Branch Documentation

| Field | Purpose |
|---|---|
| Condition Name | Identifies the decision |
| Source Stage | Stage containing the decision data |
| Source Field | Dataverse column used |
| Operator | Equals, greater than, contains, and so on |
| True Branch | Stage selected when true |
| False Branch | Stage selected when false |
| Merge Stage | Common stage, where applicable |
| Security Impact | Whether branch names reveal sensitive information |
| Automation Impact | Cloud flows triggered by the branch |
| Business Owner | Person responsible for the rule |
| Technical Owner | Person supporting the process |

---

# 🚀 Recommended Enterprise Design

A well-designed conditional process may combine:

```text
Model-Driven App
       ↓
Business Process Flow
       ↓
Conditional Branch
       ↓
Dataverse
       ↓
Power Automate
       ↓
Approvals, Notifications and Updates
       ↓
Power BI Reporting
```

Example:

```text
Access Request Created
        ↓
BPF Captures Request Details
        ↓
Privileged Access?
     /              \
   Yes               No
    ↓                 ↓
Security Review    Manager Review
       \            /
        \          /
         Provisioning
              ↓
Cloud Flow Sends Confirmation
              ↓
Power BI Tracks Completion Time
```

---

# 🧠 Engineering Design Questions

Before creating branches, ask:

- Why does the process need to branch?
- Which field determines the route?
- Is that field captured in the immediately preceding stage?
- Is the condition simple enough for users to understand?
- Should the branches merge later?
- Should both branches end separately?
- Could a separate Business Process Flow be clearer?
- Could branch names reveal sensitive information?
- Which roles should see each process?
- Does each branch use the same Dataverse table?
- Are table relationships required?
- What automation runs in each branch?
- What happens if the data changes after branching?
- Can users return to an earlier stage?
- How will branch usage be reported?
- Who owns the branching rules?
- How will the process be tested?

---

# 💭 Reflection

This module demonstrated how Business Process Flows can adapt to different scenarios using conditional branching.

The most important lesson is that branching is not only a technical design decision. It also affects:

- User experience
- Security
- Data visibility
- Reporting
- Automation
- Supportability
- Governance

A conditional BPF should guide users through the correct path without exposing information they should not see.

The core pattern is:

```text
Capture Decision Data
        ↓
Evaluate Condition
        ↓
Select Appropriate Branch
        ↓
Complete Branch-Specific Steps
        ↓
Merge or End
```

Good branching makes a process more relevant and efficient.

Poor branching can make it confusing, insecure, and difficult to maintain.

The strongest design is not necessarily the one with the most branches. It is the one that gives users the clearest process while protecting sensitive information and remaining easy to support.
