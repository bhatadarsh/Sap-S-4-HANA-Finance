# Accenture Stream Training: SAP S/4HANA Finance
## Unit 12: Correspondence

Welcome to your study guide and reference documentation for **Unit 12: Correspondence**. 

---

## 1. Assignment: Maintain correspondence for customer account

**Objective**: Configure the system to generate an account statement that you can send to a customer showing all their open and cleared items.

### Step 1: Configure Correspondence Type
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Accounts Receivable and Accounts Payable > Customer Accounts > Line Items > Correspondence > Make and Check Settings for Correspondence > Define Correspondence Types`
*   **Action**: SAP provides standard correspondence types. Check type `SAP06` (Customer Statement). Ensure the settings for mandatory fields and dates are configured according to your business needs.

### Step 2: Assign Programs for Correspondence Type
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Accounts Receivable and Accounts Payable > Customer Accounts > Line Items > Correspondence > Assign Programs for Correspondence Types`
*   **Action**: Assign the standard print program (e.g., `RFKORD11`) to correspondence type `SAP06`.

### Step 3: Define Form Names
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Accounts Receivable and Accounts Payable > Customer Accounts > Line Items > Correspondence > Define Form Names for Correspondence Print`
*   **Action**: Map the standard SAPscript or PDF form to your Company Code and correspondence type `SAP06`.

### Step 4: Create Customer Invoices
*   **T-Code**: `FB70`
*   **Action**: Post a few standard invoices to ensure the customer has open items to display on the statement.

### Step 5: Request the Account Statement
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Accounts Receivable > Periodic Processing > Print Correspondence > F.12 - As per Requests`
*   **T-Code**: `F.12` (Note: F.12 is for mass requests, `FB12` is for requesting a statement for a single customer).
*   **Action**: Enter the Company Code, Customer number, and select correspondence type `SAP06`. This tells SAP you *want* a statement, but it doesn't print it yet.

### Step 6: Print the Output
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Accounts Receivable > Periodic Processing > Print Correspondence > F.64 - Maintain`
*   **T-Code**: `F.64`
*   **Action**: Execute the transaction to view all requested correspondence. Select your request and execute the print run. This pushes the statement to the spooler (`SP01`) where you can view the PDF.
