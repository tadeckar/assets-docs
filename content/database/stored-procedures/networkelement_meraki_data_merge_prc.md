+++
title = "networkelement_meraki_data_merge_prc"
+++

### What does it do?
Inserts rows into the `networkelement` table using values from the `networkelement_meraki` table.
{{% expand "More Details" %}}
1. Count rows in the `asset_inventory_notification` table that match **customerId**/**wfId** where **mgmtSystemType** is `MERAKI`.
2. If the count is > 0, call the following stored procedures in sequence:
   - [meraki_advisory_update_prc]({{< ILink href="/database/stored-procedures/meraki_advisory_update_prc" >}})
   - [meraki_networkelement_update_prc]({{< ILink href="/database/stored-procedures/meraki_networkelement_update_prc" >}})
3. Count rows in the `base_table_partition_info` table that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `MERAKI`
4. If the count is > 0, insert rows into the `networkelement` table using values from the `networkelement_meraki` table.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- base_table_partition_info
- data_merge_logs
- networkelement
- networkelement_meraki

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [meraki_advisory_update_prc]({{< ILink href="/database/stored-procedures/meraki_advisory_update_prc" >}})
- [meraki_networkelement_update_prc]({{< ILink href="/database/stored-procedures/meraki_networkelement_update_prc" >}})
