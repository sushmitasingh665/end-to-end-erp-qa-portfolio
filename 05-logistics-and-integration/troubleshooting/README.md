# Integration Troubleshooting

## Investigation sequence
1. Use Navision as the first checkpoint for a Salesforce-originated order.
2. If the order is not visible, inspect the Order Header Staging List.
3. If no staging record exists, trace the transaction through the connected **iPaaS / Middleware** layer.
4. Capture the relevant **Message ID** and use it to locate/correlate the integration message and its processing details in authorized internal tools.
5. Inspect the available payload and processing status to identify where the transaction stopped or failed.
6. If the issue concerns a document template modification or correction, coordinate with the **SmartComm** team. Share the relevant payload and Message ID through the approved internal channel so the team can investigate the template output/mapping.
7. If the order is present in Navision, inspect the staging details and processing status.
8. For loading issues, inspect the Loading Header Staging List using the relevant trip/shipment filter.
9. Distinguish loading confirmation (LC), delivery confirmation (DC), and trip closure records.
10. Verify invoice posting separately in the relevant invoice/order records.

## Evidence to capture
- Sanitized transaction/order reference
- Message ID (keep real values in approved internal systems; use a synthetic placeholder in public examples)
- Last successful application/checkpoint
- Expected versus actual status
- Relevant staging/processing message
- Sanitized payload excerpt only where permitted
- Reproduction steps and environment category
- SmartComm coordination/reference when a template correction is involved

Never publish real payloads, Message IDs, IP addresses, URLs, credentials, customer data or proprietary document templates in this public portfolio. Do not infer invoice completion from trip closure alone.
