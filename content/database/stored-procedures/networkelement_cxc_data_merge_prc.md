+++
title = "networkelement_cxc_data_merge_prc"
+++

### What does it do?
Inserts rows into the `networkelement` table using values from the `networkelement_telemetry` and `networkelement_ib_data` tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
2. Get the **wfId** from rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `CSDFIB`
3. Count the rows in `asset_inventory_notification` that match **customerId**/**wfId** where **mgmtSystemType** is `DNAC` .
2. If the count is > 0, call the following stored procedures in sequence:
   - [dnac_advisory_update_prc]({{< ILink href="/database/stored-procedures/dnac_advisory_update_prc" >}})
   - [dnac_networkelement_update_prc]({{< ILink href="/database/stored-procedures/dnac_networkelement_update_prc" >}})
4. Open a read loop on the cursor that inserts rows into the `networkelement` table using values from the `networkelement_telemetry` table.
5. If  the **wfId** from step 2 is not null:
   1. Create a temporary table with distinct columns from the `networkelement_ib_data` table.
   2. Update columns of the `networkelement` table using values from the newly created temp table.
   3. Drop the temp table.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne
- asset_inventory_notification
- base_table_partition_info
- data_merge_logs
- networkelement
- networkelement_ib_data
- networkelement_telemetry 

### Referenced Stored Procedures
- [dnac_advisory_update_prc]({{< ILink href="/database/stored-procedures/dnac_advisory_update_prc" >}})
- [dnac_networkelement_update_prc]({{< ILink href="/database/stored-procedures/dnac_networkelement_update_prc" >}})
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
