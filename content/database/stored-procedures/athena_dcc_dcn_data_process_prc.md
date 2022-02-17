+++
title = "athena_dcc_dcn_data_process_prc"
+++

### What does it do?
Removes all rows from the `athena_subscription_stg` table that have a stale **wfId**. Calls stored procedures to process the athena subscriptions. Then, syncs the athena subscriptions to the `all_asset_view` and `all_asset_track_view` tables.
{{% expand "More Details" %}}
1. Deletes stale records from the `athena_subscription_stg` table where
   - **customerId** matches the stored procedure input param
   - **wfId** does not match the stored procedure input param
2. Count the rows in the `customer_partition_info` table that match the **customerId** where **partitionStatus** is `A`.
3. If the count is 1:
   1. Get the wfId from the `customer_partition_info` table
   2. Call the following stored procedures with **customerId**/**wfId** as parameters:
      - [athena_dcc_stg_data_process_prc]({{< ILink href="/database/stored-procedures/athena_dcc_stg_data_process_prc" >}})
      - [athena_dcn_stg_data_process_prc]({{< ILink href="/database/stored-procedures/athena_dcn_stg_data_process_prc" >}}) 
      - athena_ib_stg_data_process_prc
4. Get a count of any rows in `athena_subscription_stg` where **assetCategory** is `Cisco Plus` that are not present in the `all_asset_view` table.
5. If the count is > 0:
   1. Update rows in `all_asset_view` so that fields match rows in `athena_subscription_stg`.
   2. Update rows in `all_asset_track_view` so that fields match rows in `athena_subscription_stg`.
6. Get a count of any rows in `all_asset_view` where **assetCategory** is `Cisco Plus` that are not present in the `athena_subscription_stg` table.
7. If the count is > 0 update **assetCategory** to `Cisco` for the rows in `all_asset_view` and `all_asset_track_view` that matched previous count.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- athena_subscription_stg 
- customer_partition_info  
- all_asset_view 
- all_asset_track_view

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [athena_dcc_stg_data_process_prc]({{< ILink href="/database/stored-procedures/athena_dcc_stg_data_process_prc" >}}) 
- [athena_dcn_stg_data_process_prc]({{< ILink href="/database/stored-procedures/athena_dcn_stg_data_process_prc" >}}) 
- athena_ib_stg_data_process_prc
