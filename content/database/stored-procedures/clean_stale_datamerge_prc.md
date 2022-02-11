+++
title = "clean_stale_datamerge_prc"
+++

{{% notice note %}}
This procedure runs every 30 minutes.
{{% /notice %}}

### What does it do?
Updates status of long-running (over 2-day old) notifications from `INPROGRESS` to `FAILED`.
{{% expand "More Details" %}}
1. Gets a cursor over `asset_inventory_notification` where
   - **processingStatus** is `INPROGRESS`
   - **processingStart** was over 2 days ago
2. Loop over cursor, updating each row's **processingStatus** to `FAILED`
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- data_merge_logs


### Referenced Stored Procedures
- log_msg_prc
