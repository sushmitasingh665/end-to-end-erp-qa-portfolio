# Current Delivery Order Workflows — Test Scenarios and Test Cases

**Execution status:** All cases below are newly documented and remain **Not Run**. Use authorized test environments and synthetic data only. Record actual results and evidence only after execution.

## Preconditions and test data
- Salesforce customer configured as a normal sales customer (prepayment or credit as required).
- A separate transfer customer for location-to-location movements.
- Bulk and package products configured in Navision.
- Active source/destination locations, SKU and available inventory.
- Applicable Navision Pricing Engine setup and customer **Invoice Based On** setting (Standard or Ambient).
- WindDMS company/database, haulier, vehicle, shift and compartments configured for bulk delivery.
- TMSLite location active and accessible to the tester.
- Required integrations through the connected iPaaS / Middleware layer available.
- Where a template correction is in scope, access to the approved SmartComm support process.

## A. Current Delivery Bulk — normal sales customer

| ID | Scenario | Key steps | Expected result |
|---|---|---|---|
| CDB-001 | Create and submit a Current Delivery Bulk order | In SFDC, open the normal customer; create Current Delivery Bulk; select price; add bulk product and quantity; Get Price; submit | Price matches Navision Pricing Engine setup; order is submitted and an order number is generated |
| CDB-002 | Optional quote generation | Create a Current Delivery Bulk order; use Get Quote before submitting | Quote is generated and associated with the order; order can proceed through submission |
| CDB-003 | Submit without quote generation | Create a Current Delivery Bulk order; Get Price and submit without using Get Quote | Order can be submitted without requiring a quote document |
| CDB-004 | Validate order integration to Navision | Submit order; search order number in Navision Order Header Staging List | Order is received and staging/process status indicates successful processing; SFDC progresses to Planning |
| CDB-005 | Validate price against effective date | Create otherwise equivalent orders using applicable effective dates; compare Get Price result with Navision PE setup | Returned price matches configured price for selected effective date |
| CDB-006 | Plan order against an available vehicle | In correct WindDMS company/database, open relevant date and shift; confirm vehicle has no conflicting planned order; move order to truck and lock it | Order is assigned to selected vehicle; lock indicator changes; Trip ID is generated |
| CDB-007 | Validate Trip ID synchronization | Refresh SFDC after WindDMS planning | SFDC displays generated Trip ID and planned state |
| CDB-008 | Load bulk order in TMSLite | Open active location; find trip; enter loading date/time details; select actual vehicle; enter Standard and Ambient quantities as applicable; confirm loading | Loading is accepted for the correct trip and vehicle |
| CDB-009 | Validate Loading Confirmation in Navision | Search Trip ID in Loading Header Staging List after TMSLite loading | LC record is present and successfully processed |
| CDB-010 | Validate delivery confirmation | Complete configured delivery process in WindDMS; inspect Navision staging by Trip ID | DC record is received and successfully processed; trip progresses through configured closure |
| CDB-011 | Validate final sales invoice | Complete normal sales order lifecycle; search order number or Trip ID in Posted Sales Invoices; open PDF | Posted invoice is available and linked to expected order/trip |
| CDB-012 | Validate invoice quantity basis — Standard | Set customer Invoice Based On to Standard; load different Standard and Ambient quantities; complete invoicing | Invoice PDF reflects Standard quantity according to customer setup |
| CDB-013 | Validate invoice quantity basis — Ambient | Set customer Invoice Based On to Ambient; load different Standard and Ambient quantities; complete invoicing | Invoice PDF reflects Ambient quantity according to customer setup |
| CDB-014 | Validate prepayment customer path | Create Current Delivery Bulk for prepayment customer; satisfy payment requirement; continue through planning, loading, delivery and invoice | Payment gate is handled; eligible order follows normal downstream lifecycle; prepayment-specific information appears where applicable |
| CDB-015 | Validate credit customer path | Create Current Delivery Bulk for credit customer; complete required credit approval if applicable; continue downstream | Credit gate is satisfied; eligible order follows same downstream lifecycle and invoice path |

## B. Current Delivery Package — normal sales customer

| ID | Scenario | Key steps | Expected result |
|---|---|---|---|
| CDP-001 | Create and submit a Current Delivery Package order | In SFDC, create Current Delivery Package for normal sales customer; add package product and quantity; submit | Order is created and submitted successfully |
| CDP-002 | Validate order integration and acceptance | Search order number in Navision Order Header Staging List; refresh SFDC | Staging record is successfully processed; SFDC order status is Accepted |
| CDP-003 | Validate first Navision posting stage | Search order in Navision Sales Orders and perform first configured post action | First posting stage completes; SFDC reflects intermediate Loaded status |
| CDP-004 | Validate final Navision posting stage | Find order again and perform second configured post action | Navision shows Delivered; order is removed from active Sales Orders; SFDC updates to Invoiced |
| CDP-005 | Validate posted package invoice | Search order number in Posted Sales Invoices and open invoice PDF | Posted invoice is available and order/product/quantity details are correct |
| CDP-006 | Validate package order does not enter bulk logistics path | Follow Current Delivery Package normal sales order and inspect WindDMS/TMSLite | Package flow completes through Navision posting without bulk vehicle planning or TMSLite truck loading |

## C. Transfer customer orders

| ID | Scenario | Key steps | Expected result |
|---|---|---|---|
| TRF-001 | Current Delivery Bulk for transfer customer | Create Current Delivery Bulk for transfer customer; add product and quantity; submit; complete WindDMS planning, TMSLite loading and delivery | Order reaches Delivered; LC/DC and trip processing are reflected; no normal sales invoice is expected |
| TRF-002 | Validate bulk transfer inventory movement | Inspect source and destination SKU/inventory after completion | Quantity decreases at source and increases at destination |
| TRF-003 | Current Delivery Package for transfer customer | Create Current Delivery Package for transfer customer; submit; find order in Navision Transfer Orders | Transfer package order is available in Transfer Orders, not Sales Orders |
| TRF-004 | Post transfer shipment and delivery | Post shipment and delivery together or in separate actions, as supported | Shipment and delivery posting complete successfully |
| TRF-005 | Verify posted transfer receipt | Search order in Posted Transfer Receipts | Completed transfer record is available; active Transfer Orders entry is removed |
| TRF-006 | Validate package transfer inventory movement | Check SKU/inventory at source and destination | Source quantity is reduced and destination quantity is increased; no sales invoice is expected |

## D. Normal customer using a consignment location — Current Delivery Bulk

| ID | Scenario | Key steps | Expected result |
|---|---|---|---|
| CON-001 | Compare supply and consignment locations | Use same normal customer with configured supply and consignment locations; create comparable Current Delivery Bulk orders | Supply location follows normal sales/invoice path; consignment location follows transfer-style processing |
| CON-002 | Complete consignment-location bulk order | Create Current Delivery Bulk for normal customer using consignment location; process through Navision, WindDMS, TMSLite and delivery | Order reaches Delivered; logistics confirmations and trip processing are received |
| CON-003 | Verify consignment transfer record | Inspect active Transfer Orders where applicable; after successful trip closure, inspect Posted Transfer Receipts | Active transfer record is cleared on completion and posted transfer receipt is available |
| CON-004 | Verify no sales invoice for consignment-location order | Search Posted Sales Invoices using order number/Trip ID | No normal sales invoice PDF is expected for this consignment-location transfer scenario |

## E. Integration and template-related test scenarios

| ID | Scenario | Key steps | Expected result |
|---|---|---|---|
| INT-001 | Trace an order using Message ID | Submit an order; capture its Message ID from the authorized integration monitoring/logging view; correlate it with the transaction and processing status | Message ID identifies the relevant integration message and helps trace its processing path |
| INT-002 | Investigate a message that does not reach Navision | Confirm order is absent from Order Header Staging List; use Message ID to trace the message through iPaaS / Middleware | Investigation identifies the last successful processing point or failure details; findings are documented without exposing sensitive payloads |
| INT-003 | Support a SmartComm template correction | For a template-related issue, capture the relevant Message ID and share the associated payload with SmartComm through the approved internal channel | SmartComm receives the trace reference and payload needed to investigate template modification/correction |
| INT-004 | Validate corrected template output | After the approved template correction is deployed to the test environment, execute the relevant transaction and inspect generated output | Output reflects the agreed template correction; evidence is recorded in the authorized test record |

## F. Shared regression checks

| ID | Scenario | Key steps | Expected result |
|---|---|---|---|
| REG-001 | Verify order-type routing | Execute one normal Current Delivery Bulk and one normal Current Delivery Package order | Bulk follows logistics planning/loading/delivery; package follows Navision posting path |
| REG-002 | Verify customer-type routing | Compare normal sales customer and transfer customer orders using supported order types | Normal sales customer produces sales invoice where configured; transfer customer completes as transfer without sales invoice |
| REG-003 | Verify document destination | Search Posted Sales Invoices for sales orders and Posted Transfer Receipts for transfer/consignment flows | Each completed transaction is found in the correct posted-document area |
| REG-004 | Verify inventory impact | Compare source/destination SKU balances before and after a completed transfer | Inventory movement matches the transferred quantity |

## Scope notes
- Exact Xtract / with-ship-to / without-ship-to / scheduling order names and behavioural differences are pending confirmation. Do not document them as confirmed until verified.
- Exact names of other regression order variants are pending confirmation.
- Confirm the exact labels for the two Navision posting actions and delivery confirmation steps in the target environment.
- All cases remain **Not Run** until genuinely executed. Populate Actual Result, Status and Evidence only after execution.
