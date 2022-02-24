+++
title = "psirt_alerts_data_merge_prc"
+++

### What does it do?
Insert rows into the `asset_inventory_alert_psirt` table using values from various other tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
2. Delete all rows for the given **customerId**/**wfId** from the `asset_inventory_alert_psirt` table.
3. Get a count of rows in `base_table_partition_info` that match **customerId**/**wfId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
4. If the count is > 0, open a read loop on the cursor that inserts rows into the `asset_inventory_alert_psirt` table using values from the `alert_psirt_telemetry` table.
6. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `APIC`
7. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 6.
   2. Insert rows into the `asset_inventory_alert_psirt` table using values from the `alert_psirt_dcn` table.
8. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `MERAKI`
9. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 6.
   2. Insert rows into the `asset_inventory_alert_psirt` table using values from the `alert_psirt_meraki` table.
10. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DCC`
11. If the count is > 0: 
   1. Get the **wfId** from rows of count in step 6.
   2. Insert rows into the `asset_inventory_alert_psirt` table using values from the `alert_psirt_dcc` table.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne 
- alert_psirt_dcc
- alert_psirt_dcn
- alert_psirt_meraki
- alert_psirt_telemetry
- asset_inventory_alert_psirt 
- base_table_partition_info
- data_merge_logs

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
