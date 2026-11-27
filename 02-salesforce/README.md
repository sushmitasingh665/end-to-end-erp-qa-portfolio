# Salesforce — Environment and Customer Data Setup

This page covers the Salesforce checks and data preparation required before sales-order testing.

## 1. Verify Salesforce environment access

The team may use different Salesforce environments for different releases or testing activities (for example, Hotfix or LC Release).

1. Confirm the required environment name/type from the development team's testing details.
2. Open the corresponding Salesforce sandbox URL.
3. Verify that the supplied login credentials are mapped to that environment.
4. Log in and confirm that the user has access to the specific sandbox required for testing.
5. Confirm that the environment is the correct one before creating or updating test data.

**Expected result:** The correct Salesforce sandbox opens successfully and the tester can access the required environment.

## 2. Create normal sales customers

Create separate normal sales customers for the billing-basis and invoice-quantity combinations needed for order testing.

### Customer creation

1. Open the customer creation area in Salesforce.
2. Select the company for which the customer is being created.
3. Enter the customer ID and customer name.
4. Complete the required company and customer details.
5. Enter the relevant customer/business address details.
6. Set **Billing Basis**:
   - **Standard** for a Standard customer.
   - **Ambient** for an Ambient customer.
7. Set **Invoice Quantity Based On**:
   - **Order Quantity**
   - **Loaded Quantity**
   - **Delivered Quantity**
8. Complete the remaining mandatory fields and save/create the customer.
9. Verify that the customer is created and active.

The **Invoice Quantity Based On** field can also be updated after customer activation. Reopen the active customer, update the field to the required dropdown value and save the change.

### Customer data to keep ready for order testing

Prepare at least these five normal sales customer configurations:

| Sample customer | Billing Basis | Invoice Quantity Based On |
|---|---|---|
| QA-CUST-AMB-LOAD | Ambient | Loaded Quantity |
| QA-CUST-AMB-DEL | Ambient | Delivered Quantity |
| QA-CUST-STD-LOAD | Standard | Loaded Quantity |
| QA-CUST-STD-DEL | Standard | Delivered Quantity |
| QA-CUST-ORDER-QTY | Standard or Ambient | Order Quantity |

The names above are illustrative only. Use unique, available IDs and names in the authorized test environment.

### Impact on invoice PDF

The customer's **Billing Basis** and **Invoice Quantity Based On** settings determine which loading/delivery quantity is reflected on the generated invoice PDF.

- **Loaded Quantity:** During TMSLite loading, Standard and Ambient loaded quantities are entered separately. For a Standard customer, the invoice quantity should reflect the Standard loaded quantity. For an Ambient customer, it should reflect the Ambient loaded quantity.
- **Delivered Quantity:** During delivery/dispatch in WindDMS, Standard and Ambient delivered quantities are entered separately. The invoice quantity should reflect the delivered quantity corresponding to the customer's Billing Basis.
- **Order Quantity:** The invoice quantity should reflect the quantity originally ordered.

Use different values for ordered, loaded and delivered quantities when executing these checks so that the invoice PDF demonstrates which configured quantity was used.

## 3. Create a transfer customer

Create a separate customer with the required transfer-customer setup for transfer-order testing.

1. Open the customer creation area.
2. Select the appropriate company and transfer-customer setup/type.
3. Enter the customer ID, name, company details and required address details.
4. Complete the mandatory fields and save.
5. Verify that the transfer customer is active and available for order creation.

## 4. Create a blanket order / blanket purchase contract

A blanket contract is created against the customer and remains in **Accepted** state after successful submission/release.

1. Open the **Create Blanket Purchase Contract** area.
2. Select the customer and complete the required contract details.
3. Select the order type: **Current Delivery Bulk** or **Current Delivery Package**.
4. Select the applicable location.
5. Enter the contract start date and end date.
6. Add the product(s) and the applicable quantity/allocation details.
7. Submit the blanket contract.
8. Verify that it is successfully released and remains in **Accepted** state.

### Use a blanket contract while creating a sales order

1. Select **Create Order** for the customer.
2. Select the order type and date.
3. Select the blanket-order checkbox.
4. Verify that the available blanket-contract dropdown is populated based on the selected date and active contract period.
5. Select the required blanket contract.
6. Verify that the product list is restricted to products included in that selected blanket contract.
7. If the blanket contract selection is changed, verify that the previously displayed product selection is cleared and the product list refreshes for the newly selected contract.
8. Select a product from the refreshed list and continue with order creation.

**Expected result:** Only a blanket contract active for the selected date can be selected, and only products associated with the selected contract are available for the order.

## 5. Illustrative data and disclosure

Names such as `QA-CUST-AMB-LOAD` are examples for documentation only. They are not claims that these records were created in a company environment. Use approved/sanitized data in the public portfolio; do not publish real customer personal details, credentials, sandbox URLs or confidential company information.
