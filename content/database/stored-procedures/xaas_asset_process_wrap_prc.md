+++
title = "xaas_asset_process_wrap_prc"
+++

### What does it do?
Call stored procedures to create summary views for XAAS assets.
{{% expand "More Details" %}}
1. Get a count of the rows in the `customer_wfid_info` table that match **customerId**/**wfId** where
   - **module** is `DCC_SUB` and
   - **wfIdStatus** is `I`
2. If the count is 0, then insert a row.
3. Call stored procedures
   1. Call the `xaas_sub_data_process_prc` stored procedure
   2. Call the `xaas_sub_license_prc` stored procedure
4. Delete any row from the `customer_wfid_info` table matching **customerId**/**wfId** where **wfIdStatus** is `A`.
5. Update **wfIdStatus** to `A` for any row from the `customer_wfid_info` table matching **customerId**/**wfId** where **wfIdStatus** is `I`.
6. Delete any rows from the following tables that match **customerId** but don't match **wfId**:
   - `networkelement_sub_stg`
   - `subscription_stg`
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- customer_wfid_info
- networkelement_sub_stg
- subscription_stg

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- xaas_sub_data_process_prc
- xaas_sub_license_prc
