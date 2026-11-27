# Order Management Lifecycle

This document contains the end-to-end order workflows in one place.

## Prerequisites

Complete the application setup before execution:

- Salesforce: active normal customer or transfer customer with the required customer settings.
- Navision: location, product, SKU, available inventory and pricing are configured.
- WindDMS: synchronized transporter vendor is available as a haulier; vehicle and compartments are configured.
- TMSLite: required company location is added to the user's profile.
- Use a product that is configured for the selected location and has available stock.

## A. Sales order — Current Delivery Bulk

**Customer:** Normal sales customer (prepayment or credit, as configured).

### Salesforce — create and submit order

1. Launch Salesforce and log in.
2. Search for and open the active normal sales customer.
3. Select **Create Order**.
4. Select **Current Delivery Bulk** as the order type.
5. Complete the required order information.
6. Select the applicable date.
7. Select the required location.
8. The order line contains the columns **Item Number**, **Quantity** and **Unit Price**. Select **Add Product** to display the entry fields.
9. Select the required bulk item in **Item Number**.
10. Enter the order quantity.
11. Select **Get Price** and verify that the unit price is fetched.
12. Select **Generate Quote**.
13. Submit the order.
14. Refresh the order and verify **Submitted** status. Record the order number.

### Navision — order staging

15. Launch Navision and open **Order Header Staging List** using Global Search.
16. Search by the Salesforce order number.
17. Verify that the order is received with **Processed** status.
18. Refresh Salesforce and verify that the order status progresses to **Planning**.

### WindDMS — plan order

19. Launch WindDMS and select the correct database/company profile.
20. Open the applicable date and shift.
21. Search for the intended vehicle and verify that it is available.
22. Search for the order number.
23. Right-click the order and select **Move on Truck**.
24. Enter the vehicle number and confirm.
25. Lock the truck and verify the generated **Trip ID**.
26. Refresh Salesforce and verify that the order status is **Planned**.

### TMSLite — loading

27. Launch TMSLite and open the active company location available in the user profile.
28. Search for the Trip ID and open the trip.
29. Enter loading start and end date/time details.
30. Select the vehicle.
31. Enter the applicable Standard and Ambient loaded quantities.
32. Confirm the loading details and finish loading.
33. Refresh Salesforce and verify that the order status is **Loaded**.

### Navision — loading confirmation

34. Open **Loading Header Staging List** in Navision.
35. Search/filter using the Trip ID or Shipment ID.
36. Verify that **LC (Loading Confirmation)** is received successfully.

### WindDMS — delivery and Navision confirmations

37. Return to WindDMS and open the applicable date and shift.
38. Search for the Trip ID and complete the delivery/dispatch action. Enter the applicable Standard and Ambient delivered quantities.
39. In Navision, open **Loading Header Staging List** and verify that **DC** and **TC** are received for the Trip ID.
40. Refresh Salesforce after the DC is successfully processed and verify that the order status progresses from **Delivered** to **Invoiced**.

### Navision — posted sales invoice

41. Open **Posted Sales Invoices** in Navision.
42. Search using the order number or Trip ID.
43. Open the invoice PDF and verify the invoice details and quantity.
44. Verify that the invoice PDF quantity matches the customer's **Invoice Quantity Based On** and **Billing Basis** setup.

### Invoice quantity — customer setup validation

For normal sales Current Delivery Bulk, the customer's **Invoice Quantity Based On** setup determines the invoice PDF quantity.

| Invoice Based On | Invoice PDF quantity |
|---|---|
| Order Quantity | Ordered quantity |
| Loaded Quantity — Standard | Standard loaded quantity |
| Loaded Quantity — Ambient | Ambient loaded quantity |
| Delivered Quantity | Delivered quantity |

Illustrative quantity values:
- Ordered quantity: 1,000
- Standard loaded quantity: 999
- Ambient loaded quantity: 998
- Delivered quantity: 997

Expected invoice PDF quantity:
- Order Quantity → 1,000
- Loaded Quantity for Standard → 999
- Loaded Quantity for Ambient → 998
- Delivered Quantity → 997

Run the applicable customer setup variation and verify the invoice PDF against that customer's configured value. This quantity validation is for normal sales Current Delivery Bulk only.

**Expected outcome:** The Salesforce order progresses through **Submitted → Planning → Planned → Loaded → Delivered → Invoiced**. LC, DC and TC confirmations are received in Navision as described, and the posted invoice PDF reflects the customer's Billing Basis and Invoice Quantity Based On configuration.

## B. Sales order — Current Delivery Package

**Customer:** Normal sales customer (prepayment or credit, as configured).

1. Launch Salesforce and log in.
2. Open the active normal sales customer and select **Create Order**.
3. Select **Current Delivery Package** and complete the required order information.
4. Select **Next** and choose the current/latest applicable date.
5. Select **Add Product** and choose the package product configured for the selected location (for example, Lubricants — Package).
6. Enter quantity and select **Get Price**.
7. Verify the price, then select **Create** and **Submit**.
8. Verify successful submission and record the generated order number.
9. In Navision, open **Order Header Staging List**, search the order number and verify that the record is processed.
10. Refresh Salesforce and verify the order status is **Accepted**.
11. In Navision, open **Sales Orders**, search the order number and perform the first **Post** action.
12. Refresh Salesforce and verify the intermediate **Loaded** status.
13. In Navision, search for the order again and perform the second **Post** action.
14. Verify that Navision shows **Delivered** and the order is no longer in the active Sales Orders list.
15. Refresh Salesforce and verify **Invoiced** status.
16. In Navision, open **Posted Sales Invoices**, search the order number and open the invoice PDF.
17. Verify the invoice details.

**Expected outcome:** The package order follows the Navision posting flow, reaches Delivered/Invoiced, and its posted invoice PDF is available. The bulk WindDMS/TMSLite loading flow is not part of this package workflow.

## C. Transfer order — Current Delivery Bulk

**Customer:** Transfer customer. This is a transfer order, not a normal sales order.

1. Launch Salesforce and log in.
2. Search for and open the active transfer customer.
3. Select **Create Order**.
4. Select **Current Delivery Bulk** and complete the required order information using the configured supplier/location context.
5. Select **Next** and choose the current/latest applicable date.
6. Select **Add Product** and choose the bulk product configured for the selected location with available inventory.
7. Enter quantity and select **Get Price** where required by the order screen.
8. Complete the required order details, select **Create** and **Submit**.
9. Verify successful submission and record the generated order number.
10. In Navision, open **Transfer Orders** and search for the order record. Verify that the transfer order is available for processing.
11. Continue the confirmed bulk logistics flow: in WindDMS, select the applicable date/shift, assign the available vehicle, use the synchronized haulier and lock the truck. Record the Trip ID.
12. In TMSLite, open the applicable profile location, search the Trip ID, enter loading details and complete loading.
13. In Navision **Loading Header Staging List**, verify the LC is received and processed for the Trip ID.
14. Complete delivery/dispatch in WindDMS.
15. In Navision, verify the DC and relevant trip processing are received successfully.
16. Return to **Transfer Orders** and verify the order has completed processing.
17. Open **Posted Transfer Receipts** and search for the completed transfer record.
18. Verify the posted transfer receipt and relevant source/destination inventory movement.

**Expected outcome:** The transfer customer order is processed as a transfer order, not as a sales invoice. The completed record is available in **Posted Transfer Receipts**. Do not expect a normal sales invoice PDF for this transfer flow.

## Execution status

These documented workflows are based on the process described for the portfolio. Mark each test **Not Run** until it has been executed in an authorized environment and supported with sanitized evidence. Do not publish real customer information, credentials, environment URLs, payloads or confidential internal records.
