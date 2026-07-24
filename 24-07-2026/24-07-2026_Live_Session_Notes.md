# Accenture Stream Training: SAP S/4HANA Finance
## Live Session Notes: 24-07-2026 (FI-MM Integration / Procure-to-Pay)

Welcome to your study guide based on the live session screenshots captured on **24-07-2026**. This highly critical session covered **FI-MM Integration**, which is the technical bridge connecting Materials Management (Purchasing) to Financial Accounting via automatic account determination (`OBYC`).

---

## 1. Live Configuration & Workflow Walkthrough

### Part A: The Procure-to-Pay (P2P) Flow
The session mapped the physical business process of buying goods to the specific SAP transactions that execute them:
1.  **PO (Purchase Order)**: `ME21N` (No accounting entry generated).
2.  **GR (Goods Receipt)**: `MIGO` (Material arrives in warehouse. Accounting entry is generated).
3.  **Invoice Verification**: `MIRO` (Vendor sends the bill. Accounting entry is generated).
4.  **Goods Issue for Consumption**: `MB1A` / `MIGO` (Material is consumed by a department).

### Part B: FI-MM Flow of GL Account Finding
When a logistics user does a Goods Receipt in `MIGO`, they do not manually type in GL accounts. SAP finds the correct GL accounts automatically based on the following chain:
1.  **Material Master**: The material being purchased (e.g., Raw Material) belongs to a specific Material Type (e.g., `ROH`).
2.  **Valuation Class**: Inside the Material Master, a Valuation Class (e.g., `3000`) is assigned.
3.  **Transaction/Movement Type**: SAP knows what is happening (e.g., Goods Receipt vs Goods Issue).
4.  **Transaction Key**: SAP uses internal keys (like `BSX` or `WRX`) to identify the *type* of GL account needed.
5.  **`OBYC` (Automatic Account Determination)**: This is the massive configuration table where the FI consultant links the **Transaction Key + Valuation Class** to a specific **G/L Account Number**.

### Part C: Key Transaction Keys (OBYC)
The screenshots explicitly defined the most important transaction keys used to map MM movements to FI GL accounts:
*   **`BSX` (Inventory Posting)**: "How the material gets into the organization." This key maps to the **Inventory G/L Account** (Asset).
*   **`WRX` (GR/IR Clearing)**: "Goods Receipt / Invoice Receipt Clearing." This maps to the temporary liability account used to hold the value between receiving the goods and receiving the invoice.
*   **`GBB` (Offsetting entry for Inventory)**: "How the material is going outside from the organization." This is used for consumption or scrap, mapping to an **Expense G/L Account** (e.g., Raw Material Consumption).
    *   *Sub-modifiers for GBB*: `ZOF`, `ZOC`, `ZOR`.

### Part D: The Accounting Entries
The screenshots provided the exact debits and credits for the P2P cycle:

**1. Purchase Invoice Posting (Actually Goods Receipt - `MIGO` & `MIRO`):**
*   *Goods Receipt (`MIGO`)*:
    *   **Debit**: Inventory A/C (`BSX`)
    *   **Credit**: GR/IR Clearing A/C (`WRX`)
*   *Invoice Receipt (`MIRO`)*:
    *   **Debit**: GR/IR Clearing A/C (`WRX`)
    *   **Credit**: Vendor A/C 

**2. Issue Goods for Consumption (`MB1A` / `MIGO`):**
*   **Debit**: Raw Material Consumption A/C (`GBB`)
*   **Credit**: Inventory Raw Material A/C (`BSX`)

### Part E: Material Types
The session listed common SAP material types that dictate how a material is handled and valued:
*   **`ROH`**: Raw Material
*   **`HALB`**: Semi-Finished Goods
*   **`VERP`**: Packing Material
*   **`ERSA`**: Spare Parts
*   **`FOOD`**: Food
*   **`HAWA`**: Traded Goods
