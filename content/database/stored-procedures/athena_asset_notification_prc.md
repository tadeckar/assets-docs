+++
title = "athena_asset_notification_prc"
+++

{{% notice note %}}
This procedure runs every 10 seconds.
{{% /notice %}}

### What does it do?
Checks for any rows of the `asset_data_load_notification` table that are in the `SUBMITTED` state. If there are any, it updates the state to `INPROGRESS`, then runs the `athena_dcc_dcn_data_process_prc` procedure. Afterwards, it changes the state of those rows again to `SUCCESS`.

{{% expand "More Details" %}}
1. Gets a cursor over the `asset_data_load_notification` table for rows where:
  - **processingStatus** is `SUBMITTED` and
  - **dataSource** is `ATHENA` and
  - the **customerId** has no other rows where **processingStatus** is `INPROGRESS`
2. Gets counts of:
  - AMP subscriptions where **processingStatus** is `SUBMITTED`
  - AMP subscriptions where **processingStatus** is `INPROGRESS`
3. Gets the max parallel limit for `INPROGRESS` uploads from `upd_or_async_prop_master` table
4. If `SUBMITTED` count is > 0 and the `INPROGRESS` count is less than the max parallel limit:
  - Start a read loop that:
    - First checks for `INPROGRESS` count, if count > 0 then log info message and continue
    - Get the wfId from a row
    - Update rows from `SUBMITTED` to `INPROGRESS` **processingStatus**
    - If any rows were updated, call the `athena_dcc_dcn_data_process_prc` with customerId and wfId
    - Finally, set the **processingStatus** of the updated rows to `SUCCESS`
{{% /expand %}}

### Referenced Tables
- asset_data_load_notification
- upd_or_async_prop_master

### Referenced Stored Procedures
- amp_log_msg_prc
- athena_dcc_dcn_data_process_prc
