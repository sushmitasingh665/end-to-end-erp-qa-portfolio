# Current Delivery Order Workflows

**Execution status:** All documented cases are **Not Run** until they are executed in an authorized test environment. Use synthetic data only. Record actual results and evidence only after execution.

## Scope

1. Normal sales customer
   - Current Delivery Bulk
   - Current Delivery Package
2. Normal customer using a consignment location
   - Current Delivery Bulk
3. Transfer customer
   - Current Delivery Bulk only

## Customer setup prerequisite — Invoice Based On

For a normal sales customer, verify the customer's **Invoice Based On** configuration before creating the Current Delivery Bulk order. This customer-level setup determines the quantity printed on the sales invoice. It is not a universal quantity rule for every order type.

| Customer's Invoice Based On setup | Expected invoice PDF quantity |
|---|---|
| Order Quantity | Ordered quantity |
| Loaded Quantity — Standard customer | Standard loaded quantity |
| Loaded Quantity — Ambient customer | Ambient loaded quantity |
| Delivered Quantity | Delivered quantity |

**Example test data**

- Ordered quantity: 1,000
- Standard loaded quantity: 999
- Ambient loaded quantity: 998
- Delivered quantity: 997

Expected invoice PDF quantity for each configuration:

- Order Quantity → 1,000
- Loaded Quantity for a Standard customer → 999
- Loaded Quantity for an Ambient customer → 998
- Delivered Quantity → 997

Run the applicable invoice-basis variation by configuring the customer setup, processing the normal sales Current Delivery Bulk order, and checking the quantity on the posted invoice PDF. This validation is not included for consignment or transfer orders.

## A. Normal sales customer — Current Delivery Bulk

**Preconditions**
- Normal sales customer is configured for the applicable prepayment or credit process.
- Customer's Invoice Based On setup is known and recorded when invoice quantity is in scope.
- Selected product is configured for the selected location and has available inventory.
- Required location, pricing, WindDMS vehicle/shift and TMSLite location setup is available.
- Required integrations are available.

**Execution steps**
1. Launch Salesforce and log in.
2. Search for and open the normal prepayment or credit customer.
3. Select **Create Order**.
4. Select **Current Delivery Bulk** and the applicable location/product context using the available order fields.
5. Select **Next**.
6. Select the current/latest applicable date.
7. Select **Add Product** and choose an available product for the selected location.
8. Enter the order quantity and select **Get Price**.
9. Verify that the price is fetched, then select **Create** and **Submit**.
10. Verify successful submission, the **Submitted** status and generation of an order number. Record the order number.
11. Launch Navision and open **Order Header Staging List** from Global Search.
12. Search using the order number and verify that the order is received with **Processed** status.
13. Refresh the Salesforce order and verify that its status progresses to **Planning**.
14. Launch WindDMS and select the correct database/company profile for the test environment.
15. Open the applicable date and shift. Search for the intended vehicle and verify that it is available and has no conflicting planned order for that shift.
16. Search for the order number. Right-click the order, select **Move on Truck**, enter the vehicle number and confirm.
17. Lock the truck. Verify the lock state and generated **Trip ID**.
18. Refresh Salesforce and verify that the Trip ID is displayed and the order status changes from **Planning** to **Planned**.
19. Launch TMSLite and open the applicable active company location.
20. Search for the Trip ID and open the trip.
21. Enter the loading start and end date/time details.
22. Select the actual vehicle and enter Standard and Ambient loaded quantities, as applicable.
23. Confirm the loading details and finish loading.
24. In Navision, open **Loading Header Staging List**.
25. Filter/search by Shipment ID using the Trip ID and verify that the **LC (Loading Confirmation)** is received with **Processed** status.
26. Return to WindDMS, open the applicable date and shift, search for the Trip ID and complete the delivery/dispatch action.
27. In Navision, verify that the **DC (Delivery Confirmation)** is received successfully for the Trip ID.
28. Refresh/check the relevant trip processing record and verify that the trip has completed its configured processing.
29. In Navision, search Sales Orders using the order number or Trip ID and verify that the completed order is no longer in the active Sales Orders list.
30. Open **Posted Sales Invoices**, search using the order number or Trip ID, and open the invoice PDF.
31. Verify invoice details and validate the invoice quantity against the customer's **Invoice Based On** setup, where applicable.
32. Refresh Salesforce and verify **Invoiced** status and that the invoice document is available on the order page.

**Expected result**
- The order is accepted by the connected applications and progresses through planning, loading, delivery and invoicing.
- LC and DC are successfully processed.
- The completed order is no longer in the active Sales Orders list.
- The posted invoice is available, and its quantity follows the customer's Invoice Based On configuration.

### Prepayment and credit customer variations

The downstream Current Delivery Bulk workflow above is common once the applicable payment/credit requirement is satisfied.

- **Prepayment customer:** Complete the applicable prepayment requirement before the order proceeds, as required by the configured process.
- **Credit customer:** Complete the applicable credit approval requirement, where required, before the order proceeds.

Do not assume that prepayment and credit customers have identical release conditions. Record the actual customer setup and observed gate during execution.

## B. Normal sales customer — Current Delivery Package

**Preconditions**
- Normal sales customer and applicable prepayment/credit setup are available.
- Package product and required Navision setup are available.

**Execution steps**
1. Launch Salesforce and log in.
2. Open the normal sales customer and select **Create Order**.
3. Select **Current Delivery Package**, complete the applicable order fields and select **Next**.
4. Select the current/latest applicable date.
5. Add the package product, enter quantity, select **Get Price**, and verify the fetched price.
6. Select **Create** and **Submit**. Record the generated order number.
7. In Navision, open **Order Header Staging List**, search the order number and verify successful processing.
8. Refresh Salesforce and verify the order status is **Accepted**.
9. In Navision, open **Sales Orders**, search for the order number and perform the first **Post** action.
10. Refresh Salesforce and verify the intermediate **Loaded** status.
11. In Navision, find the order again and perform the second **Post** action.
12. Verify that Navision shows **Delivered** and the order is no longer in the active Sales Orders list.
13. Refresh Salesforce and verify **Invoiced** status.
14. In Navision, open **Posted Sales Invoices**, search for the order number and open the invoice PDF.
15. Verify the invoice details.

**Expected result**
- The package order follows the Navision posting flow described above.
- Salesforce reflects the observed Accepted, Loaded and Invoiced statuses at the corresponding stages.
- The posted invoice is available for verification.
- This package workflow does not include the WindDMS/TMSLite bulk logistics steps.

## C. Normal customer using a consignment location — Current Delivery Bulk

**Preconditions**
- The normal customer has the applicable supply location and a configured consignment location.
- Product/SKU and inventory are available for the consignment location.
- Required WindDMS and TMSLite setup is available.

**Execution steps**
1. Launch Salesforce and log in.
2. Open the normal customer and select **Create Order**.
3. Select **Current Delivery Bulk** and choose the customer's **consignment location** instead of the supply location.
4. Continue with the applicable date, product selection, quantity, **Get Price**, **Create** and **Submit** steps.
5. Record the generated order number.
6. In Navision **Order Header Staging List**, search the order number and verify successful processing.
7. Continue the bulk logistics lifecycle: plan the order in WindDMS, lock the truck and generate the Trip ID.
8. Verify the Trip ID and planned status in Salesforce.
9. In TMSLite, open the trip, enter loading details and complete loading.
10. In Navision **Loading Header Staging List**, verify the LC is received and processed for the Trip ID.
11. Complete delivery in WindDMS.
12. In Navision, verify DC and the relevant trip processing are received successfully.
13. Verify the order reaches **Delivered**.
14. Check the applicable transfer records and source/destination inventory movement.
15. Search **Posted Sales Invoices** using the order number or Trip ID and verify that no normal sales invoice PDF is generated for this consignment-location transfer scenario.

**Expected result**
- The consignment-location order follows the bulk logistics and location-transfer process.
- The order reaches Delivered and the transfer/inventory movement is reflected.
- It is not processed as a normal invoiced sales order.

## D. Transfer customer — Current Delivery Bulk only

**Preconditions**
- A transfer customer and its configured supplier location are available.
- Product/SKU and inventory are available for the relevant locations.
- Required WindDMS and TMSLite setup is available.

**Execution steps**
1. Launch Salesforce and log in.
2. Open the transfer customer and select **Create Order**.
3. Select **Current Delivery Bulk** and the configured supplier location.
4. Continue with the applicable date, product selection, quantity, **Get Price**, **Create** and **Submit** steps.
5. Record the generated order number.
6. In Navision **Order Header Staging List**, search the order number and verify successful processing.
7. Plan the order in WindDMS, assign an available vehicle, lock the truck and record the generated Trip ID.
8. Refresh Salesforce and verify the Trip ID and planned status.
9. In TMSLite, search the Trip ID, enter loading details and complete loading.
10. In Navision **Loading Header Staging List**, verify the LC is received and processed.
11. Complete delivery in WindDMS.
12. In Navision, verify the DC and relevant trip processing are received successfully.
13. Verify that the order reaches **Delivered**.
14. Verify transfer completion and the source/destination SKU inventory movement.
15. Search Posted Sales Invoices using the order number or Trip ID and verify that no normal sales invoice PDF is expected.

**Expected result**
- The transfer customer's Current Delivery Bulk order completes the logistics and transfer process.
- The order reaches Delivered and inventory movement is reflected at the relevant locations.
- No normal sales invoice PDF is generated.

## Execution record

For each test case, record:
- Test Case ID and execution date
- Customer type and relevant customer setup
- Order number and Trip ID, where applicable (use anonymized sample identifiers in this public portfolio)
- Actual result
- Status: **Not Run / Pass / Fail / Blocked**
- Sanitized evidence or defect reference

Never publish real customer details, order numbers, Trip IDs, Message IDs, payloads, screenshots, environment URLs, credentials or employer-owned documents.
