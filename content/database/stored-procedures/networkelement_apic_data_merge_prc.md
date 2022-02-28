+++
title = "networkelement_apic_data_merge_prc"
+++

### What does it do?
Inserts rows into the `networkelement` table using values from the `networkelement_dcn` table.
{{% expand "More Details" %}}
1. Count rows in the `asset_inventory_notification` table that match **customerId**/**wfId** where **mgmtSystemType** is `APIC`.
2. If the count is > 0, call the following stored procedures in sequence:
   - [apic_advisory_update_prc]({{< ILink href="/database/stored-procedures/apic_advisory_update_prc" >}})
   - [dcn_networkelement_update_prc]({{< ILink href="/database/stored-procedures/dcn_networkelement_update_prc" >}})
   - [athena_dcn_stg_data_process_prc]({{< ILink href="/database/stored-procedures/athena_dcn_stg_data_process_prc" >}})
3. Count rows in the `base_table_partition_info` table that match **customerId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `APIC`
4. If the count is > 0, insert rows into the `networkelement` table using values from the `networkelement_dcn` table.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- base_table_partition_info
- data_merge_logs
- networkelement
- networkelement_dcn

### Referenced Stored Procedures
- [apic_advisory_update_prc]({{< ILink href="/database/stored-procedures/apic_advisory_update_prc" >}})
- [athena_dcn_stg_data_process_prc]({{< ILink href="/database/stored-procedures/athena_dcn_stg_data_process_prc" >}})
- [dcn_networkelement_update_prc]({{< ILink href="/database/stored-procedures/dcn_networkelement_update_prc" >}})
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
