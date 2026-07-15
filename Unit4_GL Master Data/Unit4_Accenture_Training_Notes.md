# Accenture Stream Training: SAP S/4HANA Finance
## Unit 4: GL Master Data - Assignments & Concepts

Welcome to your study guide and reference documentation for **Unit 4: GL Master Data** of your SAP S/4HANA Finance Stream Training. This document provides a complete step-by-step walkthrough of the hands-on exercises for Unit 4 and explains the core concepts associated with GL Master Data.

---

## Table of Contents
1. [Assignment 1: GL Master Data Configuration](#1-assignment-1-gl-master-data-configuration)
2. [Topics Covered Today (Concepts)](#2-topics-covered-today-concepts)

---

## 1. Assignment 1: GL Master Data Configuration

**Objective**: Create a Chart of Accounts, configure account groups, create various GL accounts with specific properties, and configure a profit center.

### Step 1: Create a New Chart of Accounts
*   **Path**: `SPRO` > `Financial Accounting` > `General Ledger Accounting` > `Master Data` > `G/L Accounts` > `Preparations` > `Edit Chart of Accounts List`
*   **Action**: Click "New Entries". Enter a 4-character code for your Operational Chart of Accounts. Set the **Length of G/L account number** to `7`. Assign a Group Chart of Accounts in the integration section if required. Save the configuration.

### Step 2: Assign Chart of Accounts to Company Code
*   **Path**: `SPRO` > `Financial Accounting` > `General Ledger Accounting` > `Master Data` > `G/L Accounts` > `Preparations` > `Assign Company Code to Chart of Accounts`
*   **Action**: Find your Company Code. Assign both your Operational Chart of Accounts and your Country Chart of Accounts (if applicable) in their respective columns. Save.

### Step 3: Create Account Groups
*   **Path**: `SPRO` > `Financial Accounting` > `General Ledger Accounting` > `Master Data` > `G/L Accounts` > `Preparations` > `Define Account Group`
*   **Action**: Click "New Entries". Create separate account groups for your Chart of Accounts for the following categories, assigning specific number ranges for each:
    *   **Expenses** (e.g., 4000000 - 4999999)
    *   **Assets** (e.g., 2000000 - 2999999)
    *   **Investments** (e.g., 2500000 - 2599999)
    *   **Liabilities** (e.g., 1000000 - 1999999)
    *   **Inventories** (e.g., 3000000 - 3999999)

### Step 4: Create GL Account for Investments
*   **T-Code**: `FS00` (Centrally)
*   **Action**: 
    1. Enter a new GL account number falling within your Investments/Assets number range.
    2. Set Account Group to the Assets group.
    3. In the Control Data tab, assign an **Alternative account number** corresponding to the Country Chart of Accounts.
    4. Save.

### Step 5: Create GL Account for Machinery Repair Cost
*   **T-Code**: `FS00`
*   **Action**: 
    1. Enter a GL account number within your Expenses number range.
    2. Select the GL Account Type as **Primary Costs or Revenue**.
    3. Link it to a cost element by specifying the **Cost element category** (e.g., category `1` for primary costs/cost-reducing revenues) in the Control Data tab.
    4. Assign to the Expenses account group. Save.

### Step 6: Create GL Account for Accounts Receivables
*   **T-Code**: `FS00`
*   **Action**: 
    1. Enter a GL account number within your Assets/Receivables number range.
    2. In the Control Data tab, set the **Recon. account for acct type** to `Customers`. This ensures the account cannot be posted to directly, but only via customer subledger postings. Save.

### Step 7: Profit Center Configuration
*   **Path**: `SPRO` > `Controlling` > `Profit Center Accounting` > `Master Data` > `Profit Center` > `Define Profit Center` (or via T-code `KE51`)
*   **Action**: 
    1. Create a Profit Center. 
    2. Assign a **Segment** to the Profit Center in the basic data tab. 
    3. Under the Company Codes tab, assign the profit center to your specific company code. 
    4. Click the "Activate" button (the matchstick icon) to make the profit center active for postings.

---

## 2. Topics Covered Today (Concepts)

*   **Chart of Accounts (CoA)**: The central list of all General Ledger (GL) accounts used by an organization. Setting the "Length" (e.g., 7) strictly defines how many digits a GL account number will have. The **Operational CoA** is used for daily postings, while a **Group CoA** is used for corporate consolidation, and a **Country CoA** meets local legal requirements.
*   **Account Groups**: These group GL accounts based on their financial nature (e.g., Assets, Liabilities, Revenues, Expenses). They serve two main purposes: controlling the number range for the accounts and controlling the field status (which fields are required, optional, or hidden) when a user creates a new GL account in `FS00`.
*   **Primary Cost or Revenue Account**: In S/4HANA, FI and CO (Controlling) are merged through the Universal Journal. A GL account classified as "Primary Costs or Revenue" simultaneously acts as a Cost Element in CO. The cost element category (e.g., `1`) tells the system how to handle cost allocations.
*   **Reconciliation Accounts**: Special GL accounts that integrate a subledger (like Accounts Receivable or Accounts Payable) with the general ledger. You cannot post a journal entry directly to a reconciliation account; the system automatically updates it when a transaction is posted to the associated customer or vendor subledger.
*   **Profit Centers & Segments**: Organizational units used for internal management reporting. A **Profit Center** tracks revenues and costs for a specific area of responsibility. A **Segment** is a higher-level classification used for geographical or product-line reporting to meet international accounting standards (like IFRS 8). Assigning a segment to a profit center ensures segment derivation during postings.
