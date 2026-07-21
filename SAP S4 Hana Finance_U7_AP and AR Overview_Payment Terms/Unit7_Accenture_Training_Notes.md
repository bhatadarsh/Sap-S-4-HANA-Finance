# Accenture Stream Training: SAP S/4HANA Finance
## Unit 7: AP and AR Overview - Payment Terms

Welcome to your study guide and reference documentation for **Unit 7: AP and AR Overview - Payment Terms**. This document provides a walkthrough of the hands-on exercises for Unit 7, focusing on configuring and testing new payment terms for Customers and Vendors.

---

## 1. Assignment: Maintain New Terms of Payment

**Objective**: Create a custom payment term (0.5% discount in 10 days, 0.2% in 30 days, Net 45 days) and verify its functionality by assigning it to a Business Partner and posting an invoice.

### Step 1: Create New Payment Terms Code
*   **T-Code**: `OBB8` (Maintain Terms of Payment)
*   **Action**: 
    1. Click **New Entries**.
    2. Enter a 4-character identifier for your new Payment Term (e.g., `PT45`).
    3. **Description**: Enter an explanation (e.g., "0.5% 10 Days, 0.2% 30 Days, Net 45").
    4. **Account Type**: Check the boxes for both **Customer** and **Vendor** so this term can be used for both AR and AP.
    5. **Baseline Date Calculation**: Set the Default for Baseline Date to **Document Date**. This means the 45-day clock starts ticking on the date printed on the physical invoice.

### Step 2: Define Payment Terms / Installment Percentages
*   **Action**: In the same `OBB8` screen, scroll down to the **Payment terms** section and set the parameters:
    *   **Term 1**: Percentage = `0.5%`, No. of days = `10`
    *   **Term 2**: Percentage = `0.2%`, No. of days = `30`
    *   **Term 3**: No. of days = `45` (Leave percentage blank to indicate Net due).
*   Save your configuration.

### Step 3: Assign Payment Terms to Master Data
*   **T-Code**: `BP` (Maintain Business Partner)
*   **Action**: 
    1. Open an existing Customer or Vendor master record.
    2. Switch to the FI Vendor (`FLVN00`) or FI Customer (`FLCU00`) role.
    3. Navigate to the **Company Code** data segment and find the **Payment Transactions** tab.
    4. Enter your new Payment Term code (`PT45`) in the Terms of Payment field and save.

### Step 4: Post Invoice and Verify Due Date
*   **T-Code**: `FB60` (Vendor Invoice) or `FB70` (Customer Invoice)
*   **Action**: 
    1. Enter an invoice for the Business Partner you just updated.
    2. Observe the **Payment** tab on the invoice screen. The terms of payment should automatically default to `PT45`.
    3. Post the invoice.
    4. Use `FBL1N` (Vendor Line Items) or `FBL5N` (Customer Line Items) to view the open item. Verify that the Baseline Date and the calculated Due Date reflect your 45-day rule.

---

## 2. Topics Covered Today (Concepts)

*   **Baseline Date vs. Document Date**: The Document Date is the date the invoice was issued by the vendor. The Baseline Date is the date the system starts counting from to determine the due date and discount periods. By setting Baseline Date = Document Date, you ensure the vendor's actual invoice date dictates the payment schedule, not the date you happened to enter it into SAP (Posting Date).
*   **Cash Discounts**: Cash discounts are incentives for early payment. If a $10,000 invoice is paid within 10 days, the company only pays $9,950, and SAP automatically posts the $50 difference to a "Cash Discount Received" GL account during the payment clearing process (`F-53` / `F-28`).
