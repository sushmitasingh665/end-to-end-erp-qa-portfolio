# Navision — Master Data

## Data maintained here
- Product/item master data, including bulk and package product types
- Supply locations and relevant company/location attributes
- Transporter vendor records
- Purchase contracts and related setup
- SKU records and inventory setup

## QA checks
- Verify required product and location attributes before synchronization.
- Validate the location synchronization result in each configured destination.
- Confirm product synchronization follows the product-type rule: bulk to logistics where configured; package excluded from logistics where specified.
- Verify SKU creation against the intended item and location.

Do not publish real company codes, item numbers, vendor numbers, or location identifiers.