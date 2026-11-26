# Salesforce — Customer Master Data

## Customer types
The test setup includes two customer categories:
- **Prepayment customer:** order processing depends on the required payment being recorded.
- **Credit customer:** order processing depends on available credit conditions or the configured order-approval path.

## QA checks
- Create customer data only in the authorized Salesforce test environment.
- Verify customer type and required fields.
- Confirm that the created customer is available for the intended sales-order scenario.
- Keep the customer dataset separate from Navision product/location master data.

Use fictitious names and references in this portfolio. Detailed step-by-step setup will be added after the workflow walkthrough.