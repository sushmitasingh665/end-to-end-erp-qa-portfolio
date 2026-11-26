# Integration Troubleshooting

## Investigation sequence
1. Use Navision as the first checkpoint for a Salesforce-originated order.
2. If the order is not visible, inspect the Order Header Staging List.
3. If no staging record exists, investigate whether the message left Salesforce and whether middleware (such as IPAS/BizTalk, where applicable) requires review.
4. If the order is present, inspect the staging details and processing status.
5. For loading issues, inspect the Loading Header Staging List using the relevant trip/shipment filter.
6. Distinguish loading confirmation (LC), delivery confirmation (DC), and trip closure records.
7. Verify invoice posting separately in the relevant invoice/order records.

## Evidence to capture
- Sanitized transaction reference
- Last successful application/checkpoint
- Expected versus actual status
- Relevant staging/processing message
- Reproduction steps and environment category

Do not infer invoice completion from trip closure alone. Never publish internal payloads, IP addresses, URLs, IDs or customer data.