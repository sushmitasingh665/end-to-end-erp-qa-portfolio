# Master-Data Synchronization

## Location synchronization
A location created in Navision is synchronized to the connected applications configured for that location. Validate the relevant synchronization statuses and confirm destination availability.

## Product synchronization
- Bulk product: expected to synchronize to logistics/WindDMS where configured.
- Package product: expected not to synchronize to logistics where the business rule excludes it.

## SKU synchronization
Create the SKU in Navision using the item and location references, synchronize it, and verify the resulting status.

## Test design
Include positive and negative checks, source/destination validation, duplicate/retry behaviour where requirements define it, and clear expected results. Never publish actual payloads or identifiers.