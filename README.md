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

---

## 🚀 How to Use These Notes

1. **Review Study Notes**: Open the study notes markdown file for each day (e.g., [Day 1 Notes](file:///c:/Users/bhata/OneDrive/Desktop/Sap%20s4%20hana%20finance/Day1/Day1_Accenture_Training_Notes.md)).
2. **Interactive Screenshot Reference**: Throughout the notes, click on any screenshot link to open the exact classroom capture.
3. **Follow Configuration Paths**: The hands-on sections include both the SPRO IMG navigation paths and direct transaction codes (T-codes) to make practicing in the SAP sandbox easier.

---

## 🔑 Common Transaction Codes (T-Codes) Reference

Here are the critical T-codes configured during the initial phase:

| Transaction Code | Description | Purpose |
| :--- | :--- | :--- |
| **`SPRO`** | SAP Project Reference Object | Access the Customizing Implementation Guide (IMG). |
| **`OX15`** | Define Company | Create the group-level organizational entity. |
| **`OX02`** | Define Company Code | Define legal entities for statutory reporting. |
| **`OX03`** | Define Business Area | Set up segments for geographical/product-line reporting. |
| **`OX16`** | Assign Company Code to Company | Bind the legal entity to the corporate parent group. |
