+++
title = "inv_upload_notification_prc"
+++

{{% notice note %}}
This procedure runs every 20 seconds.
{{% /notice %}}

### What does it do?
Checks for rows in `asset_inventory_notification` that are in `SUBMITTED` state. Changes the state to `INPROGRESS` and calls the [update_raw_data_process_prc]({{< ILink href="/database/stored-procedures/update_raw_data_process_prc" >}}) stored procedure on the rows. On completion, changes the state to `SUCCESS`.
{{% expand "More Details" %}}
1. Gets a cursor on `asset_inventory_notification` where
   - **processingStatus** is `SUBMITTED` and
   - no other rows of the selected **customerId** have **processingStatus** that is `INPROGRESS`
2. Get a count of the number of `SUBMITTED` rows and a count of the number of `INPROGRESS` rows.
3. If `SUBMITTED` count is > 0 and `INPROGRESS` count is < 5, begin a read loop over the cursor that:
   1. Check for any `INPROGRESS` rows on the given **customerId**. If the count is > 0, do not proceed.
   2. Select one `SUBMITTED` row from `asset_inventory_notification` that matches the **customerId**.
   3. Update **processingStatus** to be `INPROGRESS` for all rows that match **customerId**, **wfId**, **processingStatus**, **mgmtSystemType**, and **mgmtSystemId** of previously selected row.
   4. If > 0 rows were updated, call the [update_raw_data_process_prc]({{< ILink href="/database/stored-procedures/update_raw_data_process_prc" >}}) stored procedure with fields from the row.
   5. Update **processingStatus** to be `SUCCESS` for the affected rows.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- data_merge_logs

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [update_raw_data_process_prc]({{< ILink href="/database/stored-procedures/update_raw_data_process_prc" >}}) 
