# WindDMS — Haulier and Vehicle Setup

WindDMS uses the transporter vendor synchronized from Navision as the haulier reference. The vehicle is then created against that haulier.

## 1. Verify synchronized haulier

1. Launch WindDMS and select the correct database/company profile.
2. Open the **Haulier** section.
3. Search using the transporter vendor number created in Navision.
4. Verify that the synchronized vendor/haulier record is displayed.
5. Verify the haulier number and associated company details.
6. Select the correct record when creating the vehicle.

**Expected result:** The transporter vendor created in Navision is available in WindDMS Haulier after synchronization.

## 2. Create vehicle

Use illustrative values only after confirming that the IDs are available in the target environment.

| Field | Illustrative value |
|---|---|
| Vehicle ID | QA-VEH-001 |
| Vehicle name/description | QA Test Bulk Vehicle |
| Haulier | Select the synchronized QA-TRANS-001 record |
| Company | Select the correct company profile |

1. Open the **Vehicle** section.
2. Select **New**.
3. Enter the vehicle ID and vehicle name/description.
4. Complete the required company details.
5. Select the haulier that corresponds to the transporter vendor created in Navision.
6. Open the **Compartment** tab.
7. Add the required compartment(s) and enter the capacity/quantity for each compartment.
8. Save the vehicle.
9. Search for the vehicle and verify its details, selected haulier and compartment capacities.

**Expected result:** The vehicle is saved with the correct company, synchronized haulier and configured compartment capacity. It is available for the applicable order planning scenario.
