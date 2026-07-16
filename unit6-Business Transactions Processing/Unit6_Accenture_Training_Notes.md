# Accenture Stream Training: SAP S/4HANA Finance
## Unit 6: GL Business Transactions Processing - Assignments & Concepts

Welcome to your study guide and reference documentation for **Unit 6: GL Business Transactions Processing** of your SAP S/4HANA Finance Stream Training. This document provides a complete step-by-step walkthrough of the hands-on exercises for Unit 6, focusing on the various ways to process, park, hold, and reverse documents.

---

## Table of Contents
1. [Assignment 1: Document Posting Functions](#1-assignment-1-document-posting-functions)
2. [Topics Covered Today (Concepts)](#2-topics-covered-today-concepts)

---

## 1. Assignment 1: Document Posting Functions

**Objective**: Master the various document states (Hold, Park, Post), utilize reference/recurring documents, execute reversals, and perform clearing transactions with partial payments and cash discounts.

### Step 1: Create Regular GL Business Transactions
*   **T-Code**: `FB50` (Enter G/L Account Document) or `F-02` (General Posting).
*   **Action**: Post 3 or 4 standard business transactions (e.g., Cash debit, Expense credit). Enter document date, GL accounts, amounts, and ensure Debits = Credits before clicking **Post**.

### Step 2: Park a Document and Post it Later
*   **T-Code**: `FV50` (Park G/L Account Document) or `FB50` using the "Park" button.
*   **Action**: 
    1. Enter incomplete information for a document (e.g., enter the header and one line item, but don't balance it yet).
    2. Click **Park** instead of Post. The system assigns a document number, but no financial balances are updated.
    3. Later, go to `FBV0` (Post Parked Document), retrieve the parked document, complete the missing line item to balance it, and click **Post**.

### Step 3: Hold a Document and Post it Later
*   **T-Code**: `FB50` 
*   **Action**: 
    1. Start entering a document, but pause midway. 
    2. Click the **Hold** button. SAP will prompt you for a temporary "Hold Document Number" (you make this up, e.g., `TEMP123`). This is saved locally to your user session and does not get an official SAP document number.
    3. Later, in `FB50`, click "Held Document", enter your temporary number, finish the entry, and **Post**.

### Step 4: Post with Reference (Sample Document)
*   **T-Code**: `FB50` or `FB01`
*   **Action**: 
    1. Click the **Post with Reference** button.
    2. Enter the document number of a previously posted document (from Step 2 or 3).
    3. The system copies all the line items and header details into a new document. You can modify the amounts or dates if needed, then **Post**.

### Step 5: Create a Recurring Document
*   **T-Code**: `FBD1` (Enter Recurring Entry)
*   **Action**: 
    1. Enter a First Run Date, Last Run Date (8 months from now), and Interval (in months, e.g., `01` for monthly). Set the run date to the 2nd of the month.
    2. Enter the GL line items as usual (e.g., Rent Expense). Save it. (Note: This does not update GL balances; it acts as a template).
    3. **To actually post it**: You would run T-code `F.14` periodically to instruct SAP to generate the actual accounting documents based on the recurring template.

### Step 6: Reverse a Document
*   **T-Code**: `FB08` (Reverse Document)
*   **Action**: 
    1. Enter the document number of one of the regular postings from Step 1.
    2. Enter a Reversal Reason (e.g., `01` for Reversal in current period).
    3. Click **Save/Post**. SAP will generate a new document that perfectly reverses the debits and credits of the original document.

### Step 7 & 8: Partial Payments and Tolerance Groups (Cash Discounts)
*   **T-Code**: `OBA4` (Tolerance Groups for Employees) & `F-28` (Incoming Payments) or `F-53` (Outgoing Payments).
*   **Action**: 
    1. Ensure your User ID is assigned to a tolerance group in `OBA4` that allows cash discounts (e.g., up to 5%).
    2. When processing a payment against an invoice, go to the **Partial Pmt** tab.
    3. Enter a payment amount less than the total invoice amount. Observe how the system leaves the original invoice open but links the partial payment to it. If paying the full amount within the discount period, observe the cash discount being automatically calculated and posted to the discount GL account based on your tolerance limits.

### Step 9: Post with Clearing
*   **T-Code**: `F-04` (Post with Clearing) or `F-03` (Clear G/L Account).
*   **Action**: 
    1. Select an open item (like the remaining balance of the invoice from Step 7).
    2. Enter the offsetting entry (e.g., cash out).
    3. Process the open items to bring the balance to exactly zero, then **Post**. This changes the status of the line items from "Open" (Red status) to "Cleared" (Green status).

---

## 2. Topics Covered Today (Concepts)

*   **Document States (Parked vs. Held)**:
    *   **Held Document**: Saved temporarily by a specific user. It does not get an official SAP document number and cannot be used for reporting. It is simply a way to save your work midway without losing data.
    *   **Parked Document**: Saved to the database and gets an official SAP document number, but does not update financial balances. It can be viewed by other users and is heavily used in "Maker-Checker" (dual control) approval workflows.
*   **Post with Reference vs. Recurring Document**: 
    *   **Post with Reference**: A manual shortcut. You tell SAP, "Make a copy of document X right now so I don't have to type it again."
    *   **Recurring Document**: Automated scheduled postings. You create a master template, and SAP's batch jobs (`F.14`) automatically post the financial documents on a set schedule (e.g., straight-line rent or depreciation).
*   **Document Reversal (`FB08`)**: In accounting, you cannot simply delete a posted document. To correct an error, you must post a reversal. SAP does this automatically by creating a new document that flips the debits and credits of the erroneous document, providing a clear audit trail.
*   **Clearing vs. Partial Payment**:
    *   **Partial Payment**: The original invoice remains fully "Open" on the vendor/customer account, and the partial payment is posted as a separate "Open" item that references the invoice.
    *   **Residual Payment** (Alternative to Partial): The original invoice is "Cleared", and a brand new invoice is created for the remaining balance.
    *   **Clearing**: Matching equal debits and credits against each other so their net balance is zero, moving them to historical/cleared status.
