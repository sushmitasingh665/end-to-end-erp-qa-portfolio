# Procurement

Document independent Navision procurement activities separately from Salesforce-originated sales orders.

## Scope
- Purchase contract creation and approval
- Purchase order creation and the known credit/non-credit categories
- Requisition creation and configured approval stages
- Purchase invoice posting (automatic or manual, depending on setup)
- Payment advice creation and payment approval
- Validation of generated payment advice documents and email notification

A credit order generated from a sales Trip ID is a distinct linked process; do not conflate it with an independently created procurement purchase order. Where a category or transition has not yet been confirmed, leave it marked for clarification rather than guessing.