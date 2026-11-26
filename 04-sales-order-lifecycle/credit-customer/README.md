# Credit Customer Orders

## Known business behaviour
A credit order can remain in an awaiting-credit-approval state when the customer's credit conditions are not met.

An authorized approver may approve the specific order through the configured approval levels. This order-level approval releases that order; it does not permanently increase the customer's credit limit.

A separate test condition can use a correctly configured credit limit and cleared overdue invoices to validate direct order release.

## QA coverage
- Credit available: order release.
- Insufficient credit: order held for approval.
- First-level and multi-level approval paths as configured.
- Verify approval affects the intended order only.
- Validate order documents and invoice lifecycle.