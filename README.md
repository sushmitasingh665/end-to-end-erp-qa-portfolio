# End-to-End ERP QA Portfolio

A practical manual QA portfolio documenting application setup, master data preparation and end-to-end order processing across connected enterprise applications.

## Repository

| Folder | Coverage |
|---|---|
| [Environment Setup](01-environment-setup/README.md) | Environment and access readiness |
| [Salesforce](02-salesforce/README.md) | Customer creation and customer-level order/invoice configuration |
| [Navision](03-navision/README.md) | Locations, products, SKU/inventory, pricing and transporter vendor setup |
| [WindDMS](04-winddms/README.md) | Haulier verification and vehicle/compartment setup |
| [TMSLite](05-tmslite/README.md) | Add the required company location to the user profile |
| [Order Management Lifecycle](06-order-management-lifecycle/README.md) | Sales order and transfer order execution from creation to completion |
| [Defects](07-defects/README.md) | Real defects, reproduction steps, investigation and outcomes |
| [Test Cases](08-test-cases/README.md) | Test cases and execution records linked to real scenarios/defects |

## Order categories

- **Sales orders:** Created for normal customers. Order types: Current Delivery Bulk and Current Delivery Package. In Navision, completed sales orders are available in Posted Sales Invoices and the invoice PDF can be checked.
- **Transfer orders:** Created for transfer customers. In Navision, the record is processed through Transfer Orders and moves to Posted Transfer Receipts when completed.

## Sample data and disclosure

Any QA-prefixed names or IDs in this repository are illustrative test data, not records claimed to have been created in a company system. Actual company IDs, customer information, addresses, internal defect references, screenshots and payloads should be published only where disclosure is authorized. Use sanitized examples otherwise.

Only document workflows that are based on actual experience. Unexecuted examples remain Not Run; do not claim a test passed unless it has been run and evidenced.
