# Accenture Stream Training: SAP S/4HANA Finance
## Unit 11: Dunning Program

Welcome to your study guide and reference documentation for **Unit 11: Dunning Program**. 

---

## 1. Assignment: Dunning Program

**Objective**: Configure the system to automatically send warning letters (dunning notices) to customers who have overdue invoices.

### Step 1: Maintain the end-to-end configuration for Dunning procedure
*   **Path**: `SPRO > SAP Reference IMG > Financial Accounting > Accounts Receivable and Accounts Payable > Business Transactions > Dunning > Dunning Procedure > Define Dunning Procedures`
*   **T-Code**: `FBMP` (Often configured via SPRO path)
*   **Action**: 
    1. Create a Dunning Procedure (e.g., `Z001`).
    2. Define the **Dunning Intervals** (e.g., send a letter every 14 days).
    3. Define the **Number of Dunning Levels** (e.g., 3 levels. Level 1 is a gentle reminder, Level 3 is a final legal warning).
    4. Set up **Dunning Charges** (e.g., adding a $10 late fee at Level 2).
    5. Assign **Dunning Texts/Forms** so the system knows what PDF template to print for each level.

### Step 2: Assign Dunning Procedure to Customer Master
*   **Context**: The system needs to know which customers should receive letters.
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Customers > Master Records > BP - Maintain Business Partner`
*   **T-Code**: `BP`
*   **Action**: Open the Customer in role `FLCU00`. Go to the **Correspondence** tab and assign your new Dunning Procedure (`Z001`).

### Step 3: Execution of Dunning program
*   **Path**: `SAP Easy Access > Accounting > Financial Accounting > Accounts Receivable > Periodic Processing > F150 - Dunning`
*   **T-Code**: `F150`
*   **Action**: 
    1. Enter a **Run Date** and **Identification** code.
    2. In the **Parameters** tab, enter the Dunning Date, Documents posted up to date, Company Code, and the Customer range.
    3. Run the **Dunning Proposal** to let SAP identify all overdue invoices.
    4. Review the Dunning List.
    5. Execute the **Dunning Print Run** to physically generate the PDF warning letters.
