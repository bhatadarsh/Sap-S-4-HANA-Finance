# Accenture Stream Training: SAP S/4HANA Finance
## Day 2 Training Notes & Reference Documentation

Welcome to your study guide and reference documentation for **Day 2** of your SAP S/4HANA Finance Stream Training at Accenture. This document summarizes the theoretical concepts and practical configuration steps covered, based on the provided screenshots and the SAP S/4HANA Finance Daywise Plan.

---

## Table of Contents
1. [FI - Org Structure & Ledger Configuration](#1-fi---org-structure--ledger-configuration)
2. [FI - Basic Settings](#2-fi---basic-settings)
3. [FI - Master Data](#3-fi---master-data)
4. [SAP Hands-On Customizing & Configuration Steps](#4-sap-hands-on-customizing--configuration-steps)
5. [Screenshot Index & Links](#5-screenshot-index--links)
6. [Topics Covered Today](#6-topics-covered-today)

---

## 1. FI - Org Structure & Ledger Configuration

### 1.1 Ledgers
A ledger is a central concept in Financial Accounting (FI). It represents a logical grouping or container for G/L accounts that share similar characteristics. It is used to record financial transactions, manage account balances, and produce financial reports (balance sheets, income statements, cash flow statements).

**Types of Ledgers:**
*   **Leading Ledger (`0L`)**: The primary ledger representing the main valuation and standard accounting principle for the entire organization.
*   **Non-Leading Ledgers (`L1`/`N1`, `L2`/`N2`, etc.)**: Used for parallel accounting (e.g., local reporting standards vs group reporting standards).
*   **Extension Ledgers (`E1`, `E2`, `E3`)**: Used to post management or reporting adjustments without duplicating the underlying data of the base ledger.

---

## 2. FI - Basic Settings

### 2.1 Fiscal Year Variants
The fiscal year determines the accounting period of a business. SAP allows different types of fiscal years:
*   **Calendar Year**: E.g., `K4` (Jan - Dec).
*   **Non-Calendar Year**: E.g., `V3` (April - March), `V6` (July - June), `V9` (Oct - Sept).

**Converting Calendar to Non-Calendar Year:**
SAP uses **Year Shifts** to map posting periods when they cross a calendar year boundary. 
*   **Year Shift Rules**: Previous Year Months (+1), Current Year Months (0), Next Year Months (-1).
*   *Example (V3 - April to March)*: Jan, Feb, March fall into the previous calendar year's logic and are shifted with `-1`.

### 2.2 Special Periods
SAP supports up to 4 special periods (typically periods 13 to 16) used for specific adjustments at year-end:
*   **13th Period**: Accounting/Finance department adjustments.
*   **14th Period**: Auditors Adjustments.
*   **15th Period**: Management adjustments (AGM Decisions).
*   **16th Period**: Tax department adjustments.

### 2.3 Posting Periods
Posting periods control the timeline within which transactions can be recorded.
*   **In FI**: Generally, only **one period** is open (the current month) for security purposes to prevent back-dated or future-dated entries by unauthorized users.
*   **In MM**: Generally, **two periods** are open (current and previous) to clear material transactions.

### 2.4 Document Types & Number Ranges
Document types classify the business transactions that take place.
*   `SA`: GL Documents (Number Range: 400000 - 499999)
*   `KR`: Vendor Invoice
*   `KZ`: Vendor Payment
*   `KA`: Vendor Adjustment Document
*   `DR`: Customer Invoice
*   `DZ`: Customer Payment
*   `DA`: Customer Adjustment Document
*   `AA`: Asset Documents (Number Range: 300000 - 399999)
*   `AF`: Asset Depreciation Document

**Use of Number Ranges:**
Number ranges easily identify where a transaction happened and who is responsible if an error occurs.
*   MM Document: 100000 - 199999
*   Sales Document: 200000 - 299999

### 2.5 Posting Keys
A posting key is a two-digit numerical key defining the type of transaction.
*   **Debit (DR)**: Increases an asset/expense account (e.g., receipt of cash).
*   **Credit (CR)**: Decreases an asset account, or increases liabilities/revenue (e.g., payment of liability).

**Account Types & Posting Keys:**
*   `S` (GL Accounts): DR `40`, CR `50`
*   `A` (Assets): DR `70`, CR `75`
*   `M` (Material): DR `89`, CR `99` (Also `80`-`86` and `90`-`96` for MM to GL)
*   `D` (Customers): DR `01-09`, CR `11-19`
*   `K` (Vendors): DR `21-29`, CR `31-39`

### 2.6 Field Status Variants
Field Status Variants specify the behavior of fields during transaction posting.
*   **Required (Mandatory)**: Must be filled (e.g., `TEXT`).
*   **Optional**: Can be filled but not necessary (e.g., `Assignment Number`).
*   **Suppress**: Hidden from the user during posting (e.g., `cost center`).

### 2.7 Tolerances
Tolerances set limits on the transaction amounts users can process, acting as an internal control mechanism.
*   **Top Level** (MD, CEO, GM): No Limit on amount per document (e.g., 999.999.999.999,00).
*   **Middle Level** (Managers, Supervisors): Limit 1,000,000.
*   **Lower Level** (Clerks, Executives): Limit 100,000.

---

## 3. FI - Master Data

### 3.1 Chart of Accounts (CoA)
A Chart of Accounts is a structured list of G/L accounts used to record transactions according to accounting standards.
**Types of CoA:**
1.  **Operative Chart of Accounts**: Used to record day-to-day business transactions (e.g., Salaries, Sales).
2.  **Group Chart of Accounts**: Used to consolidate all company codes under one overarching group.
3.  **Country-Specific Chart of Accounts**: Used to record legal transactions specific to a country (e.g., TDS in India is required, whereas it might be N/A in Japan).

### 3.2 Account Groups
An account group is a combination of accounts sharing the same nature.
*   **Examples**: Fixed Assets (Long term assets), Current Assets (Liquidity nature).
*   **Note**: Account groups control the number ranges for creating a GL account and control the field status during GL account creation.

---

## 4. SAP Hands-On Customizing & Configuration Steps

### Configuration Walkthrough (Step-by-Step)

#### Step 1: Assign Company Code to a Fiscal Year Variant
*   **Menu Path**: `Financial Accounting Global Settings` > `Ledgers` > `Fiscal Year and Posting Periods` > `Assign Company Code to a Fiscal Year Variant`
*   **Action**: Maps your specific company code to a fiscal year format (e.g., K4 or V3).

#### Step 2: Define Variants for Open Posting Periods
*   **Menu Path**: `Financial Accounting Global Settings` > `Ledgers` > `Fiscal Year and Posting Periods` > `Posting Periods` > `Define Variants for Open Posting Periods`
*   **Action**: Creates a posting period variant that can be assigned to your company code.

#### Step 3: Open and Close Posting Periods
*   **Menu Path**: `Financial Accounting Global Settings` > `Ledgers` > `Fiscal Year and Posting Periods` > `Posting Periods` > `Open and Close Posting Periods`
*   **Action**: Controls which periods are open for posting to prevent unauthorized entries.

#### Step 4: Define Document Type (T-code `OBA7`)
*   **Menu Path**: `Financial Accounting Global Settings` > `Document` > `Document type` > `Define Document Types`
*   **Action**: Defines document types and their associated number ranges.

#### Step 5: Edit Chart of Accounts List
*   **Menu Path**: `General Ledger Accounting` > `Master Data` > `G/L Accounts` > `Preparations` > `Edit Chart of Accounts List`
*   **Action**: Creates the chart of accounts structure.

#### Step 6: Define Field Status Variants (T-code `OBC4`)
*   **Menu Path**: `Financial Accounting` > `Financial Accounting Global Settings` > `Ledgers` > `Fields` > `Define Field Status Variants`
*   **Action**: Copy standard variant 001 to your custom variant (e.g., 1515) and configure field behaviors (Required, Optional, Suppress) for groups like G001 (General data).

#### Step 7: Define Tolerance Groups
*   **Menu Path**: Found under FI Basic Settings.
*   **Action**: Create new entries (e.g., for company code MAK9) specifying upper limits for posting procedures (amount per document, open item, cash discounts) for different employee levels.

#### Step 8: Company Code Settings for the Ledger
*   **Menu Path**: `Financial Accounting Global Settings` > `Ledgers` > `Ledger` > `Define Settings for Ledgers and Currency Types`
*   **Action**: Configures settings for Ledger `0L` for your Company Code (e.g., `MAK9` with Local Curr. Type `10`).

#### Step 9: Assign Accounting Principle to Ledger Groups
*   **Menu Path**: `Financial Accounting Global Settings` > `Ledgers` > `Parallel Accounting` > `Assign Accounting Principle to Ledger Groups`
*   **Action**: Maps accounting principles to specific ledger groups for parallel accounting purposes.

---

## 5. Screenshot Index & Links

Below are references to the key configuration paths executed in SAP GUI, captured in today's screenshots:

1. **Assign Company Code to a Fiscal Year Variant**: [095053.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20095053.png) 
2. **Define Variants for Open Posting Periods**: [095330.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20095330.png)
3. **Open and Close Posting Periods**: [095603.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20095603.png)
4. **Define Document Type (OBA7)**: [100522.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20100522.png)
5. **Edit Chart of Accounts List**: [104156.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20104156.png)
6. **Define Field Status Variants (OBC4)**: [105207.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20105207.png) / [104949.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20104949.png)
7. **Define Tolerance Groups**: [121622.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20121622.png)
8. **Company Code Settings for Ledger (0L)**: [122223.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20122223.png)
9. **Assign Accounting Principle to Ledger Groups**: [122720.png](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Screenshot%202026-07-09%20122720.png)

---

## 6. Topics Covered Today

According to the **SAP S/4HANA Finance Daywise Plan**, Day 2 focuses on core structural and foundational settings:
* **FI - Org Structure**: Ledger configuration, Parallel Accounting.
* **FI - Basic Settings**: Fiscal year variants, Posting period variants, Field status, Tolerances, Document types, Number ranges, Posting keys.
* **FI - Master Data**: General Ledger Master Record (Chart of Accounts, Account Groups).
