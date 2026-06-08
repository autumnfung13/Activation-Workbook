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

### 3.4 Grant Access To Users

1. In **Setup**, search **Permission Sets**.
2. Click **New**.
3. For **Label**, add **Grant Employee Access**.
4. For **API name**, **Grant_Employee_Access** autopopulates.
5. For **Description**, add **This grants access to the active Agentforce for employee agents**.
6. Click **Save**.
7. Scroll down, find & click **Agent Access**.
8. Click **Edit**.
9. Click **Employee Agent**.
10. Click **Save**.
11. A confirmation screen that states **Your selections were saved.** will appear, click **Ok**.
12. Click **Manage Assignments**.
13. Click **Add Assignment**.
14. Search and find your name.
15. Check off the box next to your name.
16. Click **Next**.
17. Click **Assign**.
18. Click **Done**. 

---

### 3.5 Use The Employee Agent
1. Search for **Sales** in App Launcher.
2. Click the Agentforce icon.
3. Type in chat: **Tell me about xxxx ( find a contact name) and include a clickable link to the contact record., and ensure the link isn't just a text.**
4. Once the link is provided, click into it.
5. Type in chat: **Generate an email inviting contact name on a Agentforce event in two weeks, use Agentforce Event in June as the subject line and do not ask for additional details.**
6. Read over the email and click on **Send Email**.
7. Click **Send**.
8. Click **Activity** on contact record to view the email you just sent.

*Next: [Build: Sales Agent — Account Management →](#4-build-sales-agent--account-management)*

---

## 4. Build: Sales Agent — Account Management

This agent helps sales reps manage their accounts. Build it by enabling Agentforce for Sales and configuring the prebuilt Sales Agent in Agentforce Studio.

---

### 4.1 Enable Agentforce for Sales

1. Go to **Setup**, search **Agentforce Account Management**.
2. Turn on **Account Management**.
3. A confirmation screen will appear, click **Confirm**.
4. Click **Turn on Account Research**.
5. Click **Go to Setup** next to **Finish Configuring Account Plans**. A new tab will open.
6. Toggle over and turn on **Switch on Sales Account Plans**. 
7. Return to the tab you turned on **Account Management**.
8. Mark **Finish Configuring Account Plans** as done.
9. Click **Go to Setup** next to **Set Up Einstein Conversation Insights**. A new tab will open.
10. Click **Enable ECI**.
11. Return to the tab you turned on **Account Management**.
12. Mark **Set Up Einstein Conversation Insights** as done.
13. Click **Go to Setup** next to **Set Up Einstein Activity Capture**. A new tab will open.
14. Click **Get Started**.
15. Click the email / calendar service you use from the options. Click **Next**,
16. Click **User Level**. Click **Next**.
17. Write your name. Click **Next**.
18. Disable any options you want to restrict access to. If none, leave as is and click **Next**.
19. Review the **Advanced Settings**. Click **Next**.
20. Select your name from the **Available** section, and move it to **Selected** using the arrows. 
21. Review the **Exclude Addresses** section. Click **Next**.
22. Click **Finish**.
23. Return to the tab you turned on **Account Management**.
24. Mark **Set Up Einstein Activity Capture** as done.

---

### 4.2 Configure Sales Agent

1. In **Setup**, search **Lightning App Builder**.
2. Click **Account - Default**.
3. Click **Edit**.
4. Search **Record Research** in left-hand components search bar.
5. Drag & drop **Record Research** to the account page.
6. Click **Save**.
7. Click **Activation...**.
8. Click **Assign as Org Default**.
9. Click **Desktop & Phone**.
10. Click **Save**.
11. Click **Save** at the top right side again. 

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

### 5.3 Update Permissions 

1. Go to **Setup**, search and select **Permission Sets**.
2. Scroll, search & select **Agentforce Agent Service_Agent**.
3. Click **Object Settings**.
4. Select **Knowledge**, the API name should be **knowledge__kav**.
5. Confirm **Read** access is **enabled** under **Object Permissions**.
6. If not, click **Edit** and check off the box next to **Read** access. Then click **Save**.
7. Click **Permission Set Overview**.
8. Click **App Permissions**.
9. Click **Edit**. 
10. Scroll and find **Knowledge Management** section.
11. Check the box next to **Allow View Knowledge** to enable access.
12. Some orgs also require **Access Conversational Entries** - scroll to the top of the list.
13. Check the box next to **Allow conversational Entries** to enable access.
14. Click **Save**.
15. A confirmation screen will appear, click **Save** again.
16. Go to **Setup**, search and select **Profiles**.
17. Select **Einstein Agent User** profile.
18. Click **Data Category Visibility**.
19. Click **Edit** next to **Audience**.
20. Set visibility to **All Categories**. 
21. Click **Save**.
22. Repeat steps 19-22 for **Inquiry Type** and **Product**.

---

### 5.4 Connect Your Data Library

1. Click to open the **App Launcher**, then search for and select **Agentforce Studio**.
2. Click **Service Agent**, the one we created in step 5.1. 
1. Click **Data** on the left hand bar.
2. Click **Data Library**.
3. Click **Select a library…**.
4. Connect your data library from the dropdown options.
5. Click **Save**.
6. Click **Commit Version**.
7. Click **Activate**.
8. Click **Activate** again.

---

### 5.5 Test Service Agent
1. Click **Preview**.
2. Ask a question to test the agent.


*Next: [Appendix A: Data Cloud Advanced Setup →](#appendix-a-data-cloud-advanced-setup)*

---

## Appendix A: Extend Your Agent - Data

Complete this setup to ground the Sales Agent in Data Cloud, enabling it to access unified account profiles and enriched data beyond standard CRM objects. This is recommended as a post-workshop follow-up for the Sales Account Management Agent.

---

### A.1 Create a Data Stream

A Data Stream ingests data from a source into Data Cloud.

> Confirm the Data Stream shows a status of **Active** before proceeding to the next step.

1. Navigate to the **Data Cloud**.
2. Click on **Data Streams**.
3. Select **New Data Stream → Salesforce CRM**.
4. Click into **View Objects**.
5. Find and select **Knowledge (Knowledge_kav)**.
6. Select an **Object Category** (Other).
7. Select fields to be ingested.
8. Add any relevant filters i.e. (Publication Status = Published).
9. **Deploy**.

---

### A.2 Map DLO to DMO

Mapping the Data Lake Object (DLO) to a Data Model Object (DMO) normalizes the ingested Knowledge data into a standard schema that agents and retrievers can query.

> You may need to create new fields in the DMO to mirror the source fields. Required fields must be mapped before the DMO can be activated.

1. From the **Data Stream** page, locate **Data Mapping** on the right-hand side of the page.
2. Click **Start** under **Data Mapping**.
3. Click **Select Objects**.
4. Type **Knowledge**.
5. Select the **+** beside **Knowledge Article Version**.
6. Map fields from **DLO** to **DMO**. You may need to create new fields in the DMO.
7. Click **Save and Close**.

---

### A.3 Build A Custom Retriever

A Retriever lets the agent search and return the most relevant Knowledge articles from Data Cloud at runtime. Build the Search Index first so the retriever has something to query, then configure the retriever fields and citations the agent will return.

> Confirm the retriever shows a status of **Active** before connecting it to your agent.

1. Click into the **Search Index** tab.
2. Click **New**.
3. Click **Easy Setup**.
4. Select **Knowledge Article Version**.
5. Click **Save**.
6. Click into the **Agentforce Studio** tab.
7. Click **Retrievers**.
8. Click **New Retriever**.
9. Select **Individual Retriever**.
10. Under **Retriever Type**, select **Data Cloud**.
11. Select **Default**.
12. Select **Knowledge Article Version**.
13. Select **Knowledge Article Version** again.
14. Under **Define Filters**, select **All Documents**.
15. Under **Configure Retriever Results**, set the result count to **20**.
16. For **Fields to return**, add the **Details** field.
    - Click into **Field Name** → **Direct Attributes** → **Knowledge Article Version** → select the field.
17. Repeat to add the **Title** field.
18. Repeat to add the **URL** field.
19. Toggle on **Standard Citations**.
20. Click **Save**.
21. Click **Activate**.

---

## Appendix B: Extend Your Agent - Agentic Development 

This appendix covers advanced agent customization — cloning and editing prompt templates so the agent uses your custom retriever and returns results tailored to your business.

---

### B.1 Clone A Prompt Template

The default **Answer Questions with Knowledge** prompt template uses Salesforce's out-of-the-box dynamic retriever. Clone and edit it to wire in the custom Knowledge Article Version retriever built in A.3, then validate the output in Prompt Builder before connecting it to the agent.

> Confirm results are accurate in Prompt Builder before moving on to the Agent Builder.

1. Navigate to **Setup**.
2. Search for **Prompt Builder**.
3. Open **Answer Questions with Knowledge**.
4. Click **Deactivate**.
5. Click **Save As New Version**.
6. Under the **KNOWLEDGE** heading, remove `{!$EinsteinSearch:sfdc_ai__DynamicRetriever.results}`.
7. Click **Insert Resource**.
8. Select **Retriever**.
9. Select **Custom Retriever**.
10. Select **Knowledge Article Version**.
11. Select **Knowledge Article Version Retriever**.
12. Click into the retriever.
13. In the **Search Text** field on the left-hand side, click into the search bar.
14. Select **Free Text**.
15. Select **Query**.
16. Add **Details** as an Output Field.
17. Add **URL** as an Output Field.
18. Update **Number of Results** to **20**.
19. Add any additional customization to tailor the prompt to your business.
20. Test thoroughly in **Prompt Builder**.
21. Confirm the results are accurate in Prompt Builder before moving on to the Agent Builder.

---

## Appendix C: Einstein Trust Layer Configuration

The Einstein Trust Layer is enabled automatically when Einstein Generative AI is turned on. This appendix covers advanced configuration options for organizations with stricter data governance or compliance requirements.

---

### C.1 Zero Data Retention

By default, Salesforce does not store prompt or response data after an Einstein interaction completes. Zero Data Retention (ZDR) provides an additional contractual guarantee of this.

> ZDR is a contract-level setting, not a toggle in Setup. If this is a compliance requirement, engage your AE before the workshop.

1. Contact your Salesforce Account Executive to confirm ZDR is included in or available for your agreement.
2. Once confirmed, go to **Setup → Einstein Trust Layer → Data Retention**.
3. Verify the retention policy is set to **Zero Retention**.

---

### C.2 Grounding Controls

Grounding controls determine what data sources Einstein is allowed to use when generating responses. Review and restrict these per agent to enforce data boundaries.

1. Go to **Setup → Einstein Trust Layer → Grounding**.
2. Review the list of connected data sources.
3. For each agent, confirm only the intended data sources are enabled.
4. Disable any data sources that should not be accessible to a given agent.

---

### C.3 Data Masking

Data Masking prevents sensitive field values (e.g. SSNs, financial data) from being sent to the LLM in prompts. Use this section to add custom rules beyond the defaults set in Section 2.4.

1. Go to **Setup → Einstein Trust Layer → Data Masking**.
2. Confirm masking is enabled (set in Section 2.4).
3. To add custom masking rules, click **New Masking Rule**.
4. Specify the object, field, and masking pattern (e.g. mask all but last 4 digits of a phone number).
5. Click **Save**.

---

### C.4 Audit Trail

The Audit Trail logs all Einstein interactions — prompts sent, responses returned, and actions executed — for review and compliance purposes. Logs can be exported manually or queried via SOQL for integration with external compliance tools.

1. Go to **Setup → Einstein Trust Layer → Audit Trail**.
2. Confirm logging is enabled.
3. To export logs, click **Export** and select a date range.
4. Logs can also be queried via SOQL from the **EinsteinLlmAuditEvent** object for integration with external SIEM or compliance tools.
