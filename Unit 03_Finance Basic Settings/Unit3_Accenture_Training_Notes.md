# Accenture Stream Training: SAP S/4HANA Finance
## Unit 3: Finance Basic Settings - Assignments & Concepts

Welcome to your study guide and reference documentation for **Unit 3: Finance Basic Settings** of your SAP S/4HANA Finance Stream Training. This document provides a complete step-by-step walkthrough of the hands-on exercises for Unit 3 and explains the core concepts mentioned in the syllabus.

---

## Table of Contents
1. [Assignment 1: Maintain Fiscal Year Variant & Posting Period Variant](#1-assignment-1-maintain-fiscal-year-variant--posting-period-variant)
2. [Assignment 2: Maintain Basic Settings](#2-assignment-2-maintain-basic-settings)
3. [Assignment 3: Create Tax Code (Input & Output)](#3-assignment-3-create-tax-code-input--output)
4. [Topics Covered Today (Concepts)](#4-topics-covered-today-concepts)

---

## 1. Assignment 1: Maintain Fiscal Year Variant & Posting Period Variant

**Objective**: Create a Fiscal year variant (Feb-Jan), create a posting period variant, open/close periods, and assign them to your company code.

### Step 1: Create a Fiscal Year Variant
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Ledgers` > `Fiscal year and Posting periods` > `Maintain Fiscal Year Variant`
*   **Action**: 
    1. Click "New Entries". 
    2. Enter a 2-character code.
    3. Since it is Feb-Jan, check the **Year-dependent** box as unchecked (it is year-independent), but **Calendar Year** must also be **unchecked** (it is a non-calendar year).
    4. Set **Number of posting periods** to `12` and **Number of special periods** to `2`.
    5. Select the variant and double click **Periods** in the dialog structure.
    6. For Month 1 (January), set Period to `12` and Year Shift to `-1`. From Month 2 (February) onwards, set Period 1 to 11 with Year Shift `0`. 

### Step 2: Define a New Posting Period Variant
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Ledgers` > `Fiscal year and Posting periods` > `Posting Periods` > `Define Variants for Open Posting Periods`
*   **Action**: Click "New Entries". Enter a variant code (e.g., matching your company code) and a description.

### Step 3: Open and Close Posting Periods
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Ledgers` > `Fiscal year and Posting periods` > `Posting Periods` > `Open and Close Posting Periods`
*   **Action**: Click "New Entries". Specify your variant. Define the account types (`+` for valid for all, `A`, `D`, `K`, `M`, `S`). Open the current period (e.g., From Period `1` To Period `1`) and close previous ones to control postings.

### Step 4: Assign Variants to Company Code (T-code `OBY6` / Customizing)
*   **Path (Fiscal Year)**: `Assign Company Code to a Fiscal Year Variant`
*   **Path (Posting Period)**: `Assign Variants to Company Code` (under Posting Periods)
*   **Action**: Link both variants created above to your 4-character Company Code. You can verify this assignment centrally using **T-code OBY6** (Global Parameters for Company Code).

---

## 2. Assignment 2: Maintain Basic Settings

**Objective**: Create document types, number ranges, field status variants, and tolerance groups.

### Step 1: Create New Document Type
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Document` > `Document Types` > `Define Document Types`
*   **Action**: 
    1. Click "New Entries". 
    2. Create a Document Type for Vendor Invoices (e.g., copy `KR`).
    3. Define Account types allowed (e.g., Vendors, G/L accounts).
    4. Assign a Number Range key and specify a reversal document type.

### Step 2: Create Number Range
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Document` > `Document Number Ranges` > `Define Document Number Ranges`
*   **Action**: Enter your Company Code. Click "Change Intervals". Enter the number range key specified in Step 1, year `2021`, a starting number, and an ending number. Leave the "External" checkbox unchecked (it must be internal).

### Step 3: Create Field Status Group Variant
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Ledgers` > `Fields` > `Define Field Status Variants`
*   **Action**: Copy standard variant `0001` to your custom variant code. Select it, double-click "Field status groups", and adjust the mandatory/optional/suppressed fields for groups like `G001`. Finally, assign this variant to your Company Code.

### Step 4: Define and Assign Tolerance Group
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Document` > `Tolerance Groups` > `Define Tolerance Groups for Employees`
*   **Action**: Click "New Entries". Enter your Company Code. You can leave the group blank (applies to all users) or give it a name. Define the upper limits (Amount per document, Amount per open item account item, Cash discount percentage). 
*   **Assign**: Go to `Assign User/Tolerance Groups` and assign your SAP user ID to the tolerance group.

---

## 3. Assignment 3: Create Tax Code (Input & Output)

**Objective**: Create tax codes, define percentages, and link them to GL accounts.

### Step 1: Create New Tax Code
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Tax on Sales/Purchases` > `Calculation` > `Define Tax Codes for Sales and Purchases`
*   **Action**: Enter your Country Code (e.g., `IN` for India, `US` for USA). Enter a 2-character Tax Code (e.g., `O1`, `I1`). 

### Step 2: Define Input or Output & Percentage
*   **Action**: In the properties, set the Tax Type: `V` for Input Tax (Purchases) or `A` for Output Tax (Sales). In the percentage screen, enter the tax percentage against the relevant condition type (e.g., MWVS for Input tax, MWAS for Output tax).

### Step 3: Maintain GL Accounts for the Tax Code
*   **Path**: `SPRO` > `Financial Accounting` > `Financial Accounting global settings` > `Tax on Sales/Purchases` > `Posting` > `Define Tax Accounts`
*   **Action**: Select the transaction key (e.g., `VST` for Input, `MWS` for Output). Enter your Chart of Accounts. Enter the GL account where the tax amounts should automatically post when this tax code is used.

---

## 4. Topics Covered Today (Concepts)

Below are detailed explanations of the key financial concepts introduced in Unit 3:

*   **Fiscal Year Variant**: Defines the financial/accounting year for the company. It dictates how many posting periods (usually 12 months) and special periods (up to 4, used for year-end audit adjustments) exist. It maps calendar dates to specific accounting periods (e.g., if Fiscal Year is April-March, then April is Period 1).
*   **Document Type**: A two-character key (like `SA` for GL, `KR` for Vendor Invoice) used to classify accounting documents. It controls what types of accounts can be posted to, mandates whether certain header fields are required, and links to the document number range.
*   **Number Range Configuration**: Every accounting document requires a unique identification number. Number ranges assign sequential numbers to documents either *Internally* (SAP automatically assigns the next available number) or *Externally* (the user manually types the document number).
*   **Posting Keys**: A two-digit numerical code (e.g., `40` for Debit GL, `50` for Credit GL) that determines at the line-item level: the account type (Customer, Vendor, GL, Asset, Material), whether it is a debit or credit, and influences field status.
*   **Posting Period Variant**: A security and control mechanism that dictates which accounting periods are "open" for users to post transactions into. By assigning this variant to a company code, the finance manager can easily lock a period (e.g., closing January) to prevent accidental back-dated postings.
*   **Field Status Control & Variant**: A setting that controls whether a specific field (like Cost Center or Text) is **Required** (must be filled), **Optional**, or **Suppressed** (hidden) when a user is posting a transaction. A Field Status Variant groups these rules together and is assigned to the company code.
*   **Tolerance and its Purposes**: Tolerances are built-in financial controls/limits. Employee tolerances restrict the maximum monetary amount a specific user can post in a single document (preventing a junior clerk from posting a billion-dollar entry). Customer/Vendor tolerances define acceptable payment differences (e.g., automatically accepting a payment that is $1 short).
*   **Tax Concepts & Tax Postings**: SAP handles taxes automatically. **Output Tax** is collected from customers on sales, while **Input Tax** is paid to vendors on purchases. By attaching a Tax Code to a line item, SAP calculates the percentage and automatically routes the tax amount to the designated GL account.
*   **Cross Company Code Transactions**: A single transaction that impacts two or more different company codes within the same SAP system. For example, Company Code A pays a vendor invoice on behalf of Company Code B. SAP automatically generates a clearing document to balance the intercompany receivables and payables between the two entities.
