# Contract and Pricing Scenarios

## Purchase contract — Navision
A purchase contract is created in Navision with location, product, allocated quantity, validity period and approval. When an eligible sales order uses the active contract-enabled location and product, consumption is drawn from the contract allocation rather than ordinary SKU stock, according to the described setup.

The related Trip ID can trigger a Navision purchase-side credit order, which may lead to requisition and purchase-invoice processing. Keep this linked process separate from independently created procurement orders.

## Blanket contract — Salesforce
A blanket contract is created for a customer and includes location, period and product. It does not create the purchase-order document described in the purchase-contract flow. The associated price is configured in the Navision pricing engine.

## QA coverage
Validate contract eligibility, product/location matching, validity dates, allocated quantity, price selection and the correct distinction between the two contract types.