# Agentforce Sales Agent: Co-Build Workshop Guide

**Goal:** Build and activate two Agentforce agents together — an internal employee-facing agent and a customer-facing Sales Agent focused on Account Management.

---

## Table of Contents

1. [Prerequisites & Org Checklist](#1-prerequisites--org-checklist)
2. [Einstein & Data Cloud Configuration](#2-einstein--data-cloud-configuration)
3. [Build: Internal Employee-Facing Agent](#3-build-internal-employee-facing-agent)
4. [Build: Sales Agent — Account Management](#4-build-sales-agent--account-management)
5. [Build: Service Agent](#5-build-service-agent)
6. [Testing & Validation](#6-testing--validation)
7. [Deployment & Enablement](#7-deployment--enablement)

---

## 1. Prerequisites & Org Checklist

Complete this checklist before and during the workshop. Items marked **[Pre-Work]** should be verified before the session. Items marked **[Day-Of]** are confirmed together at the start.

---

### 1.1 Salesforce Edition & Licenses

> **[Pre-Work]** Confirm licenses are provisioned in **Setup → Company Information → Licenses**.

| Requirement | Details | Status |
|---|---|---|
| Salesforce Edition | Enterprise or Unlimited Edition required | ☐ |
| Agentforce License | Agentforce for Sales or Agentforce Platform license provisioned | ☐ |
| Einstein Platform License | Required for Einstein Generative AI features | ☐ |
| Data Cloud License | Data Cloud for Salesforce required for agent grounding | ☐ |
| Sales Cloud License | Required for Account Management agent actions | ☐ |

---

### 1.2 Org Settings

> **[Pre-Work]** Enable these settings at least **24 hours before the workshop**. Some features require a propagation window before they become active.

| Setting | Where to Enable | Status |
|---|---|---|
| Einstein Generative AI | Setup → Einstein Generative AI → Enable | ☐ |
| Agentforce Agents | Setup → Agents → Enable Agentforce | ☐ |
| Data Cloud | Setup → Data Cloud → Enable | ☐ |
| Einstein Activity Capture | Setup → Einstein Activity Capture → Enabled | ☐ |
| Sharing Settings | Org-Wide Defaults reviewed for Accounts, Contacts, Opportunities | ☐ |

---

### 1.3 User Permissions

> **[Pre-Work]** Create a Permission Set combining these permissions and assign it to all workshop participants before the session.

The users who will build and test the agents need the following permissions assigned.

**For the Build Team (Admins / Workshop Participants):**

| Permission | Where to Assign |
|---|---|
| Customize Application | System Permissions on Profile or Permission Set |
| Manage Einstein Features | Permission Set: Einstein AI Permissions |
| Agentforce Admin | Permission Set: Agentforce Admin |
| Data Cloud Admin | Permission Set: Data Cloud Admin |
| View Setup and Configuration | System Permissions |

---

### 1.4 Data Readiness

> **[Pre-Work]** Run a SOQL report or list view to confirm data quality before the workshop.

Review the following data quality checks before the workshop. Agent output quality depends on the completeness of the underlying data.

**Account Data (Required for Sales Agent):**

| Data Check | Recommended Threshold | Status |
|---|---|---|
| Accounts have Owner assigned | 100% | ☐ |
| Accounts have Industry populated | ≥ 80% | ☐ |
| Accounts have Last Activity Date within 90 days | ≥ 60% | ☐ |
| Open Opportunities linked to Accounts | Present in org | ☐ |
| Contacts linked to Accounts | ≥ 1 contact per active Account | ☐ |

**Internal Knowledge (Required for Employee-Facing Agent):**

| Data Check | Notes | Status |
|---|---|---|
| Knowledge Articles exist in Salesforce Knowledge | At least 10 articles recommended for testing | ☐ |
| Articles are categorized and published | Draft articles will not surface in agent responses | ☐ |
| Data Categories map to agent audience | Internal-only articles should be restricted appropriately | ☐ |

---

### 1.5 Pre-Workshop Environment Check

Run through this checklist together at the **start of the workshop session**:

- [ ] All participants can log into the Salesforce org
- [ ] All participants have the workshop Permission Set assigned
- [ ] Setup → Agents page loads without error
- [ ] Data Cloud is showing as Active in Setup
- [ ] At least one Einstein Generative AI model is connected (Setup → Einstein Generative AI → AI Models)
- [ ] Build environment confirmed — sandbox, sandbox-adjacent, or production. **Note:** Building in production is not recommended. Changes made during the workshop will be live immediately. If proceeding in production, ensure participants understand this risk.

---

*Next: [Einstein & Data Cloud Configuration →](#2-einstein--data-cloud-configuration)*

---

## 2. Einstein & Data Cloud Configuration

This section covers enabling the Einstein Generative AI platform and connecting Data Cloud to your org. Complete these steps before building either agent.

---

### 2.1 Enable Einstein Generative AI

1. Go to **Setup → Einstein generative AI → Einstein Setup**.
2. Enable **Einstein Setup** to on.

---

### 2.2 Connect Data Cloud

1. Go to **Setup → Data Cloud Setup Home** 
2. Click **Get Started** if Data Cloud has not been initialized, or confirm the status shows **Active** 

---

### 2.3 Enable Agentforce in Setup

1. Go to **Setup → Agentforce & GenAI**.
2. Click **Get Started with Einstein Generative AI**.
3. Click **Activate Agentforce**.
4. Click **Go To Agent Studio** → turn on **Agentforce Agent**.

---

### 2.4 Verify Einstein Trust Layer

1. Go to **Setup → Einstein Setup**.
2. Click **Go To Einstein Trust Layer**.
3. Confirm **Large Language Model Data Masking** is set to on.

---

*Next: [Build: Internal Employee-Facing Agent →](#3-build-internal-employee-facing-agent)*

---

## 3. Build: Internal Employee-Facing Agent

This agent helps employees look up internal processes and take follow-up actions. Build it by starting from the Agentforce Employee Agent template and adding subagents from the Asset Library.

---

### 3.1 Create the Agent in Agentforce Studio

1. Click to open the **App Launcher**, then search for and select **Agentforce Studio**.
2. Click **New Agent**.
3. Find **Agentforce Employee Agent**.
4. Click **Select Template**.
5. For the **Agent Name**, add **Employee Agent**.
6. For **Developer Name**, **Employee_Agent** autopopulates.
7. Click **Let's Go**.

---

### 3.2 Create a Subagent From Asset Library

1. Hover over the side of **Subagents** — a **+** icon will appear.
2. Click on the **+** icon.
3. Click **Add from Asset Library**.
4. Search **Single Record Summary** Subagent.
5. Click **Select**.
6. Search **General CRM** Subagent.
7. Click **Select**.
8. Click **Add to Agent**.
9. Click **Save**.
10. Click **Commit Version**.
11. A Confirmation screen will appear, click **Commit Version** again. 
12. Click **Activate**.
13. A confirmation screen will appear, click **Activate** again.

---

### 3.3 Test Employee Agent
1. Click **Preview**.
2. Ask a question to test the agent (e.g. *"Find me 'x' record"*).
3. Ask the agent to summarize your record.

---

*Next: [Build: Sales Agent — Account Management →](#4-build-sales-agent--account-management)*

---

## 4. Build: Sales Agent — Account Management

This agent helps sales reps manage their accounts. Build it by enabling Agentforce for Sales and configuring the prebuilt Sales Agent in Agentforce Studio.

---

### 4.1 Enable Agentforce for Sales

1. Go to **Setup**, search **Agentforce Account Management**.
2. Turn on **Account Management**.
3. A confirmation screen will appear, click **Confirm**.
4. Click **Finish Configuring Account Plans**.
5. Click **Turn on Account Research**.
6. Click **Set Up Einstein Conversation Insights**.
7. Click **Set Up Einstein Activity Capture**.

---

### 4.2 Configure Sales Agent

1. In **Setup**, search **Lightning App Builder**.
2. Click **Account - Default**.
3. Click **Edit**.
4. Search **Record Research** in left-hand components search bar.
5. Drag & drop **Record Research** to the account page.
6. Click **Save**.
7. Click **Activation...**.
8. Click **Remove as Org Default**.
9. Click **Desktop & Phone**.
10. Click **Save**.
11. Click **Activation...**.
12. Click **Assign as Org Default**.
13. Click **Desktop & Phone**.
14. Click **Save**.
15. Click **Save** at the top right side again. 

---

### 4.3 Test Sales Agent

1. Choose an account record you want to test. You'll get the best results if the account has at least one of the following: 1. A related account plan, 2. Related video or voice call records within the last 30 days, 3. Related emails within the last 30 days, 4. Notes created or modified within the last 30 days, 5. A recent or upcoming event.
2. Click **Research** in the account. 

---

*Next: [Build: Service Agent →](#5-build-service-agent)*

---

## 5. Build: Service Agent

This agent supports service workflows, grounded in your data library. Build it from the Agentforce Employee Agent template and connect a data library to ground the agent's responses.

---

### 5.1 Create the Agent in Agentforce Studio

1. Click to open the **App Launcher**, then search for and select **Agentforce Studio**.
2. Click **New Agent**.
3. Find **Agentforce Service Agent**.
4. Click **Select Template**.
5. For the **Agent Name**, add **Service Agent**.
6. For **Developer Name**, **Service_Agent** autopopulates.
7. Confirm the user record assigned is **New User**.
8. Click **Let's Go**.

---

### 5.2 Create Your Data Library

1. Go to **Setup** -> Search and select **Agentforce Data Library**.
2. Click **New Library +**.
3. Enter a unique name (i.e. "Service Agent Library").
4. Enter a description (i.e. “The central repository of knowledge articles, FAQs, and reference documents used by the FAQ Service Agent to resolve customer inquiries.”).
5. Add a data source by clicking on **Select a data type...**.
6. Select **Knowledge**. Note: Once set, you cannot change the data source type for this specific library.
7. Select the first identifying field as **Title**.
8. Select the second identifying field as **Summary**.
9. Scroll down and check off **Chat Answer**, **Details**, **Resolution**.
10. Click **Save** at the bottom. Note: This can take some time, wait till status reflects "Ready" in green. You may need to refresh to confirm. 


---

### 5.3 Connect Your Data Library

1. Click **Data** on the left hand bar.
2. Click **Data Library**.
3. Click **Select a library…**.
4. Connect your data library from the dropdown options.
5. Click **Save**.
6. Click **Commit Version**.
7. Click **Activate**.
8. Click **Activate** again.

---

### 5.4 Test Service Agent
1. Click **Preview**.
2. Ask a question to test the agent.


*Next: [Appendix A: Data Cloud Advanced Setup →](#appendix-a-data-cloud-advanced-setup)*

---

## Appendix A: Data Cloud Advanced Setup

Complete this setup to ground the Sales Agent in Data Cloud, enabling it to access unified account profiles and enriched data beyond standard CRM objects. This is recommended as a post-workshop follow-up for the Sales Account Management Agent.

---

### A.1 Create a Data Stream

A Data Stream ingests data from a source into Data Cloud.

> Confirm the Data Stream shows a status of **Active** before proceeding to the next step.

1. Go to **Data Cloud → Data Streams**.
2. Click **New**.
3. Select the data source type — for CRM data, choose **Salesforce CRM**.
4. Select the objects to ingest: **Account, Contact, Opportunity, Task**.
5. Choose the fields to include for each object (align with the fields configured in Section 4.3).
6. Set the refresh schedule — **Hourly** is recommended for sales data.
7. Click **Deploy**. Data Cloud will begin ingesting records on the next scheduled run.

---

### A.2 Map to Data Model Objects (DMOs)

Data Model Objects normalize ingested data into a standard schema that agents and Einstein features can query.

> Field mapping is the most time-consuming part of this setup. Allocate at least 30–60 minutes depending on data complexity.

1. Go to **Data Cloud → Data Model**.
2. For each Data Stream created in A.1, map it to the corresponding standard DMO:
   - Account → **Account DMO**
   - Contact → **Individual DMO** (or Contact DMO if available)
   - Opportunity → **Sales Order DMO** *(or a custom DMO if your org has one)*
   - Task/Activity → **Engagement DMO**
3. Map the source fields to the target DMO fields. Required fields must be mapped before the DMO can be activated.
4. Click **Save and Activate** for each DMO mapping.

---

### A.3 Ground the Sales Agent in Data Cloud

Once DMOs are active and populated, connect them to the Sales Agent.

> Test the agent after re-activation to confirm it retrieves enriched account data from Data Cloud in addition to standard CRM objects.

1. Go to **Setup → Agents** and open the **Sales Account Management Agent**.
2. In Agent Builder, navigate to **Data Sources**.
3. Click **Add Data Source → Data Cloud**.
4. Select the DMOs configured in A.2.
5. Set the data access scope to align with the rep's row-level security in Data Cloud.
6. Click **Save**.
7. Re-activate the agent to apply the new data source configuration.

---

## Appendix B: Einstein Trust Layer Configuration

The Einstein Trust Layer is enabled automatically when Einstein Generative AI is turned on. This appendix covers advanced configuration options for organizations with stricter data governance or compliance requirements.

---

### B.1 Zero Data Retention

By default, Salesforce does not store prompt or response data after an Einstein interaction completes. Zero Data Retention (ZDR) provides an additional contractual guarantee of this.

> ZDR is a contract-level setting, not a toggle in Setup. If this is a compliance requirement, engage your AE before the workshop.

1. Contact your Salesforce Account Executive to confirm ZDR is included in or available for your agreement.
2. Once confirmed, go to **Setup → Einstein Trust Layer → Data Retention**.
3. Verify the retention policy is set to **Zero Retention**.

---

### B.2 Grounding Controls

Grounding controls determine what data sources Einstein is allowed to use when generating responses. Review and restrict these per agent to enforce data boundaries.

1. Go to **Setup → Einstein Trust Layer → Grounding**.
2. Review the list of connected data sources.
3. For each agent, confirm only the intended data sources are enabled.
4. Disable any data sources that should not be accessible to a given agent.

---

### B.3 Data Masking

Data Masking prevents sensitive field values (e.g. SSNs, financial data) from being sent to the LLM in prompts. Use this section to add custom rules beyond the defaults set in Section 2.4.

1. Go to **Setup → Einstein Trust Layer → Data Masking**.
2. Confirm masking is enabled (set in Section 2.4).
3. To add custom masking rules, click **New Masking Rule**.
4. Specify the object, field, and masking pattern (e.g. mask all but last 4 digits of a phone number).
5. Click **Save**.

---

### B.4 Audit Trail

The Audit Trail logs all Einstein interactions — prompts sent, responses returned, and actions executed — for review and compliance purposes. Logs can be exported manually or queried via SOQL for integration with external compliance tools.

1. Go to **Setup → Einstein Trust Layer → Audit Trail**.
2. Confirm logging is enabled.
3. To export logs, click **Export** and select a date range.
4. Logs can also be queried via SOQL from the **EinsteinLlmAuditEvent** object for integration with external SIEM or compliance tools.
