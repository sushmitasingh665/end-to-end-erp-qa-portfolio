# End-to-End ERP QA Portfolio

A focused portfolio based on real manual QA workflows and experience across connected enterprise applications.

## Repository structure

| Folder | Purpose |
|---|---|
| [Environment Setup](01-environment-setup/README.md) | Environment readiness and prerequisites before testing |
| [Salesforce](02-salesforce/README.md) | Salesforce customer and order-related setup/data |
| [Navision](03-navision/README.md) | Microsoft Dynamics NAV / Navision master data and setup |
| [WindDMS](04-winddms/README.md) | Vehicle, planning and delivery-related setup |
| [TMSLite](05-tmslite/README.md) | Location and loading-related setup |
| [Order Management Lifecycle](06-order-management-lifecycle/README.md) | Complete sales-order and transfer-order journeys |
| [Defects](07-defects/README.md) | Real defects, reproduction, investigation and outcomes |
| [Test Cases](08-test-cases/README.md) | Test cases and execution details linked to real scenarios/defects |

## Order categories covered

- **Sales orders:** Created for normal customers. The supported order types documented here are Current Delivery Bulk and Current Delivery Package. In Navision, completed sales orders move from Sales Orders to Posted Sales Invoices, where the invoice PDF can be viewed.
- **Transfer orders:** Created for transfer customers. Completed records move from Transfer Orders to Posted Transfer Receipts. These are documented separately from sales invoices.

## Documentation principles

- Document only workflows and results supplied or confirmed from actual experience.
- Keep each application's setup in its own folder.
- Keep the complete order journey in one Order Management Lifecycle folder.
- Add defect details and their related test cases when the actual defect/scenario information is provided.
- Do not invent IDs, steps, results or execution evidence. Mark unexecuted cases as Not Run.
- Use anonymized or approved information only. Do not publish credentials, customer-sensitive information, environment URLs, payloads or confidential records.

Additional business workflows will be added only when their real setup and execution details are provided.
