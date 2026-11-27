# Salesforce — Customer Master Setup

This page records the customer data needed before creating sales or transfer orders.

## Customer records to prepare

Create separate customer records for the customer setup variations being tested. The following names are illustrative only.

| Sample customer | Customer purpose | Billing method | Invoice Based On |
|---|---|---|---|
| QA-CUST-STD-ORDER | Normal sales customer | Standard | Order Quantity |
| QA-CUST-STD-LOADED | Normal sales customer | Standard | Loaded Quantity |
| QA-CUST-STD-DELIVERED | Normal sales customer | Standard | Delivered Quantity |
| QA-CUST-MVN | Normal sales customer | MVN | Order Quantity |
| QA-CUST-TRANSFER | Transfer customer | As configured for transfer customer | Not applicable to sales invoice validation |

For Loaded Quantity, use the applicable customer/product loading category:
- Standard customer/product → validate Standard loaded quantity.
- Ambient customer/product → validate Ambient loaded quantity.

Confirm the actual customer setup fields and allowed values in the target Salesforce environment. Do not assume that every field label matches this document.

## Customer creation — execution outline

1. Launch Salesforce and open the customer creation area.
2. Select the appropriate customer setup/type for a normal sales customer or transfer customer.
3. Enter the customer ID and customer name.
4. Select the correct company.
5. Enter the customer's verified business/address details in the relevant address fields, including billing address details as required.
6. Complete the required customer and company details.
7. Set the applicable billing method (Standard or MVN).
8. Set **Invoice Based On** for normal sales customers: Order Quantity, Loaded Quantity or Delivered Quantity, as applicable.
9. Select/associate the applicable product or customer category, such as Standard or Ambient, where required by the setup.
10. Complete the remaining mandatory fields and save/create the customer.
11. Verify the customer record is created and active.
12. Reopen the customer and verify the company, address, billing method, Invoice Based On and other configured values.

## Setup variations to retain

- Keep separate normal customers for the invoice quantity options so the invoice PDF can be compared against each customer's setup.
- Keep a separate Standard billing customer and MVN billing customer.
- Keep a separate transfer customer for transfer-order execution.
- Where a combination of billing method and Invoice Based On is required, configure and record that exact combination in the test environment before execution.

## Verification

The customer must be active and selectable when creating the intended order. Record the configured customer type, billing method and Invoice Based On value as test prerequisites.
