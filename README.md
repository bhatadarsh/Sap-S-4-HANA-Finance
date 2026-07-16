# SAP S/4HANA Finance: Accenture Stream Training

This repository contains study guides, hands-on configuration walkthroughs, fundamental accounting concepts, and diagrams for the **Accenture Stream Training** on SAP S/4HANA Finance (commencing July 2026).

---

## 📂 Repository Structure

The training materials are organized by day. Each folder contains the original training screenshots along with structured study notes.

* **[Day1/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day1/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day1/Day1_Accenture_Training_Notes.md)**: Topics covered include:
    * ERP & SAP fundamentals (The 4 Ms: Men, Money, Material, Machinery).
    * The **Procure-to-Pay (PTP)** / Purchase Cycle flow.
    * **SAP R/3 3-Tier Architecture** (Presentation, Application, Database layers).
    * Accounting basics (Balance Sheet and Profit & Loss statement structures).
    * **SAP FI Organizational Structure** (Operating Concern, Controlling Area, Company Code, Chart of Accounts).
    * Hands-on SAP configuration steps: defining Group Company, creating Company Code (`MAK9`), defining Business Areas (`MAKB`, `MAKH`, `MAKM`), and assigning Company Code to Company.
  * Contains 19 reference screenshots mapping to theoretical slides and SAP GUI customization steps.

* **[Day2/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day2/Day2_Accenture_Training_Notes.md)**: Topics covered include:
    * **FI - Org Structure**: Ledger configuration, Parallel Accounting.
    * **FI - Basic Settings**: Fiscal year variants, Posting period variants, Field status, Tolerances, Document types, Number ranges, Posting keys.
    * **FI - Master Data**: General Ledger Master Record (Chart of Accounts, Account Groups).
  * Contains 24 reference screenshots mapping to theoretical slides and SAP GUI customization steps.

* **[Unit2_Organizational Structure(Assignments)/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit2_Organizational%20Structure%28Assignments%29/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit2_Organizational%20Structure%28Assignments%29/Day3_Accenture_Training_Notes.md)**: A complete, step-by-step walkthrough of the Unit 2 assignment exercises, covering:
    * **SAP System Login**: General prerequisites and navigation.
    * **Assignment 1**: Define and Assign Organization Structure (Company, Company Codes, Business Areas).
    * **Assignment 2**: Ledger Settings (Defining ledgers and assigning company codes).
    * **Assignment 3**: Currency Configuration (Exchange rate types, translation ratios, maintaining exchange rates).
  * Contains 3 PDF assignment exercise sheets.

* **[Unit 03_Finance Basic Settings/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit%2003_Finance%20Basic%20Settings/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit%2003_Finance%20Basic%20Settings/Unit3_Accenture_Training_Notes.md)**: Walkthrough for Unit 3 assignments and concepts:
    * **Assignment 1**: Maintain Fiscal Year Variant and Posting Period Variant.
    * **Assignment 2**: Maintain Basic Settings (Document Type, Number Ranges, Field Status Variant, Tolerance Group).
    * **Assignment 3**: Create Tax Code for output & input tax type.
  * Contains 3 PDF assignment exercise sheets.

* **[Unit4_GL Master Data/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit4_GL%20Master%20Data/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit4_GL%20Master%20Data/Unit4_Accenture_Training_Notes.md)**: Walkthrough for Unit 4 assignments and concepts:
    * **Assignment 1**: GL Master Data Configuration (Chart of Accounts, Account Groups, GL Accounts, Profit Centers).
  * Contains 1 PDF assignment exercise sheet.

* **[Unit5_DocumentSplitting/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit5_DocumentSplitting/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Unit5_DocumentSplitting/Unit5_Accenture_Training_Notes.md)**: Walkthrough for Unit 5 assignments and concepts:
    * **Assignment 1**: Document Splitting & Posting (Vendor invoices, GL balancing, Document Change Rules).
  * Contains 1 PDF assignment exercise sheet.

* **[15-07-2026 (Live Session)/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/15-07-2026/)**
  * **[Live Session Study Notes](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/15-07-2026/15-07-2026_Live_Session_Notes.md)**: A synthesis of 43 live classroom screenshots, detailing:
    * **Tax Configuration**: Assigning Tax Calculation Procedure (TAXINN).
    * **Retained Earnings**: Defining P&L account types and mapping the retained earnings account.
    * **Document Splitting**: Classifying GL accounts to item categories and configuring the Zero-Balance Clearing Account.
    * **Master Data**: Central creation of GL accounts via `FS00`.
  * Contains 43 reference screenshots.

* **[unit6-Business Transactions Processing/](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/unit6-Business%20Transactions%20Processing/)**
  * **[Study Notes & Configuration Guide](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/unit6-Business%20Transactions%20Processing/Unit6_Accenture_Training_Notes.md)**: Walkthrough for Unit 6 assignments and concepts:
    * **Assignment 1**: GL Business Transactions (Regular, Park, Hold, Reference, Recurring, Reversals, and Clearing).
  * Contains 1 PDF assignment exercise sheet.

---

## 🚀 How to Use These Notes

1. **Review Study Notes**: Open the study notes markdown file for each day (e.g., [Day 1 Notes](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day1/Day1_Accenture_Training_Notes.md)).
2. **Interactive Screenshot Reference**: Throughout the notes, click on any screenshot link to open the exact classroom capture.
3. **Follow Configuration Paths**: The hands-on sections include both the SPRO IMG navigation paths and direct transaction codes (T-codes) to make practicing in the SAP sandbox easier.

---

## 🔑 Common Transaction Codes (T-Codes) Reference

Here are the critical T-codes configured during the initial training phase:

| Transaction Code | Description | Purpose | Importance / Usage |
| :--- | :--- | :--- | :--- |
| **`SPRO`** | SAP Project Reference Object | Access the Customizing Implementation Guide (IMG). | ⭐ **Highly Used** (Daily config) |
| **`OX15`** | Define Company | Create the group-level organizational entity. | Foundational (One-time setup) |
| **`OX02`** | Define Company Code | Define legal entities for statutory reporting. | Foundational (One-time setup) |
| **`OX03`** | Define Business Area | Set up segments for geographical/product-line reporting. | Foundational (One-time setup) |
| **`OX16`** | Assign Company Code to Company | Bind the legal entity to the corporate parent group. | Foundational (One-time setup) |
| **`OBA7`** | Define Document Type | Defines document types and their associated number ranges. | ⭐ **Highly Important** (Core FI setup) |
| **`OBC4`** | Define Field Status Variants | Configures field behaviors (Required/Optional/Suppress) for GL accounts. | ⭐ **Highly Important** (Core FI setup) |
| **`OB08`** | Maintain Exchange Rates | Direct entry screen to maintain daily currency exchange rates. | ⭐ **Highly Important** (Daily operation) |
| **`FS00`** | Create G/L Account Centrally | Create, change, or display General Ledger master records. | ⭐ **Highly Important** (Master Data) |
| **`FB01`** | Post Document | Post standard financial documents (GL, Vendor, Customer). | ⭐ **Highly Used** (Daily operation) |
| **`FB02`** | Change Document | Modify changeable fields (like Document Date) in a posted document. | Standard Operation |
| **`FB03`** | Display Document | View posted documents (Entry View vs. General Ledger View). | ⭐ **Highly Used** (Audit/Review) |
| **`KE51`** | Create Profit Center | Create new Profit Center master data. | Foundational (Master Data) |
| **`SE16N`** | General Table Display | Query database tables directly (e.g., viewing `BKPF` for document headers). | ⭐ **Highly Important** (Technical/Debug) |
| **`FB50`** | Enter G/L Account Document | Single-screen transaction to post GL documents. | ⭐ **Highly Used** (Daily operation) |
| **`FV50`** | Park G/L Account Document | Save an incomplete GL document without updating balances. | ⭐ **Highly Used** (Daily operation) |
| **`FBD1`** | Enter Recurring Entry | Create a template for automated recurring postings. | Foundational (Periodic Processing) |
| **`FB08`** | Reverse Document | Reverse a previously posted financial document. | ⭐ **Highly Important** (Corrections) |
| **`F-04`** | Post with Clearing | Manually clear open items against incoming/outgoing payments. | ⭐ **Highly Used** (Daily operation) |
