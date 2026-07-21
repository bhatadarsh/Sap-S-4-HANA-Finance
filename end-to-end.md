# SAP S/4HANA Finance: End-to-End Implementation Guide

This guide is designed to take you from a completely blank system to a fully functioning financial operation capable of posting customer down payments and running recurring batches. It synthesizes all individual topics from Unit 2 through Unit 9 into a single, cohesive project.

## The Business Scenario: "MAK9 Group"
To make these instructions concrete, we will configure a fictitious global enterprise called **MAK9 Group**. Use the exact codes provided below so that every subsequent step works seamlessly.

**Master Data Cheat Sheet:**
*   **Company**: `MAK9` (MAK9 Group)
*   **Company Codes**: `MAK1` (US Operations), `MAK2` (EU Operations)
*   **Credit Control Area / FM Area / Chart of Accounts**: `MAK9`
*   **Fiscal Year Variant**: `K4` (Calendar Year)
*   **Retained Earnings**: `100100` | **Zero-Balance Clearing**: `100110` | **Share Capital**: `100000`
*   **Business Partner**: `BP9001`
*   **Payment Term**: `PT45`

---

## Phase 1: Enterprise Structure (Unit 2)
*Goal: Build the legal and organizational skeleton of MAK9 Group.*

### 1. Define the Company
*   **T-Code**: `OX15`
*   **Action**: Click **New Entries**. Enter Company `MAK9`, Company Name `MAK9 Group`. Fill in address details and Save.

### 2. Define Company Codes
*   **T-Code**: `OX02`
*   **Action**: Click **New Entries**. Create `MAK1` (Name: MAK9 US, Country: US, Currency: USD). Create a second entry `MAK2` (Name: MAK9 EU, Country: DE, Currency: EUR).

### 3. Define Credit Control & Financial Management Areas
*   **T-Code**: `OB45` (Credit Control) & `OF01` (FM Area)
*   **Action**: Create Credit Control Area `MAK9` (Currency: USD) and FM Area `MAK9`.

### 4. Define Segments and Profit Centers
*   **T-Code**: `KE51`
*   **Action**: Create a Profit Center `PC_MAK9` (ensure you assign it to the correct controlling area if prompted).

### 5. Assignments (Linking it all together)
*   **Company Code to Company (`OX16`)**: Assign `MAK1` and `MAK2` to Company `MAK9`.
*   **Company Code to Credit Control Area (`OB38`)**: Assign `MAK1` and `MAK2` to `MAK9`.
*   **Company Code to FM Area (`OFA2`)**: Assign `MAK1` and `MAK2` to `MAK9`.

---

## Phase 2: Global Financial Settings (Unit 3)
*Goal: Establish the accounting rules (Dates, Numbers, Tolerances).*

### 1. Fiscal Year & Posting Periods
*   **T-Code**: `OB37` (Assign Fiscal Year) & `OBBP` (Assign Posting Period Variant).
*   **Action**: Assign the standard SAP Calendar Year variant **`K4`** to both `MAK1` and `MAK2`. Create a Posting Period Variant `MAK9` and assign it to your company codes.

### 2. Document Number Ranges
*   **T-Code**: `FBN1`
*   **Action**: For Company Code `MAK1`, create an interval for standard documents (e.g., Interval `01`, Year `2026`, From `100000` to `199999`).

### 3. Field Status Variant
*   **T-Code**: `OBC4` (Define) & `OBC5` (Assign)
*   **Action**: Copy standard variant `0001` to `MAK9`. Assign variant `MAK9` to Company Codes `MAK1` and `MAK2`.

### 4. Tolerance Groups
*   **T-Code**: `OBA4` (Define) & `OB57` (Assign to User)
*   **Action**: Create a blank tolerance group for company code `MAK1` to apply to all users by default. Set upper limits for posting amounts and cash discount percentages (e.g., 5%).

### 5. Tax Configuration
*   **T-Code**: `OBBG` (Assign Country to Calculation Procedure)
*   **Action**: Ensure country `US` or `IN` is assigned to standard tax procedures (like `TAXUS` or `TAXINN`).

---

## Phase 3: Master Data Foundation (Unit 4 & 8)
*Goal: Create the Chart of Accounts, GL Accounts, and Business Partners.*

### 1. Chart of Accounts & Account Groups
*   **T-Code**: `OB13` (Define COA) & `OB62` (Assign COA) & `OBD4` (Account Groups).
*   **Action**: 
    1. Define Chart of Accounts `MAK9`. Assign it to `MAK1` and `MAK2`.
    2. Go to `OBD4` and define Account Groups for `MAK9` (e.g., `LIAB` for Liabilities 100000-199999, `ASST` for Assets 200000-299999).

### 2. Define Retained Earnings Account
*   **T-Code**: `OB53`
*   **Action**: For COA `MAK9`, enter P&L statement account type `X` and assign it to GL account `100100`.

### 3. Create General Ledger Accounts
*   **T-Code**: `FS00`
*   **Action**: 
    1. Create `100000` (Share Capital) as a Balance Sheet Account.
    2. Create `100100` (Retained Earnings) as a Balance Sheet Account.
    3. Create `100110` (Zero Balance Clearing) as a Balance Sheet Account.
    4. Create `100500` (Accounts Receivable Recon) and set the Recon. Account for Acct Type to **Customers**.

### 4. Create Business Partner
*   **T-Code**: `BP`
*   **Action**: 
    1. Create a General BP (Role `000000`) for "Global Tech Supplies". Note the BP number `BP9001`.
    2. Switch to role `FLCU00` (FI Customer), click Company Code, enter `MAK1`, and assign the Reconciliation Account `100500`.
    3. Save the customer profile.

---

## Phase 4: Advanced Configuration (Unit 5 & 7)
*Goal: Enable Document Splitting and Custom Payment Terms.*

### 1. Document Splitting Configuration
*   **Action**: 
    1. Navigate in SPRO to `Financial Accounting > General Ledger > Business Transactions > Document Splitting > Classify G/L Accounts`. Map account range `100000` to `199999` to Item Category `01000` (Balance Sheet).
    2. Go to `Define Zero-Balance Clearing Account`. Under account key `000`, assign your GL account `100110`.

### 2. Maintain Payment Terms
*   **T-Code**: `OBB8`
*   **Action**: Create Payment Term `PT45`. Set Default Baseline Date to **Document Date**. Set Term 1 to 0.5% in 10 days, Term 2 to 0.2% in 30 days, and Term 3 to 45 Days Net. Check both Customer and Vendor boxes.
*   **Action 2**: Go back to `BP`, open `BP9001` in Customer role `FLCU00`, and under the Payment Transactions tab, assign term `PT45`.

---

## Phase 5: Day-to-Day Operations & Testing (Unit 6 & 9)
*Goal: Prove the system works by running real business scenarios.*

### Scenario A: Standard Posting and Reversal
1.  **Post GL Document (`FB50`)**: Debit `100000` and Credit another asset account.
2.  **Reverse Document (`FB08`)**: Take the document number generated in step 1, enter it here, use reversal reason `01`, and post.

### Scenario B: Maker-Checker Document Parking
1.  **Park Document (`FV50` or `FB50 > Park`)**: Enter a journal entry but click **Park**. Write down the document number.
2.  **Approve/Post (`FBV0`)**: Open the parked document number. Review it, then click **Post** to officially hit the ledger.

### Scenario C: Customer Down Payments & Clearing
1.  **Down Payment (`FBA2` or `F-29`)**: Customer `BP9001` gives you a cash advance. Post it using Special GL indicator `A`.
2.  **Customer Invoice (`FB70`)**: You deliver the goods. Post a $10,000 invoice for customer `BP9001`. (Notice the `PT45` payment terms default automatically!).
3.  **Clear the Down Payment (`F-39`)**: The customer has an open advance and an open invoice. Use `F-39` to match the down payment against the invoice, clearing the balances. 

### Scenario D: Recurring Documents
1.  **Define Number Range (`FBN1`)**: Create interval `X1` for recurring documents.
2.  **Create Template (`FBD1`)**: Create a monthly rent posting template for the next 12 months.
3.  **Execute Template (`F.14`)**: Run the batch program to instruct SAP to look at your template and post this month's actual rent expense.

---
**Congratulations!** You have configured a global enterprise from scratch, established its master data, defined advanced accounting rules, and executed a full lifecycle of financial transactions.
