# Sales Order Lifecycle

This section separates the normal sales order variants and the consignment transfer flow.

## Normal sales orders
- Prepayment customers may remain in a payment-waiting state until payment is recorded and the order is released.
- Credit customers may require order-specific credit approval when credit conditions are not met.
- After submission, follow the order through acceptance and Navision release before validating logistics planning.
- Bulk products follow the configured WindDMS/TMSLite logistics path.
- Package products follow the Navision process without the bulk logistics vehicle-loading path, according to the described business rule.
- Validate relevant order documents, invoice posting, and any credit memo created after invoice cancellation.

## Contract distinction
- Purchase contract: maintained in Navision and can allocate quantity for a product/location and period.
- Blanket contract: maintained in Salesforce for a customer/product/location context and may use a specific price configured in Navision's pricing engine.

## Consignment
Consignment orders represent movement from a source location to a destination location. Validate shipment and posted transfer receipt. Do not expect the standard sales invoice PDF for this transfer flow.