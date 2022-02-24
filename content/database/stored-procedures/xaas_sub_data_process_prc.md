+++
title = "xaas_sub_data_process_prc"
+++

### What does it do?
Inserts rows into the `all_asset_view` table using values from other various tables.
{{% expand "More Details" %}}
1. If the **wfType** is `DCC_SUB`:
   1. Count rows in the `customer_partition_info` table that match the **customerId** input where **partitionStatus** is `A` (Active).
   2. If the count is 1:
      1. Call the following stored procedures in sequence:
         - xaas_neId_update_pr
         - athena_xaas_assetCategory_update_prc
      2. Insert rows into the `all_asset_view` table using values from the `networkelement_sub_stg` and `subscription_stg` tables.
      3. Get a count of rows in the `asset_group_master` table matching **customerId**/**wfId** that does not have a corresponding row in the `asset_group_device` table.
      4. If the count is > 0, insert rows into `asset_group_device` using values from `asset_group_master` and `networkelement_sub_stg`.
      5. Delete all rows from `contract_group_device_summary` that match **customerId** and **neId** from rows in the `networkelement_sub_stg` table.
      6. Insert rows into `contract_group_device_summary` using values from `networkelement_sub_stg`, `asset_group_device`, and `subscription_stg` tables.
2. If the **wfType** is _not_ `DCC_SUB`:
   1. Count rows in the `networkelement_sub_stg` table that match the **customerId** input.
   2. If the count is > 0:
      1. Insert rows into the `all_asset_view` table using values from the `networkelement_sub_stg` and `subscription_stg` tables.
      2. Call the `xaas_all_asset_track_prc` stored procedure.
{{% /expand %}}

### Referenced Tables
- all_asset_view
- amp_data_merge_logs
- asset_group_device
- asset_group_master
- contract_group_device_summary
- customer_partition_info
- networkelement_sub_stg
- subscription_stg

### Referenced Stored Procedures
- athena_xaas_assetCategory_update_prc
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- xaas_all_asset_track_prc
- xaas_neId_update_prc
