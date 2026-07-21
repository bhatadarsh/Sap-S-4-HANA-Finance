# Accenture Stream Training: SAP S/4HANA Finance
## Unit 8: Business Partner Master

Welcome to your study guide and reference documentation for **Unit 8: Business Partner Master**. This document provides a walkthrough of the hands-on exercises for creating and extending Business Partners, a core architectural change in SAP S/4HANA.

---

## 1. Assignment: Business Partner

**Objective**: Create a centralized Business Partner (BP) master record and extend it to function as both an FI Vendor and an FI Customer.

### Step 1: Create a General Business Partner Master Record
*   **T-Code**: `BP` (Maintain Business Partner)
*   **Action**: 
    1. Click on **Organization** to create a corporate partner.
    2. Select the BP Role: `000000` (Business Partner - General). This role is mandatory and stores basic, globally relevant data (Name, Address, Communication details).
    3. Fill in the required fields (Name, Search Term, Address, Country, Language).
    4. Click **Save**. The system generates a central BP number.

### Step 2: Extend to FI Customer BP
*   **Action**: 
    1. Remain in the `BP` transaction, viewing the partner you just created.
    2. Click the **Switch Between Display and Change** button.
    3. In the "Change in BP Role" dropdown, select **`FLCU00` (FI Customer)**.
    4. Click on the **Company Code** button at the top of the screen.
    5. Enter your Company Code (e.g., `MAK9`) and press Enter.
    6. Fill in the mandatory FI Customer data (e.g., Reconciliation Account, Sort Key) on the Account Management tab.
    7. Save the record. You have now extended the BP to act as a Customer in your company code.

### Step 3: Extend to FI Vendor BP
*   **Action**: 
    1. Still in the `BP` transaction in change mode.
    2. Change the BP Role dropdown to **`FLVN00` (FI Vendor)**.
    3. Click on the **Company Code** button.
    4. Ensure your Company Code is selected.
    5. Fill in the mandatory FI Vendor data (e.g., Vendor Reconciliation Account on the Account Management tab, Payment Terms on the Payment Transactions tab).
    6. Save the record. Your single Business Partner can now act as both a buyer and a seller for your organization.

---

## 2. Topics Covered Today (Concepts)

*   **The Single Point of Entry (BP vs. FK01/FD01)**: In older SAP ECC versions, you had to use different transactions to create a Vendor (`FK01`) and a Customer (`FD01`). In S/4HANA, the `BP` transaction is the single point of entry. You create one central entity and simply assign "Roles" to it.
*   **BP Roles**:
    *   **`000000` (General Data)**: Name, Address, Bank details. Shared across all modules.
    *   **`FLCU00` (FI Customer)**: Adds Company Code specific data for Accounts Receivable (Reconciliation account, payment terms).
    *   **`FLCU01` (Sales Customer)**: Adds Sales Area data for SD integration.
    *   **`FLVN00` (FI Vendor)**: Adds Company Code specific data for Accounts Payable.
    *   **`FLVN01` (Purchasing Vendor)**: Adds Purchasing Organization data for MM integration.
*   **Reconciliation Accounts**: When extending a BP to FI Customer or FI Vendor, assigning a Reconciliation Account is mandatory. This is a special GL account (e.g., Accounts Receivable or Accounts Payable) that cannot be posted to directly. Every time an invoice is posted to the Business Partner, SAP automatically updates this summary GL account in real-time.
