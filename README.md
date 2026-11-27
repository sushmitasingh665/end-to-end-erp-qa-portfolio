# End-to-End ERP Quality Assurance Portfolio

A practical portfolio documenting manual QA experience across connected ERP, CRM, logistics, inventory, pricing, order-management and procurement workflows.

The examples are anonymized. No employer-owned documents, client information, production identifiers, screenshots, credentials, environment URLs or proprietary test assets are included.

## QA coverage
- Requirements understanding and scenario design
- Environment readiness and application-wise master-data preparation
- Functional, integration, negative, regression, smoke, sanity and UAT testing
- End-to-end order lifecycle and cross-application validation
- Inventory, pricing, contracts, approvals and financial-document checks
- Defect reproduction, investigation, retesting and regression impact analysis
- Test documentation and requirement traceability

## Application landscape

| Application / Component | Business purpose represented |
|---|---|
| Salesforce (SFDC) | Customer records, blanket contracts and sales-order initiation |
| Microsoft Dynamics NAV / Navision | Product/location master data, SKU, inventory, pricing, purchase contracts, procurement and staging validation |
| WindDMS | Vehicle/haulier data, order planning, compartment allocation and delivery scheduling |
| TMSLite | Trip acknowledgement, loading workflow and Bill of Lading-related outputs |
| iPaaS / Middleware | Integration-message and payload tracing between connected applications |
| SmartComm | Template-related investigation and correction support using the relevant message ID and payload |

## Portfolio map
1. [Environment readiness](01-environment-readiness/README.md)
2. [Application master data and synchronization](02-application-master-data/README.md)
3. [Inventory and pricing](03-inventory-and-pricing/README.md)
4. [Sales order lifecycle](04-sales-order-lifecycle/README.md)
5. [Logistics and integration](05-logistics-and-integration/README.md)
6. [Procurement](06-procurement/README.md)
7. [Test cases](07-test-cases/README.md)
8. [Defect management](08-defect-management/README.md)
9. [Test data and execution](09-test-data-and-execution/README.md)
10. [Requirement traceability](10-requirement-traceability/README.md)

## Key business rules represented
- Prepayment and credit customers follow different payment/credit-control paths.
- Bulk products require logistics processing where configured; package products are excluded from logistics where the business rule specifies.
- Location and product synchronization must be validated in each required destination.
- Order-level credit approval releases the relevant order; it does not itself permanently increase the customer's credit limit.
- Purchase contracts in Navision and blanket contracts in Salesforce are distinct business concepts.
- Consignment orders follow a location-transfer process and are not treated as standard invoiced sales orders.
- Normal sales orders may involve planning, loading, delivery confirmation and invoice processing.
- Integration investigation uses the relevant Message ID and processing/payload details; template-related issues may require coordination with SmartComm.

## Test-case format
| Field | Purpose |
|---|---|
| Test Case ID | Unique reference |
| Module / Application | System and functional area |
| Scenario | Behaviour being validated |
| Preconditions | Required setup and data |
| Test Data | Synthetic values only |
| Steps | Reproducible actions |
| Expected Result | Expected business/system outcome |
| Actual Result | Filled only after execution |
| Status | Not Run / Pass / Fail / Blocked |
| Evidence / Defect ID | Sanitized evidence or sample defect reference |

**Execution integrity:** Test cases are marked *Not Run*, *Illustrative* or *Simulated* unless genuinely executed in an authorized environment. Simulated results are never represented as actual project execution.

## About
**Quality Assurance Engineer | Manual Testing | 7 Years of Experience**

Experience areas include manual and functional testing, ERP and enterprise applications, end-to-end and integration testing, inventory and order management, procurement, regression, smoke, sanity, UAT, defect lifecycle and Azure DevOps / TFS.

This is a living portfolio. Detailed workflows, test cases, sample defects and traceability artefacts will be added progressively.
