# Accenture Stream Training: SAP S/4HANA Finance
## Unit 10: Automatic Payment Program (APP)

Welcome to your study guide and reference documentation for **Unit 10: Automatic Payment Program**. This document provides a walkthrough of the hands-on exercises for Unit 10, focusing on configuring the APP via `FBZP` and executing payment runs via `F110`.

---

## 1. Assignment: Automatic Payment Program

**Objective**: Configure the rules that allow SAP to automatically pay hundreds of vendors at once, rather than paying them manually one by one.

### Step 1: Maintain the Configuration for One Payment Method
*   **Context**: You must tell SAP exactly how you want to pay (e.g., Check, Bank Transfer) and the rules for that method.
*   **Path**: `SPRO > Financial Accounting > Accounts Receivable and Accounts Payable > Business Transactions > Outgoing Payments > Automatic Outgoing Payments > Payment Method/Bank Selection > Set Up Payment Methods per Country for Payment Transactions`
*   **T-Code**: `FBZP` (Click the **Payment Methods in Country** button).
*   **Action**: Create a Payment Method (e.g., `C` for Check or `T` for Transfer) for your Country (e.g., `US`). Define the minimum and maximum amounts allowed for this method.

### Step 2: Define House Bank and Bank Accounts
*   **Context**: A House Bank is your company's actual, physical bank (e.g., CitiBank, JP Morgan) configured within SAP.
*   **T-Code**: `FI12` (or via `FBZP` > **House Banks**).
*   **Action**: 
    1. Select your Company Code.
    2. Create a House Bank ID (e.g., `CITI`).
    3. Enter the Bank Key (Routing Number).
    4. Create an Account ID (e.g., `OPR1` for Operations Account) and link it to the specific G/L Account you created for this bank.

### Step 3: Maintain Ranking Order Configuration
*   **Context**: If you have multiple bank accounts, you must tell SAP which one to draw money from first.
*   **Path**: `FBZP` > **Bank Determination** button.
*   **Action**: 
    1. Select your Company Code.
    2. Go to **Ranking Order**: Select your Payment Method and rank your House Bank (e.g., Rank 1 = `CITI`).
    3. Go to **Bank Accounts**: Link the House Bank, Payment Method, and Account ID, and assign the Bank Subaccount G/L.
    4. Go to **Available Amounts**: Tell SAP the maximum amount of money it is allowed to draw from this bank account during an automatic payment run.

### Step 4: Execute Automatic Payment Program
*   **Context**: Once configured, you can run the program to pay all open vendor invoices that are due.
*   **T-Code**: `F110`
*   **Action**: 
    1. Enter a **Run Date** and a **Identification** code (e.g., `MAK1A`).
    2. Go to the **Parameters** tab: Enter your Company Code, Payment Method, Next Posting Date, and the Vendor range you want to pay.
    3. Go to the **Proposal** tab to run a simulation. Check the Proposal Log to ensure the invoices were picked up successfully without errors (like missing payment terms or bank details).
    4. Execute the **Payment Run**. This physically clears the open vendor invoices and posts the payment document to the bank clearing G/L account.

---

## 2. Topics Covered Today (Concepts)

*   **Manual vs. Automatic (`F-53` vs `F110`)**: 
    *   `F-53` is used for **Manual Payments** (paying a single vendor manually). 
    *   `F110` is the **Automatic Payment Program (APP)**, used to process mass payments to thousands of vendors simultaneously based on due dates and payment terms.
*   **The Power of `FBZP`**: This is one of the most critical transaction codes in SAP FI. It controls all 6 major steps of APP configuration: All Company Codes, Paying Company Codes, Payment Methods in Country, Payment Methods in Company Code, Bank Determination, and House Banks.
