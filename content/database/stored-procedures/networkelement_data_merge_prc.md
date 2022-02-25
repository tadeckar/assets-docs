+++
title = "networkelement_data_merge_prc"
+++

### What does it do?
Inserts rows into `networkelement` using values from various other tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table and
   - **partitionValue** is not equal to the **wfId** input parameter 
2. Delete all rows for the given **customerId**/**wfId** from the `networkelement` table.
3. Get a count of rows in `asset_inventory_notification` that match **customerId**/**wfId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `CSDFIB`
4. If the count is > 0, call the `upd_contract_cxLevel_and_coverage_prc` stored procedure.
5. Get the **wfId** from rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `CSDFIB`
6. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `APIC`
7. If the count is > 0, call the [networkelement_apic_data_merge_prc]({{< ILink href="/database/stored-procedures/networkelement_apic_data_merge_prc" >}}) stored procedure.
8. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `MERAKI`
9. If the count is > 0, call the `networkelement_meraki_data_merge_prc` stored procedure.
10. Get a count of the rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DCC`
11. If the count is > 0, call the `networkelement_dcc_data_merge_prc` stored procedure.
12. Get a count of rows in `base_table_partition_info` that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
13. If the count it > 0, call the [networkelement_cxc_data_merge_prc]({{< ILink href="/database/stored-procedures/networkelement_cxc_data_merge_prc" >}}) stored procedure.
14. If the **wfId** from step 5 is not null:
    1. Get a count of rows in the `asset_inventory_notification` table matching **customerId**/**wfId** where **mgmtSystemType** is `CSDFIB`.
    2. If the count it > 0, call the following stored procedures:
       - ib_advisory_update_prc
       - ib_networkelement_update_prc
       - athena_ib_stg_data_process_prc
    3. Insert rows into `networkelement` using values from `networkelement_ib_data`.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne 
- asset_inventory_notification
- base_table_partition_info
- data_merge_logs
- networkelement
- networkelement_ib_data

### Referenced Stored Procedures
- athena_ib_stg_data_process_prc
- ib_advisory_update_prc
- ib_networkelement_update_prc
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [networkelement_apic_data_merge_prc]({{< ILink href="/database/stored-procedures/networkelement_apic_data_merge_prc" >}})
- [networkelement_cxc_data_merge_prc]({{< ILink href="/database/stored-procedures/networkelement_cxc_data_merge_prc" >}})
- networkelement_dcc_data_merge_prc
- networkelement_meraki_data_merge_prc
- upd_contract_cxLevel_and_coverage_prc
