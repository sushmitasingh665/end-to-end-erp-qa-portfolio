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
6. Reopen/search the location and verify that it is available for the required setup.

## 2. Create/prepare products

Create the products required for the order scenarios.

- **Diesel — Bulk:** configure as the bulk product.
- **Lubricants — Package:** configure as the package product.

1. Open the relevant item/product master page.
2. Select **New**.
3. Enter the item/product ID and description.
4. Complete the mandatory product details and configure the correct product/order category (Bulk or Package) using the actual available fields.
5. Save and verify each product.

## 3. Create SKU and prepare inventory

1. Open the relevant SKU/location setup page.
2. Create the SKU association for the required product and location.
3. Verify the product is associated with the intended location.
4. Prepare available stock for the product/location.
5. Post the inventory transaction using the applicable Navision inventory journal/process.
6. Verify the posted inventory and available quantity for the SKU/location.

The product should be configured for the selected location and have available inventory so that it is selectable during Salesforce order creation.

## 4. Set up pricing

1. Open the Navision Pricing Engine.
2. Select the applicable location.
3. Select the product.
4. Enter/configure the applicable price and effective date using the available pricing setup.
5. Save the pricing setup.
6. Verify that the location/product combination returns the expected price when the order is created in Salesforce using **Get Price**.

## 5. Create transporter vendor

1. Open the **Vendor** page in Navision.
2. Select **New**.
3. Enter the vendor number/ID.
4. Enter the vendor name.
5. Complete the required vendor/company details.
6. Set **Vendor Type** to **Transporter**.
7. Save the vendor.
8. Search for the vendor number and verify the record and Transporter type.
9. Run the applicable synchronization so the transporter vendor is available to WindDMS.

## 6. Verify order records

- Normal customer sales orders are viewed in **Sales Orders** and, after invoicing, in **Posted Sales Invoices**.
- Transfer customer records are viewed in **Transfer Orders** and, after completion, in **Posted Transfer Receipts**.
