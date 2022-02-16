+++
title = "amp_upload_notification_prc"
+++

{{% notice note %}}
This procedure runs every 30 seconds.
{{% /notice %}}

### What does it do?
Checks for rows in `asset_data_load_notification` in `SUBMITTED` state where **dataSource** is `CSDF_AMP_TELE`. Transitions the rows to `INPROGRESS` state and calls the [iso_data_process_wrap_prc]({{< ILink href="/database/stored-procedures/iso_data_process_wrap_prc" >}}) stored procedure. Afterwards, updates the state of the rows to `SUCCESS`.
{{% expand "More Details" %}}
1. Get a cursor over the `asset_data_load_notification` table where:
   - **processingStatus** is `SUBMITTED` and
   - **dataSource** is `CSDF_AMP_TELE` and
   - None of the rows for same **customerId** are `INPROGRESS`
2. Get a counts for
   - `SUBMITTED` notifications and
   - `INPROGRESS` notifications
3. Get the max parallel limit of amp uploads from the `upd_or_async_prop_master` table.
4. If the `SUBMITTED` count is > 0 and `INPROGRESS` count is less than the max parallel limit, open a read loop that:
   1. Counts the number of `INPROGRESS` rows for the given **customerId**
   2. If the count is 0 (none `INPROGRESS`), get the **wfId** from a `SUBMITTED` row.
   3. Update the status to `INPROGRESS` of `SUBMITTED` rows with the **wfId** from the previous step.
   4. Call the [iso_data_process_wrap_prc]({{< ILink href="/database/stored-procedures/iso_data_process_wrap_prc" >}}) stored procedure with input data from the row.
   5. Update the status to `SUCCESS` on the affected rows.
{{% /expand %}}

### Referenced Tables
- asset_data_load_notification
- amp_data_merge_logs
- upd_or_async_prop_master

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [iso_data_process_wrap_prc]({{< ILink href="/database/stored-procedures/iso_data_process_wrap_prc" >}})
