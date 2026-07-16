# Accenture Stream Training: SAP S/4HANA Finance
## Live Session Notes: 16-07-2026 (Document Parking & Approval Workflow)

Welcome to your study guide based on the live session screenshots captured on **16-07-2026**. This session provided a practical, hands-on demonstration of the concepts covered in Unit 6, focusing specifically on the **Document Parking and Approval Workflow** (Maker-Checker process).

---

## 1. Live Configuration Walkthrough

### Part A: The "Maker-Checker" Parking Workflow
The primary focus of this session was demonstrating how a junior accountant (Maker) can park a document, and a senior accountant/manager (Checker) can review and post it.

#### Step 1: Parking the Document
*   **Context**: The junior accountant needs to enter a journal entry but requires approval before it updates the GL balances.
*   **Action**: In the screenshots, the user enters a standard GL document (e.g., Debiting Salaries A/C and Crediting HDFC Bank A/C). Instead of clicking 'Post', the user navigates to the top menu: **Document > Park (F8)**.
*   **Result**: SAP saves the document (e.g., Doc `100002`) to the database without updating any financial balances.

#### Step 2: Sending a Message to the Superior (T-Code `SO00`)
*   **Context**: The superior needs to be notified that a document is waiting for their approval.
*   **Action**: The user opens T-code **`SO00`** (SAP Business Workplace / SAP Mail). 
*   **Detail**: The user drafts a short internal message: *"Doc 100002 need approved and Posted"*. They set the Recipient Type to **SAP Logon Name** and enter the superior's username (e.g., `KUMARM`). The message is dispatched to the superior's SAP inbox.

#### Step 3: Posting the Parked Document by Superior (T-Code `FBV0`)
*   **Context**: The superior logs in, checks their `SO00` inbox, and sees the pending document number.
*   **Action**: The superior uses T-code **`FBV0`** (Post Parked Document). They pull up Document `100002`, review the line items (Salaries and Bank), verify the amounts, and then click **Post**. 
*   **Result**: The system converts the parked document into a real accounting document. We see the final success message: *"Document 100004 was posted in company code MAK9"*.

---

### Part B: Number Range Maintenance (T-Code `FBN1`)
*   **Context**: The session also touched upon ensuring document number ranges were properly maintained for the posting process.
*   **Action**: We see the configuration screen for **Object RF_BELEG** (the technical name for Accounting Document Number Ranges) for Company Code `MAK9`. This is where intervals are defined so that when documents are parked or posted, SAP knows exactly which sequential number to assign to them.

---

## 2. Topics Covered Today (Concepts)

*   **The Maker-Checker Principle (Dual Control)**: A vital internal control concept in finance. It dictates that the person who initiates a financial transaction (the Maker) cannot be the same person who authorizes/posts it (the Checker). Document Parking is SAP's native way of enforcing this.
*   **Parked Documents vs. Held Documents**: As a reminder from Unit 6, Parked documents are visible to the whole organization and get an official document number from the number range interval. Held documents are only visible to the user who held them and use a temporary, made-up number.
*   **SAP Business Workplace (`SO00`)**: SAP's internal email and workflow inbox system. While modern S/4HANA systems often use automated Business Workflows (where the document automatically appears in a Fiori My Inbox app), `SO00` is the traditional, manual way of sending internal notifications and documents between SAP users.
