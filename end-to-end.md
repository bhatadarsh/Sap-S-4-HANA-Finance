# SAP S/4HANA Finance: Beginner's End-to-End Implementation Guide

Welcome to your master implementation guide! This document is designed specifically for beginners. It takes all the individual assignments you've been given from **Unit 2 through Unit 9** and strings them together into one continuous, logical project.

Instead of just telling you *what* to click, this guide explains *why* you are clicking it. We will use a consistent set of fictitious data (The "MAK9 Group") so that every assignment builds perfectly on top of the previous one.

---

## 🏗️ The Scenario: "MAK9 Group"
To follow this guide exactly, type exactly what is suggested in the "Examples" below.
*   **Company (The parent group)**: `MAK9` (MAK9 Group)
*   **Company Codes (The regional branches)**: `MAK1` (US Branch) and `MAK2` (Europe Branch)
*   **Business Areas**: `MAKB` (Bikes) and `MAKH` (Helmets)
*   **Chart of Accounts**: `MAK9`

---

## Phase 1: Organizational Structure (Unit 2 Assignments)

### Assignment Prompt: 
> *"Create 1 company, 2 company codes and 2 business areas. Assign company codes to company."*

**Explanation for Beginners**: 
Before you can post any financial data in SAP, you must build the "legal skeleton" of the business. 
*   A **Company** is the highest level (the global corporate group).
*   A **Company Code** is a distinct legal entity (like a regional branch) that requires its own separate balance sheet and tax reporting. We need 2 of them to practice cross-company transactions later.
*   A **Business Area** is a separate line of business (e.g., selling Bikes vs. Helmets) used for internal management reporting.

### Step-by-Step Configuration:

**1. Create the Company**
*   **Path**: SPRO > Enterprise Structure > Definition > Financial Accounting > Define company (or T-Code `OX15`).
*   **Action**: Click **New Entries**.
*   **Type this**: 
    *   Company: `MAK9`
    *   Company Name: `MAK9 Group`
    *   Fill in any mock address/country data and click **Save**.

**2. Create 2 Company Codes**
*   **Path**: SPRO > Enterprise Structure > Definition > Financial Accounting > Edit, Copy, Delete, Check Company Code (or T-Code `OX02`).
*   **Action**: Click **New Entries**.
*   **Type this (First CC)**: Company Code `MAK1`, Name `MAK9 US`, Country `US`, Currency `USD`. Save.
*   **Type this (Second CC)**: Company Code `MAK2`, Name `MAK9 EU`, Country `DE`, Currency `EUR`. Save.

**3. Create 2 Business Areas**
*   **Path**: SPRO > Enterprise Structure > Definition > Financial Accounting > Define Business Area (or T-Code `OX03`).
*   **Action**: Click **New Entries**.
*   **Type this**: 
    *   `MAKB` - MAK9 Bikes Division
    *   `MAKH` - MAK9 Helmets Division

**4. Assign Company Codes to the Company**
*   **Path**: SPRO > Enterprise Structure > Assignment > Financial Accounting > Assign company code to company (or T-Code `OX16`).
*   **Action**: Find `MAK1` in the list, and in the "Company" column next to it, type `MAK9`. Do the same for `MAK2`. Save. *(Why? This links the regional branches to the parent group for consolidated reporting).*

---

## Phase 2: Global Financial Settings (Unit 3 Assignments)

### Assignment Prompt:
> *"Create new document type to post vendor invoice. Define parameters. Create number range. Create new Field status group variant. Define new tolerance group and assign to user."*

**Explanation for Beginners**:
Now that the skeleton exists, we must define the rules of accounting for `MAK1` and `MAK2`.
*   **Document Types & Number Ranges**: Every time you save a journal entry, SAP assigns it a unique ID number. We must tell SAP what number to start counting from (e.g., 100000 to 199999).
*   **Field Status Variant**: Controls whether fields on a screen are mandatory, optional, or hidden when a user is typing an invoice.
*   **Tolerance Groups**: Security limits. It prevents a junior accountant from posting a billion-dollar invoice by accident.

### Step-by-Step Configuration:

**1. Assign Fiscal Year & Posting Periods**
*   **T-Code**: `OB37` (Fiscal Year) and `OBBP` (Posting Period).
*   **Action**: SAP needs to know if your financial year runs Jan-Dec or April-March. Assign the standard calendar year **`K4`** to `MAK1` and `MAK2`. 

**2. Create Document Number Range**
*   **T-Code**: `FBN1`
*   **Action**: Enter Company Code `MAK1`. Click the **Intervals (Pencil)** icon. 
*   **Type this**: No: `01`, Year: `2026`, From No: `100000`, To Number: `199999`. Save.

**3. Create and Assign Field Status Variant**
*   **T-Code**: `OBC4` (Define) then `OBC5` (Assign).
*   **Action**: In `OBC4`, highlight the standard SAP variant `0001` and click the **Copy As** button. Name your copy `MAK9`. Save. Then go to `OBC5` and type `MAK9` next to Company Codes `MAK1` and `MAK2`.

**4. Define Tolerance Group and Assign to User**
*   **T-Code**: `OBA4` (Define) and `OB57` (Assign).
*   **Action**: In `OBA4`, click **New Entries**. Enter Company Code `MAK1`. *Leave the Tolerance Group name blank* (this makes it the default for everyone). Set the "Amount per document" to `999,999,999` and Cash Discount to `5%`. Save.

---

## Phase 3: Master Data Foundation (Unit 4 & 8 Assignments)

### Assignment Prompt (Unit 4):
> *"Define Chart of Accounts, Account Groups, Retained Earnings Account, and create GL accounts."*

### Assignment Prompt (Unit 8):
> *"Create one Business Partner master record. Create FI Customer BP and FI Vendor BP."*

**Explanation for Beginners**:
Master Data is the permanent data in the system. 
*   **Chart of Accounts (COA)** is the master list of every single G/L account (like Bank, Rent, Salaries). 
*   **Retained Earnings**: At the end of the year, all profit/loss accounts empty their balances into this one specific balance sheet account.
*   **Business Partner (BP)**: In modern SAP (S/4HANA), we don't create "Vendors" and "Customers" separately. We create one "Business Partner" (a person or company) and simply give them *roles* (they can buy from us, and sell to us).

### Step-by-Step Configuration:

**1. Define Chart of Accounts (COA)**
*   **T-Code**: `OB13` (Define) and `OB62` (Assign).
*   **Action**: Create COA `MAK9`. Length of GL Account Number: `6`. Save. In `OB62`, assign `MAK9` to `MAK1` and `MAK2`.

**2. Define Account Groups & Retained Earnings**
*   **T-Code**: `OBD4` (Account Groups) and `OB53` (Retained Earnings).
*   **Action**: In `OBD4`, create groups for `MAK9`: e.g., `ASST` (Assets: 100000-199999) and `LIAB` (Liabilities: 200000-299999). 
*   **Action**: In `OB53`, enter COA `MAK9`. Type P&L Statement Account type: `X`. Type Account: `100100`. (Ignore the warning that the account doesn't exist yet, press enter to save).

**3. Create GL Accounts (`FS00`)**
*   **Action**: Open `FS00`. Ensure Company Code is `MAK1`. 
*   Create `100100` as a Balance Sheet account (Retained Earnings). 
*   Create `100500` as a Balance Sheet account. In the "Control Data" tab, set **Recon. Account for Acct Type** to **Customers**. *(Why? We cannot post directly to a customer account; SAP posts to this Recon GL in the background automatically).*

**4. Create the Business Partner (`BP`)**
*   **Action**: Open T-Code `BP`. Click **Organization**.
*   **Role 1**: Select role `000000` (General). Type name "Global Tech Supplies". Save. Write down the BP Number (e.g., `BP9001`).
*   **Role 2**: Change the dropdown role to `FLCU00` (FI Customer). Click the **Company Code** button at the top. Enter `MAK1`. In the Account Management tab, type `100500` in the Reconciliation Account field. Save.

---

## Phase 4: Payment Terms Configuration (Unit 7 Assignment)

### Assignment Prompt:
> *"Create payment terms with 0.5% in 10 days, 0.2% in 30 days and 45-days net. Assign to vendor/customer."*

**Explanation for Beginners**:
If a customer pays us early, we want the system to automatically calculate a small discount to encourage fast payment.

### Step-by-Step Configuration:
**1. Create the Rule**
*   **T-Code**: `OBB8`
*   **Action**: Click **New Entries**. Name it `PT45`. 
*   Check both **Customer** and **Vendor** boxes.
*   Set Default for Baseline Date to **Document Date** (The clock starts ticking on the invoice date).
*   Under Payment terms:
    *   Term 1: `0.5` % in `10` days.
    *   Term 2: `0.2` % in `30` days.
    *   Term 3: `45` days (leave % blank). Save.

**2. Assign to Business Partner**
*   **Action**: Go back to T-Code `BP`. Open your partner `BP9001` in role `FLCU00` (Customer). Click Company Code. Go to the **Payment Transactions** tab. Type `PT45` in the Terms of Payment field. Save.

---

## Phase 5: Day-to-Day Postings (Unit 6 & 9 Assignments)

### Assignment Prompt:
> *"Post customer down payment (FBA2), post customer Invoice against down payment (F-22/FB70), clear Invoice against down payment (F-39). Post regular transactions (FB70/FB60)."*

**Explanation for Beginners**:
The system is fully built! Now we act as the end-user (the accountant) to process daily paperwork. A **Down Payment** is a "Special GL" transaction—meaning the customer gives us cash *before* we issue the invoice, so it must hit a special liability account instead of the normal Accounts Receivable account.

### Step-by-Step Configuration:

**1. Receive a Down Payment from the Customer**
*   **T-Code**: `FBA2` (or `F-29`).
*   **Action**: Customer `BP9001` wires us $5,000 in advance. Enter the Customer ID. Enter Special GL Indicator **`A`** (This tells SAP: "Hey, this is an advance, route it to the liability account!"). Enter your Bank GL account and the $5,000 amount. Save/Post.

**2. Post the Regular Customer Invoice**
*   **T-Code**: `FB70`
*   **Action**: We finally deliver the goods and bill them for $10,000. Enter Customer `BP9001`, amount `$10,000`, and a Revenue GL account. 
*   *(Notice that on the Payment tab, your `PT45` rule automatically populated!)*
*   Simulate and Post. You will likely see a yellow warning: "Down payments exist for this customer". Press Enter to bypass it.

**3. Clear the Down Payment against the Invoice**
*   **T-Code**: `F-39`
*   **Action**: The customer owes us $10,000, but we already have their $5,000. We use `F-39` to match them together. Enter Customer `BP9001` and the Invoice Document Number. Select the $5,000 down payment. Save. The system nets the balances, leaving exactly $5,000 open for the customer to pay later.

---
**Congratulations!** By following these steps sequentially, you have learned exactly how a global enterprise structures its backend, protects its data, builds its masters, and processes its daily cashflow in SAP S/4HANA.
