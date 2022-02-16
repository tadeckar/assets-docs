+++
title = "stale_uploads_cleanup_prc"
+++

{{% notice note %}}
This procedure runs once every day.
{{% /notice %}}

### What does it do?
Updates the **processingStatus** of 2-day-old rows in `asset_inventory_notification` to be `FAILED` after first verifying whether or not the device count for the **customerId**/**wfId** is changing within a 3-minute timespan.
{{% expand "More Details" %}}
1. Get a cursor over `asset_inventory_notification` where
   - **processingStart** is greater than 2 days ago, is also not null/undefined,  and
   - **processingStatus** is `STARTED`
2. Open a read loop on the cursor that
   1. Gets a device count by
      - When **mgmtSystemType** is `DNAC`:
        - Get a count of rows in `networkelement_telemetry` table that match the row's **customerId**/**wfId**.
      - Otherwise
        - Get a count of rows in `networkelement_ib_data` table that match the row's **customerId**/**wfId**.
   2. Sleeps for 180 seconds.
   3. Gets the device count again.
   4. If the 2 counts are the same (no devices have been added in 3 minutes,) update the **processingStatus** of the rows to `FAILED`.
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- data_merge_logs
- networkelement_ib_data
- networkelement_telemetry

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
