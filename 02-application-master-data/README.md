# Application Master Data and Synchronization

This section describes the source application for each type of test data and the checks needed before an end-to-end order scenario.

## Data ownership by application
| Data | Source application | QA validation |
|---|---|---|
| Prepayment and credit customers | Salesforce | Customer type and required customer details |
| Products/items and locations | Navision | Product type, location attributes, company setup |
| Transporter/vendor | Navision | Vendor type and vendor reference |
| Vehicles and compartments | WindDMS | Company, haulier, vehicle and compartment association |
| TMSLite location/product/haulier data | Synchronized from configured source applications | Destination availability and activation where required |

## Key synchronization rules
- A newly configured location is synchronized to the connected applications required by the environment.
- Bulk products are synchronized to logistics/WindDMS where configured.
- Package products are not sent to logistics when the business rule excludes them.
- A SKU is created in Navision using the relevant item and location, then synchronized; verify its status after processing.

See the application-specific subfolders for focused checklists.