# Logistics and Integration

## Bulk-order logistics checkpoints
1. Confirm the order is released in Navision.
2. In WindDMS, locate the order and select the correct company, haulier and vehicle.
3. Allocate the order to the vehicle/compartment and lock the vehicle to generate the Trip ID.
4. Verify the order's planned status and Trip ID in Salesforce.
5. In TMSLite, locate the trip and load the quantity into the appropriate compartments.
6. Verify the loading confirmation and related Bill of Lading/loading document output.
7. Schedule delivery in WindDMS with valid date, quantity and product time windows.
8. Verify delivery confirmation and final trip-processing records.

## Staging investigation
- If the order is not visible downstream, inspect the relevant Navision order-header staging record first.
- If no record exists, investigate whether the message left Salesforce and whether middleware processing is required.
- For loading issues, inspect the Loading Header Staging List and the relevant trip/shipment record.
- Validate loading confirmation (LC), delivery confirmation (DC), and trip closure as distinct processing checkpoints.
- Verify invoice status/document separately; do not infer invoice posting solely from trip closure.

Use synthetic trip/order identifiers in all examples.