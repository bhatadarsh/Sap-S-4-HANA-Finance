# SAP S/4HANA Finance: Beginner's End-to-End Implementation Guide

Welcome to your master implementation guide! This document is designed specifically for beginners. It takes all the individual assignments you've been given from **Unit 2 through Unit 9** and strings them together into one continuous, logical project.

Instead of just telling you *what* to click, this guide explains *why* you are clicking it. We will use a consistent set of fictitious data (The "MAK9 Group") so that every assignment builds perfectly on top of the previous one. Every step contains both the **Navigation Path** and the **Transaction Code (T-Code)**.

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
*   **Path**: `SPRO > SAP Reference IMG > Enterprise Structure > Definition > Financial Accounting > Define company`
*   **T-Code**: `OX15`
*   **Action**: Click **New Entries**.
*   **Type this**: 
    *   Company: `MAK9`
    *   Company Name: `MAK9 Group`
    *   Fill in any mock address/country data and click **Save**.

**2. Create 2 Company Codes**
*   **Path**: `SPRO > SAP Reference IMG > Enterprise Structure > Definition > Financial Accounting > Edit, Copy, Delete, Check Company Code`
*   **T-Code**: `OX02`
*   **Action**: Click **New Entries**.
*   **Type this (First CC)**: Company Code `MAK1`, Name `MAK9 US`, Country `US`, Currency `USD`. Save.
*   **Type this (Second CC)**: Company Code `MAK2`, Name `MAK9 EU`, Country `DE`, Currency `EUR`. Save.

**3. Create 2 Business Areas**
*   **Path**: `SPRO > SAP Reference IMG > Enterprise Structure > Definition > Financial Accounting > Define Business Area`
*   **T-Code**: `OX03`
*   **Action**: Click **New Entries**.
*   **Type this**: 
    *   `MAKB` - MAK9 Bikes Division
    *   `MAKH` - MAK9 Helmets Division

**4. Assign Company Codes to the Company**
*   **Path**: `SPRO > SAP Reference IMG > Enterprise Structure > Assignment > Financial Accounting > Assign company code to company`
*   **T-Code**: `OX16`
*   **Action**: Find `MAK1` in the list, and in the "Company" column next to it, type `MAK9`. Do the same for `MAK2`. Save. *(Why? This links the regional branches to the parent group for consolidated reporting).*

---

## Phase 2: Global Financial Settings (Unit 3 Assignments)

### Assignment Prompt:
> *"Create new document type to post vendor invoice. Define parameters. Create number range. Create new Field status group variant. Define new tolerance group and assign to user."*

**Explanation for Beginners**:
Now that the skeleton exists, we must define the rules of accounting for `MAK1` and `MAK2`.
*   **Fiscal Year & Posting Periods**: Does your financial year run Jan-Dec or April-March?
*   **Document Types & Number Ranges**: Every time you save a journal entry, SAP assigns it a unique ID number. We must tell SAP what number to start counting from (e.g., 100000 to 199999).
*   **Field Status Variant**: Controls whether fields on a screen are mandatory, optional, or hidden when a user is typing an invoice.
*   **Tolerance Groups**: Security limits. It prevents a junior accountant from posting a billion-dollar invoice by accident.

### Step-by-Step Configuration:

**1. Assign Fiscal Year**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Ledgers > Fiscal Year and Posting Periods > Assign Company Code to a Fiscal Year Variant`
*   **T-Code**: `OB37` 
*   **Action**: Assign the standard SAP Calendar Year variant **`K4`** to both `MAK1` and `MAK2`. 

**2. Assign Posting Period Variant**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Ledgers > Fiscal Year and Posting Periods > Posting Periods > Assign Variants to Company Code`
*   **T-Code**: `OBBP`
*   **Action**: Create a variant `MAK9` and assign it to `MAK1` and `MAK2`.

**3. Create Document Number Range**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Document > Document Number Ranges > Define Document Number Ranges`
*   **T-Code**: `FBN1`
*   **Action**: Enter Company Code `MAK1`. Click the **Intervals (Pencil)** icon. 
*   **Type this**: No: `01`, Year: `2026`, From No: `100000`, To Number: `199999`. Save.

**4. Create Field Status Variant**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Ledgers > Fields > Define Field Status Variants`
*   **T-Code**: `OBC4` 
*   **Action**: Highlight the standard SAP variant `0001` and click the **Copy As** button. Name your copy `MAK9`. Save. 

**5. Assign Field Status Variant**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Ledgers > Fields > Assign Company Code to Field Status Variants`
*   **T-Code**: `OBC5`
*   **Action**: Type `MAK9` next to Company Codes `MAK1` and `MAK2`.

**6. Define Tolerance Group**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Document > Tolerance Groups > Define Tolerance Groups for Employees`
*   **T-Code**: `OBA4`
*   **Action**: Click **New Entries**. Enter Company Code `MAK1`. *Leave the Tolerance Group name blank* (this makes it the default for everyone). Set the "Amount per document" to `999,999,999` and Cash Discount to `5%`. Save.

**7. Assign Tolerance Group to User**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Financial Accounting Global Settings > Document > Tolerance Groups > Assign User/Tolerance Groups`
*   **T-Code**: `OB57`
*   **Action**: Enter your SAP username, and leave the tolerance group blank so it picks up the default you just created.

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
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > General Ledger Accounting > Master Data > G/L Accounts > Preparations > Edit Chart of Accounts List`
*   **T-Code**: `OB13`
*   **Action**: Create COA `MAK9`. Length of GL Account Number: `6`. Save. 

**2. Assign Chart of Accounts**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > General Ledger Accounting > Master Data > G/L Accounts > Preparations > Assign Company Code to Chart of Accounts`
*   **T-Code**: `OB62`
*   **Action**: Assign `MAK9` to `MAK1` and `MAK2`.

**3. Define Account Groups**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > General Ledger Accounting > Master Data > G/L Accounts > Preparations > Define Account Group`
*   **T-Code**: `OBD4` 
*   **Action**: Create groups for `MAK9`: e.g., `ASST` (Assets: 100000-199999) and `LIAB` (Liabilities: 200000-299999). 

**4. Define Retained Earnings Account**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > General Ledger Accounting > Master Data > G/L Accounts > Preparations > Define Retained Earnings Account`
*   **T-Code**: `OB53`
*   **Action**: Enter COA `MAK9`. Type P&L Statement Account type: `X`. Type Account: `100100`. (Ignore the warning that the account doesn't exist yet, press enter to save).

**5. Create GL Accounts Centrally**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > General Ledger > Master Records > G/L Accounts > Individual Processing > FS00 - Centrally`
*   **T-Code**: `FS00`
*   **Action**: Open `FS00`. Ensure Company Code is `MAK1`. 
    *   Create `100100` as a Balance Sheet account (Retained Earnings). 
    *   Create `100500` as a Balance Sheet account. In the "Control Data" tab, set **Recon. Account for Acct Type** to **Customers**. *(Why? We cannot post directly to a customer account; SAP posts to this Recon GL in the background automatically).*

**6. Create the Business Partner**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Customers > Master Records > BP - Maintain Business Partner`
*   **T-Code**: `BP`
*   **Action**: 
    *   **Role 1**: Click **Organization**. Select role `000000` (General). Type name "Global Tech Supplies". Save. Write down the BP Number (e.g., `BP9001`).
    *   **Role 2**: Change the dropdown role to `FLCU00` (FI Customer). Click the **Company Code** button at the top. Enter `MAK1`. In the Account Management tab, type `100500` in the Reconciliation Account field. Save.

---

## Phase 4: Payment Terms Configuration (Unit 7 Assignment)

### Assignment Prompt:
> *"Create payment terms with 0.5% in 10 days, 0.2% in 30 days and 45-days net. Assign to vendor/customer."*

**Explanation for Beginners**:
If a customer pays us early, we want the system to automatically calculate a small discount to encourage fast payment.

### Step-by-Step Configuration:
**1. Create the Rule**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Accounts Receivable and Accounts Payable > Business Transactions > Incoming Invoices/Credit Memos > Maintain Terms of Payment`
*   **T-Code**: `OBB8`
*   **Action**: Click **New Entries**. Name it `PT45`. 
*   Check both **Customer** and **Vendor** boxes.
*   Set Default for Baseline Date to **Document Date** (The clock starts ticking on the invoice date).
*   Under Payment terms:
    *   Term 1: `0.5` % in `10` days.
    *   Term 2: `0.2` % in `30` days.
    *   Term 3: `45` days (leave % blank). Save.

**2. Assign to Business Partner**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Customers > Master Records > BP - Maintain Business Partner`
*   **T-Code**: `BP`
*   **Action**: Open your partner `BP9001` in role `FLCU00` (Customer). Click Company Code. Go to the **Payment Transactions** tab. Type `PT45` in the Terms of Payment field. Save.

---

## Phase 5: Day-to-Day Postings (Unit 6 & 9 Assignments)

### Assignment Prompt:
> *"Post customer down payment (FBA2), post customer Invoice against down payment (F-22/FB70), clear Invoice against down payment (F-39). Post regular transactions (FB70/FB60)."*

**Explanation for Beginners**:
The system is fully built! Now we act as the end-user (the accountant) to process daily paperwork. A **Down Payment** is a "Special GL" transaction—meaning the customer gives us cash *before* we issue the invoice, so it must hit a special liability account instead of the normal Accounts Receivable account. Note that for daily operations, we do not use the SPRO configuration menu; we use the SAP Easy Access menu.

### Step-by-Step Configuration:

**1. Receive a Down Payment from the Customer**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Customers > Document Entry > Down Payment > F-29 - Down Payment`
*   **T-Code**: `FBA2` (or `F-29`).
*   **Action**: Customer `BP9001` wires us $5,000 in advance. Enter the Customer ID. Enter Special GL Indicator **`A`** (This tells SAP: "Hey, this is an advance, route it to the liability account!"). Enter your Bank GL account and the $5,000 amount. Save/Post.

**2. Post the Regular Customer Invoice**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Customers > Document Entry > FB70 - Invoice`
*   **T-Code**: `FB70`
*   **Action**: We finally deliver the goods and bill them for $10,000. Enter Customer `BP9001`, amount `$10,000`, and a Revenue GL account. 
*   *(Notice that on the Payment tab, your `PT45` rule automatically populated!)*
*   Simulate and Post. You will likely see a yellow warning: "Down payments exist for this customer". Press Enter to bypass it.

**3. Clear the Down Payment against the Invoice**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Customers > Document Entry > Down Payment > F-39 - Clearing`
*   **T-Code**: `F-39`
*   **Action**: The customer owes us $10,000, but we already have their $5,000. We use `F-39` to match them together. Enter Customer `BP9001` and the Invoice Document Number. Select the $5,000 down payment. Save. The system nets the balances, leaving exactly $5,000 open for the customer to pay later.

---

## Phase 6: Automatic Payment Program (Unit 10 Assignment)

### Assignment Prompt:
> *"Maintain the configuration for one payment method. Define house bank and bank accounts. Maintain ranking order configuration. Execute Automatic Payment program. Execute manual payment transaction."*

**Explanation for Beginners**:
Instead of paying 500 vendors manually one-by-one (`F-53`), SAP's Automatic Payment Program (APP) can pay all 500 at once. To do this, we must configure our physical bank (House Bank) in SAP and set up the rules for how we pay (e.g., Check or Transfer).

### Step-by-Step Configuration:

**1. Define House Bank and Bank Accounts**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Bank Accounting > Bank Accounts > Define House Banks`
*   **T-Code**: `FI12`
*   **Action**: 
    1. Select Company Code `MAK1`.
    2. Create House Bank ID `CITI`. Enter Bank Key (Routing Number).
    3. Double click **Bank Accounts**. Create Account ID `OPR1`. Link it to the G/L Account you created for this bank.

**2. Configure Automatic Payment Program (APP)**
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Accounts Receivable and Accounts Payable > Business Transactions > Outgoing Payments > Automatic Outgoing Payments > Payment Method/Bank Selection > Set Up Payment Methods per Country for Payment Transactions`
*   **T-Code**: `FBZP`
*   **Action**: 
    1. Click **Payment Methods in Country**: Create Method `C` (Check) for Country `US`.
    2. Click **Bank Determination**: Select Company Code `MAK1`. 
       *   Under **Ranking Order**, rank your House Bank `CITI` as `1` for Method `C`.
       *   Under **Bank Accounts**, link House Bank `CITI`, Method `C`, Account ID `OPR1`, and the Bank Subaccount G/L.

**3. Execute the Payment Run**
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Accounts Payable > Periodic Processing > F110 - Payments`
*   **T-Code**: `F110`
*   **Action**: 
    1. Enter a **Run Date** (today) and an **Identification** (e.g., `MAK1A`).
    2. Go to **Parameters**: Enter Company Code `MAK1`, Payment Method `C`, Next Posting Date, and the Vendor ID (`BP9001`).
    3. Go to **Proposal**: Run a simulation to ensure invoices are picked up.
    4. Click **Payment Run** to execute and pay the vendor!

---
**Congratulations!** By following these steps sequentially, you have learned exactly how a global enterprise structures its backend, protects its data, builds its masters, processes daily cashflow, and pays vendors in bulk in SAP S/4HANA.
