# Order Management Lifecycle

This folder contains the end-to-end order journeys in one place. It is separated by the business purpose of the order, not by individual application.

## 1. Sales orders — normal customer

Normal-customer orders are sales orders. The two order types covered are:

- **Current Delivery Bulk**
- **Current Delivery Package**

The order is created in Salesforce and follows the applicable downstream application flow.

### Navision record movement
- Before completion, the record is available in **Sales Orders**.
- Once processed and invoiced, it moves to **Posted Sales Invoices**.
- The posted sales invoice PDF is available for invoice verification.

### Customer-specific invoice quantity
For Current Delivery Bulk, the customer's **Invoice Based On** setup determines which quantity appears on the invoice PDF.

| Customer setup | Invoice PDF quantity to verify |
|---|---|
| Order Quantity | Ordered quantity |
| Loaded Quantity — Standard customer | Standard loaded quantity |
| Loaded Quantity — Ambient customer | Ambient loaded quantity |
| Delivered Quantity | Delivered quantity |

Example values for validation:
- Ordered: 1,000
- Standard loaded: 999
- Ambient loaded: 998
- Delivered: 997

Expected invoice quantity is selected according to the customer's configured Invoice Based On value. This check belongs to normal sales Current Delivery Bulk; do not apply it to transfer orders.

## 2. Transfer orders — transfer customer

Transfer orders are created for a **transfer customer** and are kept separate from normal sales orders.

### Navision record movement
- The record is available in **Transfer Orders** while it is being processed.
- Once processing is completed, the record moves to **Posted Transfer Receipts**.
- Verify transfer completion and the relevant inventory movement. Do not expect a normal sales invoice PDF for this transfer-order flow.

## 3. End-to-end application flow

The detailed execution steps will be documented here as the actual workflow is confirmed across Salesforce, Navision, WindDMS and TMSLite.

## Documentation rules
- Keep Current Delivery Bulk and Current Delivery Package under Sales Orders.
- Keep transfer-customer processing under Transfer Orders.
- Do not include consignment as a separate order category.
- Do not add unconfirmed order types, steps or status transitions.
- Record actual results only after execution; otherwise mark the case Not Run.
