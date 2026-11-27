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
4. Select **Current Delivery Bulk** in the applicable order type field.
5. Complete the required order information and select the applicable location/context.
6. Select **Next**.
7. Select the current/latest applicable date.
8. Select **Add Product**.
9. Select the bulk product configured for the chosen location and with available inventory (for example, Diesel — Bulk).
10. Enter the order quantity.
11. Select **Get Price** and verify that the price is fetched.
12. Complete the quantity/order details required on the screen and continue using the available action.
13. Select **Create**, then **Submit**.
14. Verify successful submission, the **Submitted** status and generated order number. Record the order number.

### Navision — order staging and release

15. Launch Navision.
16. Open **Order Header Staging List** using Global Search.
17. Search by the Salesforce order number.
18. Verify that the order has been received and shows **Processed**.
19. Refresh the Salesforce order and verify that it progresses to **Planning**.

### WindDMS — plan order and assign vehicle

20. Launch WindDMS and select the correct database/company profile.
21. Open the applicable date and shift.
22. Search for the intended vehicle and verify that it is available and has no conflicting order planned for that shift.
23. Search for the order number.
24. Right-click the order and select **Move on Truck**.
25. Enter the vehicle number and confirm.
26. Lock the truck.
27. Verify the locked state and generated **Trip ID**.
28. Refresh Salesforce and verify that the Trip ID is displayed and the status changes from **Planning** to **Planned**.

### TMSLite — enter loading details

29. Launch TMSLite and open the active company location available in the user profile.
30. Search for the Trip ID and open the trip.
31. Enter loading start and end date/time details.
32. Select the actual vehicle.
33. Enter the applicable Standard and Ambient loaded quantities.
34. Confirm the loading details and finish loading.

### Navision — verify Loading Confirmation

35. Launch Navision and open **Loading Header Staging List**.
36. Filter/search by Shipment ID using the Trip ID.
37. Verify that the **LC (Loading Confirmation)** is received successfully with **Processed** status.

### WindDMS and Navision — delivery and completion

38. Return to WindDMS and open the applicable date and shift.
39. Search for the Trip ID and complete the delivery/dispatch action.
40. In Navision, verify that the **DC (Delivery Confirmation)** is received successfully for the Trip ID.
41. Refresh/check the relevant trip processing record and verify that the configured trip processing has completed.
42. Search Sales Orders in Navision using the order number or Trip ID.
43. Verify that the completed order is no longer in the active Sales Orders list.
44. Open **Posted Sales Invoices** and search by order number or Trip ID.
45. Open the invoice PDF and verify the invoice details and quantity.
46. Refresh Salesforce and verify **Invoiced** status and invoice document availability on the order.

### Invoice quantity — customer setup validation

For normal sales Current Delivery Bulk, the customer's **Invoice Based On** setup determines the invoice PDF quantity.

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

**Expected outcome:** The order is submitted, staged, planned, loaded and delivered; LC and DC are processed; the sales order is invoiced; and the invoice PDF reflects the customer's Invoice Based On configuration.

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
