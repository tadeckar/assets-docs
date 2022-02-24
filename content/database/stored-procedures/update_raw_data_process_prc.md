+++
title = "update_raw_data_process_prc"
+++

### What does it do?
Gets counts for devices by **mgmtSystemType**. If counts are 0, removes relevant partitions. Otherwise, call stored procedures to create summary views and merge data.
{{% expand "More Details" %}}
1. Get a count of rows matching **customerId**/**wfId** from tables based on **mgmtSystemType** stored procedure input parameter:
| **mgmtSystemType**   | **Table**                 |
| ------------------   | ------------------------- |
| `CSDFIB`             | networkelement_ib_data    |
| `DNAC`               | networkelement_telemetry  |
| `APIC`               | networkelement_dcn        |
| `MERAKI`             | networkelement_meraki     |
| `DCC`                | networkelement_dcc        |
2. If the row count is 0:
   1. Update the **partitionStatus** to `D` for the **customerId**/**wfId** row in the `base_table_partition_info` table.
   2. Call the [drop_dnac_old_partions_prc]({{< ILink href="/database/stored-procedures/drop_dnac_old_partions_prc" >}}) stored procedure
   3. Update the **processingStatus** to `NODATA` for rows in the `asset_inventory_notification` table where **customerId**/**wfId** match.
   4. Exit the current procedure.
3. Otherwise, count the number of rows in the `base_table_partition_info` table where the row matches the stored procedure's input parameters.
4. If the count is > 0:
   1. Set the **partitionStatus** to `D` (Deleted) for the matching row in the `base_table_partition_info` table for any rows that were in `A` (Active) state.
   2. Set the **partitionStatus** to `A` (Active) for the matching row in the `base_table_partition_info` table for any rows that were in `I` (Inprogress) state.
   3. Call the [drop_dnac_old_partions_prc]({{< ILink href="/database/stored-procedures/drop_dnac_old_partions_prc" >}}) stored procedure
   4. Delete rows in the `base_table_partition_info` table that are marked with **partitionStatus** as `D`.
5. Call the following stored procedures:
   1. [add_sumview_table_partions_prc]({{< ILink href="/database/stored-procedures/add_sumview_table_partions_prc" >}})
   2. [data_merge_prc]({{< ILink href="/database/stored-procedures/data_merge_prc" >}})
   3. [sum_table_data_update_prc]({{< ILink href="/database/stored-procedures/sum_table_data_update_prc" >}})
   4. `update_sum_data_process_prc`
6. Update the **processingStatus** to `SUCCESS` for relevant rows from the `asset_inventory_notification` table.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification 
- base_table_partition_info
- data_merge_logs
- networkelement_dcc
- networkelement_dcn
- networkelement_ib_data
- networkelement_meraki
- networkelement_telemetry


### Referenced Stored Procedures
- [add_sumview_table_partions_prc]({{< ILink href="/database/stored-procedures/add_sumview_table_partions_prc" >}})
- [data_merge_prc]({{< ILink href="/database/stored-procedures/data_merge_prc" >}})
- [drop_dnac_old_partions_prc]({{< ILink href="/database/stored-procedures/drop_dnac_old_partions_prc" >}})
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [sum_table_data_update_prc]({{< ILink href="/database/stored-procedures/sum_table_data_update_prc" >}})
- update_sum_data_process_prc
