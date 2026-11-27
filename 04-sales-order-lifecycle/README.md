# Sales Order Lifecycle

This section uses two core order workflows as the portfolio baseline: **Current Delivery Bulk** and **Current Delivery Package**. Customer and location variations are documented as test scenarios against these workflows, avoiding unnecessary duplication.

## 1. Current Delivery Bulk

### Normal sales customer
1. Sign in to Salesforce (SFDC), open the customer and select **Create Order**.
2. Select **Current Delivery Bulk**, continue to the order details, choose the applicable price, add the product and enter quantity.
3. Select **Get Price** and validate the returned price against the Navision Pricing Engine (PE) setup. Where applicable, compare effective-date pricing.
4. Quote generation is optional: validate both quote-generated and direct-submit paths.
5. Save and submit. Record the order number and verify the order in Navision's **Order Header Staging List**. Confirm successful processing, then refresh SFDC and verify the order progresses to **Planning**.
6. In the correct WindDMS database/company, open the relevant date and shift. Confirm the intended vehicle is available and has no conflicting planned order.
7. Find the order and move it to the selected truck (drag-and-drop or the available move-to-truck action). Lock the vehicle/truck; verify the lock indicator changes and a Trip ID is generated.
8. Refresh SFDC and verify the Trip ID is visible.
9. In TMSLite, open the active, accessible destination location and find the trip/order for the relevant date. Enter loading details and the required start/end dates or times. Select the actual vehicle and enter both Standard and Ambient quantities as applicable. Confirm loading.
10. Validate the Loading Confirmation (LC) in Navision's Loading Header Staging List using the Trip ID.
11. Complete the delivery step through the configured WindDMS delivery process. Validate Delivery Confirmation (DC) and subsequent trip closure/processing. Verify the actual invoice separately rather than treating trip closure alone as proof of invoicing.
12. For a normal sales customer, locate the transaction in Navision's **Posted Sales Invoices** using the order number or Trip ID. Open the PDF and validate the invoice details.

### Invoice quantity rule
Where the customer profile has an **Invoice Based On** setting, validate that the invoice reflects the configured quantity basis (Standard or Ambient), not simply both entered quantities. The customer setup drives which quantity is used on the invoice.

### Customer payment/credit variation
Prepayment and credit customers use the same core Current Delivery Bulk lifecycle after the order is eligible for release. Validate the relevant payment or credit-control gate before planning. The ordinary order documents and downstream workflow remain the same; prepayment-specific information may appear where applicable.

## 2. Current Delivery Package

### Normal sales customer
1. Create a Salesforce order using **Current Delivery Package**.
2. Add the product and quantity using the configured order details, then submit.
3. Verify the order is received and successfully processed in Navision's **Order Header Staging List**.
4. Refresh SFDC and verify the package order reaches **Accepted**.
5. In Navision, find the order in **Sales Orders** and post it using the environment's configured two-stage posting sequence.
6. After the first posting, refresh SFDC and verify the intermediate **Loaded** status.
7. Post the order again to complete the next posting stage. Verify Navision shows **Delivered** and the order is no longer in the active Sales Orders list.
8. Refresh SFDC and verify the final **Invoiced** status. Find the posted document in **Posted Sales Invoices** and validate the PDF.

Package orders in this documented flow do not require the WindDMS vehicle-planning or TMSLite truck-loading steps used for bulk delivery.

## 3. Transfer customer orders

A transfer customer represents an internal/location-to-location movement rather than a normal customer sale. Orders for this customer type are completed as transfers and are not invoiced.

- **Current Delivery Bulk:** the logistics flow is followed through planning, loading and delivery. Validate the location-level inventory movement and final transfer records; do not expect a sales invoice PDF.
- **Current Delivery Package:** find the order in Navision **Transfer Orders**, not Sales Orders. Post shipment and delivery (together or as separate posting actions, as supported by the environment). Verify the order leaves the active Transfer Orders list and appears in **Posted Transfer Receipts**.
- Validate that quantity is reduced at the source location and increased at the destination location in the relevant SKU/inventory records.
- Transfer customer orders do not use the normal sales-price/invoice path described for sales customers.

## 4. Consignment location on a normal customer

Consignment is determined by the location selected on the order, not merely by the customer being a transfer customer.

- A normal customer may have both a supplier/supply location and a separately configured consignment location.
- Using the supplier/supply location follows the normal sales-order path and can result in an invoice.
- Using the configured consignment location for a **Current Delivery Bulk** order follows the logistics flow but is processed as a location transfer: complete planning, loading and delivery, validate LC/DC and trip processing, and confirm the transfer record is reflected in **Posted Transfer Receipts**.
- Do not expect a normal sales invoice PDF for this consignment-location transfer scenario.
- The described consignment-location scenario is documented for Current Delivery Bulk only. Do not assume other order types support it without confirming the business configuration.

## 5. Scope boundaries and terminology

- The Xtract / with-ship-to / without-ship-to / scheduling variants were discussed but their exact names and behavioural differences were not finalized. They are intentionally excluded from the confirmed baseline until verified.
- Other order labels, including regression variants, should be added only after their exact names and rules are confirmed.
- Use the exact status labels and posting behaviour configured in the target environment; status wording can vary by implementation.
