# Test Cases

Test cases are organized by functional, negative, integration and regression coverage.

## Current documented workflow baseline
- [Current Delivery Bulk and Current Delivery Package — scenarios and test cases](current-delivery-workflows.md)

The linked document covers normal sales customers (including prepayment and credit paths), transfer customers, and a normal customer using a consignment location.

## Integration and document-template checks
The workflow test suite includes Message ID tracing through the connected **iPaaS / Middleware** layer and coordination with **SmartComm** when a payload is needed for template modification or correction. Actual Message IDs and payloads must remain in approved internal systems; public examples use synthetic data only.

## Required fields
| Field | Description |
|---|---|
| Test Case ID | Unique identifier |
| Application / Module | System and area |
| Scenario | Behaviour under test |
| Preconditions | Required configuration/data |
| Test Data | Synthetic values |
| Steps | Numbered, reproducible actions |
| Expected Result | Expected business outcome |
| Actual Result | Complete only after execution |
| Status | Not Run / Pass / Fail / Blocked |
| Evidence / Defect ID | Sanitized evidence reference |

## Status integrity
Newly authored scenarios remain **Not Run** until genuinely executed. Clearly label conceptual examples as **Illustrative** or **Simulated**. Never imply that a test was executed in a former employer's environment when it was not.
