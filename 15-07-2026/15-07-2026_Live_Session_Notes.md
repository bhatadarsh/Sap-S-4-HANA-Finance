# Accenture Stream Training: SAP S/4HANA Finance
## Live Session Notes: 15-07-2026 (GL Master Data & Document Splitting)

Welcome to your study guide based on the live session screenshots captured on **15-07-2026**. This session covered a blend of topics tying together Tax Configuration, GL Master Data, and the critical setup for Document Splitting in SAP S/4HANA. 

---

## 1. Live Configuration Walkthrough

### Part A: Tax Calculation Procedures
*   **Context**: Building on the basic settings, the system needs to know which tax rules apply to which country.
*   **Action**: In the screenshots, we see the navigation to `Tax on Sales/Purchases` > `Basic Settings` > `Assign Country/Region to Calculation Procedure`. The country `IN` (India) was mapped to the calculation procedure `TAXINN` (a standard condition-based tax procedure for India).

### Part B: Defining the Retained Earnings Account
*   **Context**: Before you can create P&L (Profit & Loss) accounts, you must define a Retained Earnings account.
*   **Action**: 
    1. Navigate to `G/L Accounts` > `Preparations` > `Define Retained Earnings Account`.
    2. Enter the Chart of Accounts (`MAK9`).
    3. Define a P&L statement account type (usually `X`) and assign it to a specific GL account number (e.g., `100100`). This ensures that at the end of the fiscal year, all P&L account balances roll up into this balance sheet account.

### Part C: General Ledger Account Creation (`FS00`)
*   **Context**: Creating the actual GL accounts that will be used for daily postings.
*   **Action**: 
    1. Go to T-code `FS00` (Edit G/L Account Centrally).
    2. Enter the new account number (e.g., `100000`) and the Company Code (`MAK9`).
    3. Under the `Type/Description` tab, select the G/L Account Type (e.g., **Balance Sheet Account**) and assign it to the correct Account Group (e.g., **LIABILITIES**).
    4. Provide the Short Text and Long Text (e.g., `Share Capital A/C`).

### Part D: Document Splitting Configuration
*   **Context**: A major feature of New GL in S/4HANA is Document Splitting, which ensures balance sheets can be drawn up by Profit Center or Segment.
*   **Action 1 - Classify G/L Accounts**: Navigate to `Document Splitting` > `Classify G/L Accounts for Document Splitting`. Here, GL account ranges are mapped to specific Item Categories. For example:
    *   `100000` to `199999` $\rightarrow$ `01000` (Balance Sheet Account)
    *   `200000` to `299999` $\rightarrow$ `07000` (Fixed Assets)
    *   `300000` to `399999` $\rightarrow$ `300000` (Revenue)
    *   `400000` to `499999` $\rightarrow$ `20000` (Expense)
*   **Action 2 - Zero-Balance Clearing Account**: Navigate to `Define Zero-Balance Clearing Account`. When a document doesn't balance at the Profit Center level, SAP uses this clearing account (e.g., Account Key `000` assigned to GL `100110`) to automatically generate balancing line items.

---

## 2. Topics Covered Today (Concepts)

Based on the live session screenshots, here are the detailed explanations of the core concepts taught:

*   **Tax Calculation Procedure (`TAXINN`)**: A calculation procedure contains the structural foundation for calculating and posting taxes in SAP. It dictates the condition types (like base amount, central tax, state tax) and their calculation sequence. Assigning it to a country ensures that any company code created in that country adheres to those tax calculation rules.
*   **Retained Earnings Account**: A mandatory configuration in SAP Finance. At the end of a fiscal year, the balances of all Revenue and Expense accounts are reset to zero, and the net profit or loss is transferred to the Retained Earnings account on the Balance Sheet. SAP uses the P&L statement account type (like 'X') to link P&L accounts to this specific Retained Earnings account.
*   **G/L Account Type**: In S/4HANA, when creating a GL account, you must classify it. **Balance Sheet Accounts** track assets/liabilities. **Primary Costs or Revenue** accounts are used for P&L items that flow between FI and CO (Controlling). **Secondary Costs** are used purely for internal cost allocations within CO.
*   **Document Splitting - Item Categories**: Document splitting works by looking at the "Item Category" of a GL account. By classifying an account range (like expenses) to category `20000`, the system knows that when an expense is posted, the vendor line item (which has a different category) should inherit the profit center from this expense line.
*   **Zero-Balance Clearing Account**: If Document Splitting is set to demand a "Zero Balance" for Profit Centers, and a user posts a document crossing two profit centers (e.g., Debit PC1, Credit PC2), the document balances at the company code level but NOT at the profit center level. SAP automatically injects this "Zero-Balance Clearing Account" to credit PC1 and debit PC2 internally, ensuring every profit center's mini-balance sheet balances to exactly zero.
