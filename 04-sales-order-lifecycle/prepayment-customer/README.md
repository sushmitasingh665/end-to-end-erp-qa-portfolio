# Prepayment Customer Orders

## Known business behaviour
A prepayment customer's order can remain in a waiting-for-payment state until the required payment is recorded. After payment completion, validate that the order can proceed through its configured release process.

## Documents to validate
- Order Quote / order-created document where applicable
- Perform invoice for the prepayment flow
- Order confirmation after release where applicable
- Loading and delivery documents for bulk logistics orders
- Sales invoice after the configured invoicing step

## Test scenarios to author
1. Prepayment order with payment completed.
2. Prepayment order without payment; verify the waiting-payment hold.
3. Payment completion followed by order release.
4. Bulk product logistics path versus package product path.

Detailed steps and expected status transitions will be written after the complete normal prepayment bulk-order walkthrough.