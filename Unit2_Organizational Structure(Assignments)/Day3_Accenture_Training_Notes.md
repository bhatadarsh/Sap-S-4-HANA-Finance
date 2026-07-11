# Accenture Stream Training: SAP S/4HANA Finance
## Day 3 Assignments & Hands-On Walkthrough

Welcome to your study guide and reference documentation for **Day 3** of your SAP S/4HANA Finance Stream Training at Accenture. This document provides a complete step-by-step walkthrough of the hands-on exercises assigned for Day 3, explaining every step from system login to final configuration.

---

## Table of Contents
1. [General Prerequisites: SAP System Login](#1-general-prerequisites-sap-system-login)
2. [Assignment 1: Define and Assign Organization Structure](#2-assignment-1-define-and-assign-organization-structure)
3. [Assignment 2: Ledger Settings](#3-assignment-2-ledger-settings)
4. [Assignment 3: Currency Configuration](#4-assignment-3-currency-configuration)
5. [Topics Covered Today](#5-topics-covered-today)

---

## 1. General Prerequisites: SAP System Login

Before starting any configuration assignment, you must log into the SAP system and navigate to the customizing menu.

### Step-by-Step Login Process:
1. **Launch SAP GUI**: Double-click the SAP Logon pad icon on your desktop.
2. **Select System**: From the list of connections, select your designated training server (e.g., S/4HANA Sandbox) and double-click to open.
3. **Enter Credentials**: 
   * **Client**: Enter the 3-digit client number provided by the instructor.
   * **User**: Enter your assigned User ID.
   * **Password**: Enter your password.
4. **Log In**: Press `Enter` or click the green checkmark (Continue) button. You are now on the **SAP Easy Access** screen.
5. **Access Customizing (IMG)**:
   * In the top-left command field, type **`SPRO`** and press `Enter`.
   * Click on **SAP Reference IMG**. This opens the Implementation Guide tree where all configurations are made.

---

## 2. Assignment 1: Define and Assign Organization Structure

**Objective**: Create 1 Company, 2 Company Codes, and 2 Business Areas, and then assign the company codes to the company.

### Step 1: Define Company (T-code `OX15`)
* **Path**: `SPRO` > `SAP Reference IMG` > `Enterprise Structure` > `Definition` > `Financial Accounting` > `Define company`
* **Action**: Click "New Entries". Enter a 6-character code for your parent company, fill in the address and basic details, and save to your Transport Request (TR).

### Step 2: Define Company Codes (T-code `OX02`)
* **Path**: `SPRO` > `SAP Reference IMG` > `Enterprise Structure` > `Definition` > `Financial Accounting` > `Edit, Copy, Delete, Check Company Code`
* **Action**: Double-click on "Edit Company Code Data". Click "New Entries". Create your **first** company code (4 characters), provide the company name, city, country, currency, and language. Save it. Repeat the exact same process to create your **second** company code.

### Step 3: Define Business Areas (T-code `OX03`)
* **Path**: `SPRO` > `SAP Reference IMG` > `Enterprise Structure` > `Definition` > `Financial Accounting` > `Define Business Area`
* **Action**: Click "New Entries". Define a 4-character code for your first business area and a description. Repeat for the second business area. Save the entries.

### Step 4: Assign Company Codes to Company (T-code `OX16`)
* **Path**: `SPRO` > `SAP Reference IMG` > `Enterprise Structure` > `Assignment` > `Financial Accounting` > `Assign company code to company`
* **Action**: Click "Position" and search for your first Company Code. In the "Company" column next to it, enter the Company code you created in Step 1. Do the same for your second Company Code. Save.

---

## 3. Assignment 2: Ledger Settings

**Objective**: Create 1 or 2 new Ledgers and define their settings.

### Step 1: Define Settings for Ledgers and Currency Types
* **Path**: `SPRO` > `SAP Reference IMG` > `Financial Accounting` > `Financial Accounting Global Settings` > `Ledgers` > `Ledger` > `Define Settings for Ledgers and Currency Types`
* **Action**: 
  1. Under the dialog structure, click on **Ledgers**.
  2. Click "New Entries" to create your new ledgers (e.g., L1, L2). Specify if they are Non-Leading or Extension ledgers.
  3. Select your newly created ledger and double-click **Company Code Settings for the Ledger** in the dialog structure.
  4. Click "New Entries" and assign your previously created Company Codes to this new ledger. Save to your TR.

---

## 4. Assignment 3: Currency Configuration

**Objective**: Define exchange rate types, translation ratios, and maintain exchange rates.

### Step 1: Check Exchange Rate Types
* **Path**: `SPRO` > `SAP Reference IMG` > `SAP NetWeaver` > `General settings` > `Currencies` > `Check Exchange Rate Types`
* **Action**: Review or create specific exchange rate types. By default, SAP uses:
  * `M` (Standard Average Rate)
  * `B` (Bank Selling Rate)
  * `G` (Bank Buying Rate)
  If instructed to create a custom type, click "New Entries" and define a custom key and description.

### Step 2: Define Translation Ratios for Currency Translation
* **Path**: `SPRO` > `SAP Reference IMG` > `SAP NetWeaver` > `General settings` > `Currencies` > `Define Translation Ratios for Currency Translation`
* **Action**: You must specify the ratio between two currencies before entering an actual exchange rate. Click "New Entries". Enter the Exchange Rate Type (e.g., M), the "From" currency (e.g., USD), the "To" currency (e.g., INR), and set the ratio (typically 1:1, unless dealing with high-inflation or low-value currencies).

### Step 3: Maintain Exchange Rates (T-code `OB08`)
* **Direct Access**: Since OB08 is a standalone transaction, you can type `/nOB08` directly into the command field to open it.
* **Action**: Click "New Entries". Enter the Exchange Rate Type (e.g., M), the Valid From date (e.g., today's date), the From Currency (USD), the actual exchange rate (e.g., 83.50), and the To Currency (INR). Save the configuration.

---

## 5. Topics Covered Today

Below are general definitions for the topics scheduled for Day 3, based on your assignments. This serves as a quick conceptual reference:

### Core Organizational Structure
* **Defining & Assigning Structures**: The foundational architecture of SAP FI. It begins by creating the overarching corporate group (**Company**), defining independent legal entities (**Company Codes**), and establishing reporting segments (**Business Areas**). The assignment step links these independent entities together, ensuring that financial data from multiple company codes can roll up and consolidate into the parent company.

### Ledger Configuration
* **Ledgers Overview**: A ledger stores all accounting transactions. 
  * The **Leading Ledger (0L)** represents the main valuation method for the enterprise. 
  * Creating **Non-Leading Ledgers** allows a company to maintain separate, parallel accounting books (e.g., one book for IFRS and another for local tax laws) without redundant data entry. 
  * **Extension Ledgers** are used for manual management adjustments that sit on top of the base ledger without altering the underlying data.

### Currency Configuration
* **Exchange Rate Types**: Different types of rates used in business (Average, Buying, Selling). SAP allows you to configure which type of rate applies to specific transactions.
* **Translation Ratios**: A mathematical mapping (usually 1:1) that tells SAP how to relate two currencies before applying the exchange rate. 
* **Maintaining Exchange Rates**: The ongoing operational task (often updated daily via interfaces or manual entry in `OB08`) to ensure all foreign currency transactions are accurately converted to the company's local currency for accurate financial reporting.
