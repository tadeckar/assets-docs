+++
title = "equipment_meraki_data_merge_prc"
+++

### What does it do?
Inserts rows into the `equipment` table using values from the `equipment_dcn` table.
{{% expand "More Details" %}}
1. Count the rows in the `asset_inventory_notification` table matching **customerId**/**wfId** where **mgmtSystemType** is `MERAKI`.
2. If the count is > 0, call the `meraki_equipment_update_prc` stored procedure.
3. Count the rows in the `base_table_partition_info` table matching **customerId** where
   - **mgmtSystemType** is `MERAKI` and
   - **partitionTag** is `BASE`
4. If the count is > 0:
   1. Get the **wfId** from the counted rows.
   2. Insert rows into the `equipment` table using values from the `equipment_dcn` table.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- base_table_partition_info
- data_merge_logs
- equipment
- equipment_meraki

### Referenced Stored Procedures
- meraki_equipment_update_prc
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
