+++
title = "sweox_alerts_data_merge_prc"
+++

### What does it do?
Insert rows into the `asset_inventory_alert_sweox` table using values from various other tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
2. Delete all rows for the given **customerId**/**wfId** from the `asset_inventory_alert_sweox` table.
3. Get a count of rows in `base_table_partition_info` that match **customerId**/**wfId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
4. If the count is > 0, open a read loop on the cursor that inserts rows into the `asset_inventory_alert_sweox` table using values from the `alert_sweox_telemetry` table.
5. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `APIC`
6. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 5.
   2. Insert rows into the `asset_inventory_alert_sweox` table using values from the `alert_sweox_dcn` table.
7. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `MERAKI`
8. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 7.
   2. Insert rows into the `asset_inventory_alert_sweox` table using values from the `alert_sweox_meraki` table.
9. Get a count of the rows in `base_table_partition_info` that match **customerId** where
    - **partitionStatus** is `A` (Active) and
    - **partitionTag** is `BASE` and
    - **mgmtSystemType** is `DCC`
10. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 9.
   2. Insert rows into the `asset_inventory_alert_sweox` table using values from the `alert_sweox_dcc` table.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne
- alert_sweox_dcc
- alert_sweox_dcn
- alert_sweox_ib_data
- alert_sweox_meraki
- alert_sweox_telemetry
- asset_inventory_alert_sweox
- base_table_partition_info
- data_merge_logs
- networkelement

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
