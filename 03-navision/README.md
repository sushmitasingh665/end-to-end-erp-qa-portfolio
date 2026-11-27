# Microsoft Dynamics NAV / Navision — Master Data Setup

Prepare the Navision master data required for order creation, pricing, inventory and logistics integration.

## Illustrative test data

These IDs and names are examples for documentation only. Confirm availability and uniqueness before using them in any test environment.

| Data | Illustrative value | Purpose |
|---|---|---|
| Location | QA-LOC-001 | Test supply/location context |
| Bulk product | QA-DIESEL-BULK | Diesel — bulk product |
| Package product | QA-LUBES-PACK | Lubricants — package product |
| Transporter vendor | QA-TRANS-001 | Vendor with type Transporter |

## 1. Create/prepare a location

1. Open the relevant location master page in Navision.
2. Select **New**.
3. Enter an available location ID and location name.
4. Complete the mandatory location/company details.
5. Save the location.
6. Select **Synchronize**.
7. Refresh/search the page and allow the synchronization to complete.
8. Verify that the location is synchronized and its status becomes **Active**.

## 2. Create/prepare products

Create the products required for the order scenarios.

- **Diesel — Bulk:** configure as the bulk product.
- **Lubricants — Package:** configure as the package product.

1. Open the relevant item/product master page.
2. Select **New**.
3. Enter the item/product ID and description.
4. Complete the mandatory product details and configure the correct product/order category (Bulk or Package) using the actual available fields.
5. Save the product.
6. Select **Synchronize**.
7. Refresh/search the page and verify that the product is synchronized and active.

## 3. Create SKU and prepare inventory

1. Open the **Stockkeeping Unit** page in Navision.
2. Select **New**.
3. Select the required product and location.
4. Save the SKU record.
5. Select **Synchronize**.
6. Wait a few seconds, refresh/search the page and verify that the SKU becomes active.
7. Prepare available stock for the product/location.
8. Post the inventory transaction using the applicable Navision inventory journal/process.
9. Verify the posted inventory and available quantity for the SKU/location.

The product should be configured for the selected location and have available inventory so that it is selectable during Salesforce order creation.

## 4. Approval prerequisite

Complete the required workflow approval setup before submitting requests that require approval, such as a Pricing Engine setup/change request. Verify the approval route is configured and the request can be submitted through the approved process.

## 5. Set up pricing

1. Open the Navision Pricing Engine.
2. Select the applicable location.
3. Select the product.
4. Enter/configure the applicable price and effective date using the available pricing setup.
5. Save the pricing setup.
6. Verify that the location/product combination returns the expected price when the order is created in Salesforce using **Get Price**.

### Blanket-order pricing

Maintain the blanket-order price separately from the normal-order price where the business setup requires it. For the same location and product, verify that:
- A normal sales order fetches the normal Pricing Engine value.
- An order created using a blanket contract fetches the blanket-order-specific value.

Compare the Unit Price returned by **Get Price** in Salesforce for both cases.

## 6. Create vendor for WindDMS Haulier

In Navision, create the vendor with **Vendor Type = Transporter**. After synchronization, this vendor is displayed as a **Haulier** in WindDMS.


1. Open the **Vendor** page in Navision.
2. Select **New**.
3. Enter the vendor number/ID.
4. Enter the vendor name.
5. Complete the required vendor/company details.
6. Set **Vendor Type** to **Transporter**.
7. Save the vendor.
8. Search for the vendor number and verify the record and Transporter type.
9. Run the applicable synchronization so the transporter vendor is available to WindDMS.

## 7. Create a purchase contract

A purchase contract is created in Navision and can be selected at the individual product-line level during Salesforce sales-order creation.

1. Use Global Search to open **Purchase Contract**.
2. Select **New**.
3. Verify that the purchase contract number is generated automatically by the number series; do not enter a manual number.
4. Enter the purchase contract name.
5. Select the vendor. The vendor must already exist in Navision with **Vendor Type = Third-Party Supplier**.
6. Select the applicable location.
7. Enter the contract **From** and **To** dates.
8. Add the required item number/product.
9. Enter the inventory/allocation quantity for that item.
10. Save the purchase contract and verify its details.

### Use purchase contract inventory on a sales order

- During Salesforce order creation, the **Purchase Contract** field is available at the product-line level alongside the item details.
- Select the applicable purchase contract for each product line.
- Different product lines in one sales order can use different purchase contracts; one contract can also contain multiple products.
- Verify that the order quantity is consumed against the inventory allocated to the selected purchase contract, rather than the ordinary SKU inventory.

**Expected result:** The correct purchase contract is selectable for the product line, and its allocated inventory is used for the order.

## 8. Verify order records

- Normal customer sales orders are viewed in **Sales Orders** and, after invoicing, in **Posted Sales Invoices**.
- Transfer customer records are viewed in **Transfer Orders** and, after completion, in **Posted Transfer Receipts**.
