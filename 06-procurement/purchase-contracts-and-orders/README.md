# Purchase Contracts and Orders

Document independent Navision procurement activities separately from sales-order-linked credit orders generated from a logistics Trip ID.

## Known scope
- Create and maintain purchase contracts with product, location, allocated quantity, validity period and approval.
- Create purchase orders using the confirmed credit and non-credit categories.
- Known non-credit types include non-trade and service; leave any unconfirmed third category unspecified until verified.

## QA coverage
- Required fields and valid dates.
- Product/location eligibility.
- Quantity allocation and approval.
- Correct order category and downstream status.
- Manual versus automatic posting behaviour where configured.