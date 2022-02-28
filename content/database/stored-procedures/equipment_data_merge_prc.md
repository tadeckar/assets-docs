+++
title = "equipment_data_merge_prc"
+++

### What does it do?
Inserts rows into the `equipment` table using values from `equipment_telemetry` and `equipment_ib_data`.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
2. Delete all rows for the given **customerId**/**wfId** from the `equipment` table.
3. Get a count of rows in `asset_inventory_notification` that match **customerId**/**wfId** where **mgmtSystemType** is `DNAC`. If count is > 0, run the [dnac_equipment_update_prc]({{< ILink href="/database/stored-procedures/dnac_equipment_update_prc" >}}) stored procedure.
4. Get a count of rows in `asset_inventory_notification` that match **customerId**/**wfId** where **mgmtSystemType** is `CSDFIB`. If count is > 0, run the [ib_equipment_update_prc]({{< ILink href="/database/stored-procedures/ib_equipment_update_prc" >}}) stored procedure.
5. Get the **wfId** from rows in `base_table_partition_info` that match **customerId** where **mgmtSystemType** is `CSDFIB` and **partitionStatus** is `A`. **wfId** is stored in a variable and used in step 9.
6. Get a count of rows in `base_table_partition_info` that match **customerId**/**wfId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
7. If the count is > 0, open a read loop on the cursor (from step 1) that inserts rows into the `equipment` table using values the `equipment_telemetry` table.
8. Call the following stored procedures in sequence:
   1. [equipment_apic_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_apic_data_merge_prc" >}})
   2. [equipment_meraki_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_meraki_data_merge_prc" >}})
   2. [equipment_dcc_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_dcc_data_merge_prc" >}})
9. If the **wfId** from step 5 is not null, insert rows into the `equipment` table using values from the `equipment_ib_data` table.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne
- asset_inventory_notification
- base_table_partition_info
- data_merge_logs
- equipment
- equipment_ib_data
- equipment_telemetry

### Referenced Stored Procedures
- [dnac_equipment_update_prc]({{< ILink href="/database/stored-procedures/dnac_equipment_update_prc" >}})
- [equipment_apic_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_apic_data_merge_prc" >}})
- [equipment_meraki_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_meraki_data_merge_prc" >}})
- [equipment_dcc_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_dcc_data_merge_prc" >}})
- [ib_equipment_update_prc]({{< ILink href="/database/stored-procedures/ib_equipment_update_prc" >}})
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
