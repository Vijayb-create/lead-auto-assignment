# 🚀 Lead Auto-Assignment System (Salesforce)

Automatically assigns incoming **Leads** to different Salesforce users based on the Lead's `Rating` field (e.g., Hot, Warm, Cold). This project uses **Apex Triggers**, **Custom Metadata**, and a **custom logging object** to ensure flexibility and traceability.

---

## 🧩 Features

- 🔄 Auto-assigns Lead records based on their Rating
- 🧠 Logic controlled via **Custom Metadata** (no hardcoding!)
- 📝 Tracks all assignments in a custom log object
- 💯 Includes test class for 100% code coverage

---

## 🧱 Components

| Type                | Name                       | Description                             |
|---------------------|----------------------------|-----------------------------------------|
| Trigger             | `LeadAssignmentTrigger`     | Runs on Lead insert                     |
| Apex Class          | `LeadAssignmentHandler`     | Handles assignment logic and logging    |
| Apex Test Class     | `LeadAssignmentHandlerTest` | Unit tests for trigger and logic        |
| Custom Metadata     | `Lead_Assignment__mdt`      | Maps Rating to User                     |
| Custom Object       | `Lead_Assignment_Log__c`    | Logs each assignment made               |

---

## 🛠️ Setup Instructions

### 1. Create Custom Metadata Type
- Name: `Lead_Assignment__mdt`
- Fields:
  - `Rating__c` (Text)
  - `User__c` (Lookup → User)

Create records like:
| Label | Rating__c | User__c |
|-------|-----------|---------|
| Hot   | Hot       | [User A] |
| Warm  | Warm      | [User B] |
| Cold  | Cold      | [User C] |

### 2. Create Custom Object
- Label: `Lead Assignment Log`
- Fields:
  - `Lead__c` (Lookup → Lead)
  - `Assigned_To__c` (Lookup → User)
  - `Rating__c` (Text)
  - `Assignment_Date__c` (Date/Time)

### 3. Deploy Apex Code
Upload the following files:
- `LeadAssignmentHandler.cls`
- `LeadAssignmentTrigger.trigger`
- `LeadAssignmentHandlerTest.cls`

You can deploy these via:
- Developer Console
- Salesforce CLI (VS Code)
- Change Sets

---

## 👨‍💻 Sample Code Snippet

### Apex Trigger
```apex
trigger LeadAssignmentTrigger on Lead (before insert) {
    if (Trigger.isBefore && Trigger.isInsert) {
        LeadAssignmentHandler.assignLeads(Trigger.new);
    }
}
# lead-auto-assignment
Lead Auto-Assignment System A Salesforce automation project that assigns incoming Leads to users based on their rating ("Hot", "Warm", "Cold"). Built using Apex Trigger, Handler class, Custom Metadata, and logging via a custom object. Demonstrates logic abstraction, metadata-driven development, and test coverage.
