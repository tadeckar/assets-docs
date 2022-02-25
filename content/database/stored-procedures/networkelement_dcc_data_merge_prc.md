+++
title = "networkelement_dcc_data_merge_prc"
+++

### What does it do?
Inserts rows into the `networkelement` table using values from the `networkelement_dcc` table.
{{% expand "More Details" %}}
1. Count rows in the `asset_inventory_notification` table that match **customerId**/**wfId** where **mgmtSystemType** is `DCC`.
2. If the count is > 0, call the following stored procedures in sequence:
   - dcc_advisory_update_prc 
   - dcc_networkelement_update_prc 
   - athena_dcc_stg_data_process_prc
3. Count rows in the `base_table_partition_info` table that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DCC`
4. If the count is > 0, insert rows into the `networkelement` table using values from the `networkelement_dcc` table.
5. If the count from step 1 is > 0:
   1. Delete rows from the `device_license_view` table that match column values from rows in the `networkelement_dcc` table.
   2. Insert rows into `device_license_view` using values from `networkelement_dcc` for all devices with full data present.
   3. Update the **licenseType** and **licenseName** for rows in the `device_license_view` table based on values of other columns in the row.
   4. Insert rows into `device_license_view` again for any row where **licenseType** is `Intersight`, but also has a non-empty **licenseStatus**.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- base_table_partition_info
- device_license_view
- data_merge_logs
- networkelement
- networkelement_dcc 

### Referenced Stored Procedures
- athena_dcc_stg_data_process_prc
- dcc_advisory_update_prc 
- dcc_networkelement_update_prc 
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
