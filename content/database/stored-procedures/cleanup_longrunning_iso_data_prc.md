+++
title = "cleanup_longrunning_iso_data_prc"
+++

{{% notice note %}}
This procedure runs every 4 hours.
{{% /notice %}}

### What does it do?
Checks for rows of `asset_data_load_notification` that have been `INPROGRESS` for over 2 hours. Updates the status of those rows to `SUBMITTED`. Also, updates rows that have been `SCHEDULED` for over 2 hours to `RECEIVED`.
{{% expand "More Details" %}}
1. Get a cursor over the `asset_data_load_notification` where
   - **processingStart** is over 2 hours ago, also not null/undefined, and
   - **processingStatus** is `INPROGRESS`
2. Get a count of rows in the `asset_data_load_notification` table where
   - **processingStart** is over 2 hours ago, also not null/undefined, and
   - **processingStatus** is `INPROGRESS` or `SCHEDULED`
3. If the count is > 0, open a read loop on the cursor that
   1. Update the **processingStatus** to `SUBMITTED` and the **processingEnd** to the current time for any `INPROGRESS` rows that were started over 2 hours ago.
   2. Update the **processingStatus** to `RECEIVED` and the **processingEnd** to the current time for any `SCHEDULED` rows that were started over 2 hours ago.
{{% /expand %}}

### Referenced Tables
- asset_data_load_notification
- data_merge_logs

### Referenced Stored Procedures
- amp_log_msg_prc
