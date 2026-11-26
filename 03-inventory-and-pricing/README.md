# Inventory and Pricing

## SKU and inventory readiness
1. Confirm that the required product and location master data exist.
2. Create the Stock Keeping Unit (SKU) using the correct item and location references.
3. Synchronize the SKU and verify the resulting active/synchronized status.
4. Create the relevant Item Ledger Entry with item, location and quantity.
5. If posting fails because a required product/setup code is missing, investigate the referenced setup, update only authorized configuration, and retry.
6. Verify the resulting inventory balance for the correct item and location.

## Pricing validation
Use the Navision Pricing Engine to verify that the returned price matches the selected business context:
- Standard supply location
- Location enabled for a purchase contract
- Customer/product/location eligible for a Salesforce blanket contract

The same product may have different configured prices for different location or contract contexts. Record the selected context and expected price source in each test case. Do not publish real customer, product, location, or price data.