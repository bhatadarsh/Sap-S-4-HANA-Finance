# Accenture Stream Training: SAP S/4HANA Finance
## Unit 9: Special GL and Regular Transactions

Welcome to your study guide and reference documentation for **Unit 9: Special GL and Regular Transactions**. This document provides a walkthrough of the hands-on exercises for Unit 9, focusing on day-to-day invoice processing and managing down payments (Special GL transactions).

---

## 1. Assignment: Special GL and Regular Transactions

**Objective**: Master the end-to-end process of customer down payments and standard AR/AP invoice processing.

### Step 1: Post Regular Transactions (Invoices)
*   **Action (Customer Invoice)**: 
    1. Use T-Code **`FB70`** (Enter Customer Invoice).
    2. Enter the Customer ID, Invoice Date, Amount, and the offsetting Revenue GL account.
    3. Simulate and **Post**. This updates the customer's open receivables.
*   **Action (Vendor Invoice)**: 
    1. Use T-Code **`FB60`** (Enter Vendor Invoice).
    2. Enter the Vendor ID, Invoice Date, Amount, and the offsetting Expense GL account.
    3. Simulate and **Post**. This updates your open payables.

### Step 2: Post a Customer Down Payment
*   **Context**: A customer pays you in advance before you have issued an invoice. This is a "Special GL" transaction because it should not hit your standard Accounts Receivable reconciliation account; it must hit a special Liability account (Advances Received).
*   **T-Code**: `FBA2` (Post Customer Down Payment) or `F-29`.
*   **Action**: 
    1. Enter Document Date and Customer ID.
    2. Enter the **Special G/L Indicator** (usually `A` for Down Payment). This indicator tells SAP to route the posting to the alternative reconciliation account.
    3. Enter the Bank Account receiving the cash and the amount.
    4. Post the document.

### Step 3: Post Customer Invoice Against Down Payment
*   **Context**: You now deliver the goods/services and issue the actual invoice.
*   **T-Code**: `F-22` (Enter Customer Invoice - General) or `FB70`.
*   **Action**: 
    1. Post the invoice for the total amount of the sale just like you did in Step 1.
    2. *Note*: In a real scenario, SAP will display a warning message: "Down payments exist for this customer", prompting the user to clear them.

### Step 4: Clear Invoice Against Customer Down Payment
*   **Context**: The customer has an open Invoice (Debit) and an open Down Payment (Credit) on their account. You must link them together to clear the balance.
*   **T-Code**: `F-39` (Clear Customer Down Payment).
*   **Action**: 
    1. Enter the Customer ID and the Invoice document number you want to clear against.
    2. Select the down payment to be cleared.
    3. The system moves the down payment from the Special GL (Advances) to the standard GL (Accounts Receivable) and matches it against the invoice, clearing both open items.

---

## 2. Topics Covered Today (Concepts)

*   **Regular Transactions (`FB60`/`FB70`)**: These are single-screen, enjoy-transactions designed for fast data entry of simple AP/AR invoices without needing to remember posting keys (`40`, `50`, `31`, `01`). 
*   **Special GL Transactions**: Standard postings to a BP automatically update their assigned Reconciliation Account. However, certain transactions (Down Payments, Guarantees, Bills of Exchange) need to be reported separately on the balance sheet. **Special GL Indicators** (like `A`) intercept the posting and route it to an *Alternative Reconciliation Account*.
*   **The Down Payment Lifecycle**:
    1. **Receive Cash**: Bank (Dr) / Special GL Advance (Cr).
    2. **Issue Invoice**: Standard AR (Dr) / Revenue (Cr).
    3. **Clearing (`F-39`)**: Special GL Advance (Dr) / Standard AR (Cr). This nets the accounts receivable balance to zero and eliminates the liability of the advance.
