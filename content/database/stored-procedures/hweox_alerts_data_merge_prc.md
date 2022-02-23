+++
title = "hweox_alerts_data_merge_prc"
+++

### What does it do?
Insert rows into the `asset_inventory_alert_hweox` table using values from various other tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
2. Delete all rows for the given **customerId**/**wfId** from the `asset_inventory_alert_hweox` table.
3. Get the **wfId** from rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `CSDFIB`
4. Get a count of rows in `base_table_partition_info` that match **customerId**/**wfId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
5. If the count is > 0, open a read loop on the cursor that inserts rows into the `asset_inventory_alert_hweox` table using values from the `alert_hweox_telemetry` table.
6. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `APIC`
7. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 6.
   2. Insert rows into the `asset_inventory_alert_hweox` table using values from the `alert_hweox_dcn` table.
8. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `MERAKI`
9. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 6.
   2. Insert rows into the `asset_inventory_alert_hweox` table using values from the `alert_hweox_meraki` table.
10. If the **wfId** from step 3 is not null, insert rows into the `asset_inventory_alert_hweox` table using values from the `alert_hweox_ib_data` table.
11. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DCC`
12. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 6.
   2. Insert rows into the `asset_inventory_alert_hweox` table using values from the `alert_hweox_dcc` table.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne
- alert_hweox_dcc
- alert_hweox_dcn
- alert_hweox_ib_data
- alert_hweox_meraki
- alert_hweox_telemetry
- asset_inventory_alert_hweox
- base_table_partition_info
- data_merge_logs
- networkelement

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
