+++
title = "meraki_license_notification_prc"
+++

{{% notice note %}}
This procedure runs every 30 seconds.
{{% /notice %}}

### What does it do?
Checks for `SUBMITTED` rows in `asset_data_load_notification`. Transitions them to `INPROGRESS` state and then calls the `meraki_lic_process_wrap_prc` stored procedure. Afterward, updates the state to `SUCCESS` for the affected rows.
{{% expand "More Details" %}}
1. Gets a cursor over `asset_data_load_notification` where:
   - **processingStatus** is `SUBMITTED` and
   - **dataSource** is `MERAKI_LICENSE` and
   - the **customerId** has no other rows where **processingStatus** is `INPROGRESS`
2. Get counts for:
   - Number of rows in `SUBMITTED` state
   - Number of rows in `INPROGRESS` state
3. Get the max number of parallel uploads from the `upd_or_async_prop_master` table
4. If `SUBMITTED` count > 0 and `INPROGRESS` count < max parallel uploads, open a read loop that:
   1. Checks if any rows are `INPROGRESS` for the current **customerId**. If so: does nothing, otherwise
   2. Gets the wfId
   3. Updates **processingStatus** to `INPROGRESS` on rows where **customerId**/**wfId** match and **processingStatus** is `SUBMITTED`.
   4. If any were updated, call the `meraki_lic_process_wrap_prc` stored procedure on the **customerId**/**wfId**.
   5. Update **processingStatus** to `SUCCESS` for affected rows.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- asset_data_load_notification
- upd_or_async_prop_master

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [meraki_lic_process_wrap_prc]({{< ILink href="/database/stored-procedures/meraki_lic_process_wrap_prc" >}})
