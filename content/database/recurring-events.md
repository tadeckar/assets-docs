+++
title = "Recurring Events"
+++

#### Event to Stored Procedure Mapping
- **athena_sub_process_01**: [athena_asset_notification_prc]({{< ILink href="/database/stored-procedures/athena_asset_notification_prc" >}}) - every 10 seconds
- **clean_base_part_invalid_status**: [clean_invalid_status_prc]({{< ILink href="/database/stored-procedures/clean_invalid_status_prc" >}}) - every 1 day
- **clean_stale_datamerge**: [clean_stale_datamerge_prc]({{< ILink href="/database/stored-procedures/clean_stale_datamerge_prc" >}}) - every 30 minutes
- **clean_stale_partitions**: [drop_stale_partions_prc]({{< ILink href="/database/stored-procedures/drop_stale_partions_prc" >}}) - every 1 day
- **clean_sum_part_invalid_status**: [clean_invalid_wfId_status_sum_tables_prc]({{< ILink href="/database/stored-procedures/clean_invalid_wfid_status_sum_tables_prc" >}}) - every 1 day
- **data_merge_process_01**: [inv_upload_notification_prc]({{< ILink href="/database/stored-procedures/inv_upload_notification_prc" >}}) - every 20 seconds
- **data_process_writer_cleanup_script**: [stale_uploads_cleanup_prc]({{< ILink href="/database/stored-procedures/stale_uploads_cleanup_prc" >}}) - every 1 day
- **drop_pending_partitions**: `drop_pending_wfid_status_sum_tables_prc` - every 1 day
- **iso_data_merge_cleanup_process**: `cleanup_longrunning_iso_data_prc` - every 4 hours
- **iso_data_merge_process_01**: `amp_upload_notification_prc` - every 30 seconds
- **meraki_license_process_01**: `meraki_license_notification_prc` - every 30 seconds
- **retry_failed_data_process_writer**: `retry_failed_uploads_prc` - every 12 hours
- **stale_inprogress_upload_cleanup**: `stale_inprogress_data_cleanup_prc` - every 30 minutes
- **sub_data_merge_process_01**: `amp_subscription_notification_prc` - every 30 seconds
- **xass_asset_process_01**: `xaas_asset_notification_prc` - every 30 seconds
