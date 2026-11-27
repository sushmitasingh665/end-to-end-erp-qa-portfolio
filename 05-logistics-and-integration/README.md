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

## Integration and message tracing
- Use Navision as the first checkpoint for a Salesforce-originated order.
- If the order is not visible in the Order Header Staging List, investigate the message path through the connected iPaaS / Middleware layer.
- Capture the relevant **Message ID** when tracing an integration transaction. Use it to correlate the message with its processing status and payload in the authorized internal tools.
- If a template requires modification or correction, coordinate with the **SmartComm** team and share the relevant payload together with the Message ID through the approved internal channel. The payload helps the team investigate the template output/mapping.
- Do not publish actual Message IDs, payloads, customer data, document contents or internal integration details in this public portfolio. Use synthetic examples only.

## Staging investigation
- If the order is present in Navision, inspect the staging details and processing status.
- For loading issues, inspect the Loading Header Staging List and the relevant trip/shipment record.
- Validate loading confirmation (LC), delivery confirmation (DC), and trip closure as distinct processing checkpoints.
- Verify invoice status/document separately; do not infer invoice posting solely from trip closure.

Use synthetic trip/order identifiers in all examples.
