+++
title = "meraki_lic_process_wrap_prc"
+++

### What does it do?
Creates summary views for meraki licenses.
{{% expand "More Details" %}}
1. Get a count of rows matching **customerId**/**wfId** in the `customer_wfid_info` table.
2. If count is 0, add a row.
3. Call the [meraki_license_sum_view_prc]({{< ILink href="/database/stored-procedures/meraki_license_sum_view_prc" >}}) stored procedure with **customerId**/**wfId** as input.
4. Delete the row (if it exists) from the `customer_wfid_info` table where
   - **customerId** matches and
   - **module** is `MERAKI_LICENSE` and
   - **wfIdStatus** is `A`
5. Update **wfIdStatus** to `A` from the row in the `customer_wfid_info` table where
   - **customerId** matches and
   - **module** is `MERAKI_LICENSE` and
   - **wfIdStatus** is `I`
6. Delete the previous **wfId** rows from the `meraki_license_sum_view_stage` table where
   - **customerId** matches input and
   - **wfId** does not match input and
   - **wfId** does not match any **wfId** in `asset_data_load_notification` where **processingStatus** is `SUBMITTED`
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- asset_data_load_notification
- customer_wfid_info
- meraki_license_sum_view_stage

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [meraki_license_sum_view_prc]({{< ILink href="/database/stored-procedures/meraki_license_sum_view_prc" >}})
