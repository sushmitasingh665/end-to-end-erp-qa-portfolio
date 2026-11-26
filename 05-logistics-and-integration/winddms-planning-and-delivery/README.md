# WindDMS — Planning and Delivery

## Planning workflow
1. Confirm the sales order has been released in Navision.
2. Search for the order in WindDMS.
3. Identify the correct company and haulier.
4. Assign the appropriate vehicle and compartment.
5. Lock/confirm the vehicle to generate a Trip ID.
6. Refresh Salesforce and verify the expected planned status and Trip ID.

## Delivery scheduling
Enter the delivery date, product-wise quantity and delivery time windows. The described process requires at least a 20-minute gap between different product delivery windows; validate this against the configured business rule.

## QA scenarios
- Correct vehicle/haulier assignment.
- Compartment capacity and allocation.
- Trip ID generation and downstream visibility.
- Invalid or overlapping delivery windows.
- Successful delivery confirmation and corresponding processing record.

Use only synthetic order, vehicle and trip references.