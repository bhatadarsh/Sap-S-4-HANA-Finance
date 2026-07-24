# Accenture Stream Training: SAP S/4HANA Finance
## Unit 13: MM and SD Integration

Welcome to your study guide and reference documentation for **Unit 13: MM and SD Integration**. 

---

## 1. Assignment: Explain MM and SD Integration

**Objective**: Understand how the logistics modules (Materials Management and Sales & Distribution) automatically post financial documents to the General Ledger without manual accounting entry.

### Part 1: Explain MM Integration (Procure-to-Pay)
Materials Management handles the purchasing of goods. When goods are received in the warehouse, the system must recognize an increase in inventory (Asset) and an unbilled liability.

*   **The T-Code**: `OBYC` (Automatic Account Determination for Inventory Management).
*   **How it works**: SAP uses a combination of the material's **Valuation Class** and a specific **Transaction Key** to find the correct G/L account.
*   **Key Transaction Keys**:
    *   **BSX**: Inventory Posting (Maps to Inventory Asset G/L)
    *   **WRX**: GR/IR Clearing (Maps to the Goods Receipt/Invoice Receipt liability G/L)
*   **The Process Flow**:
    1.  `ME21N` (Purchase Order): No FI entry.
    2.  `MIGO` (Goods Receipt): Debit Inventory (`BSX`), Credit GR/IR (`WRX`).
    3.  `MIRO` (Invoice Verification): Debit GR/IR (`WRX`), Credit Vendor.

### Part 2: Explain SD Integration (Order-to-Cash)
Sales and Distribution handles selling goods to customers. When an invoice is sent to a customer, the system must recognize revenue and record the customer's debt.

*   **The T-Code**: `VKOA` (Assign G/L Accounts for Sales and Distribution).
*   **How it works**: SAP uses a combination of factors including the Sales Organization, Chart of Accounts, Account Assignment Group of the Customer, and the Account Assignment Group of the Material to find the correct Revenue G/L account.
*   **Key Transaction Keys (Account Keys)**:
    *   **ERL**: Revenue (Maps to Sales Revenue G/L)
    *   **ERF**: Freight Revenue (Maps to Freight G/L)
*   **The Process Flow**:
    1.  `VA01` (Sales Order): No FI entry.
    2.  `VL01N` (Outbound Delivery / Goods Issue): Debit Cost of Goods Sold (COGS), Credit Inventory.
    3.  `VF01` (Billing / Invoice): Debit Customer, Credit Revenue (`ERL`).
