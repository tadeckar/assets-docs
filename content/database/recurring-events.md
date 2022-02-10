+++
title = "Recurring Events"
+++

### Recurring Events
```json
[
	{
		"Name" : "athena_sub_process_01",
		"Interval value" : "10",
		"Interval field" : "SECOND",
        ...
	},
	{
		"Name" : "clean_base_part_invalid_status",
		"Interval value" : "1",
		"Interval field" : "DAY",
        ...
	},
	{
		"Name" : "clean_stale_datamerge",
		"Interval value" : "30",
		"Interval field" : "MINUTE",
        ...
	},
	{
		"Name" : "clean_stale_partitions",
		"Interval value" : "1",
		"Interval field" : "DAY",
        ...
	},
	{
		"Name" : "clean_sum_part_invalid_status",
		"Interval value" : "1",
		"Interval field" : "DAY",
        ...
	},
	{
		"Name" : "data_merge_process_01",
		"Interval value" : "20",
		"Interval field" : "SECOND",
        ...
	},
	{
		"Name" : "data_process_writer_cleanup_script",
		"Interval value" : "1",
		"Interval field" : "DAY",
        ...
	},
	{
		"Name" : "drop_pending_partitions",
		"Interval value" : "1",
		"Interval field" : "DAY",
        ...
	},
	{
		"Name" : "iso_data_merge_cleanup_process",
		"Interval value" : "4",
		"Interval field" : "HOUR",
        ...
	},
	{
		"Name" : "iso_data_merge_process_01",
		"Interval value" : "30",
		"Interval field" : "SECOND",
        ...
	},
	{
		"Name" : "meraki_license_process_01",
		"Interval value" : "30",
		"Interval field" : "SECOND",
        ...
	},
	{
		"Name" : "retry_failed_data_process_writer",
		"Interval value" : "12",
		"Interval field" : "HOUR",
        ...
	},
	{
		"Name" : "stale_inprogress_upload_cleanup",
		"Interval value" : "30",
		"Interval field" : "MINUTE",
        ...
	},
	{
		"Name" : "sub_data_merge_process_01",
		"Interval value" : "30",
		"Interval field" : "SECOND",
        ...
	},
	{
		"Name" : "xass_asset_process_01",
		"Interval value" : "30",
		"Interval field" : "SECOND",
        ...
	}
]
```
#### Event to Stored Procedure Mapping
- **athena_sub_process_01**: `athena_asset_notification_prc`
- **clean_base_part_invalid_status**: `clean_invalid_status_prc`
- **clean_stale_datamerge**: `clean_stale_datamerge_prc`
- **clean_stale_partitions**: `drop_stale_partions_prc`
- **clean_sum_part_invalid_status**: `clean_invalid_wfId_status_sum_tables_prc`
- **data_merge_process_01**: `inv_upload_notification_prc`
- **data_process_writer_cleanup_script**: `stale_uploads_cleanup_prc`
- **drop_pending_partitions**: `drop_pending_wfid_status_sum_tables_prc`
- **iso_data_merge_cleanup_process**: `cleanup_longrunning_iso_data_prc`
- **iso_data_merge_process_01**: `amp_upload_notification_prc`
- **meraki_license_process_01**: `meraki_license_notification_prc`
- **retry_failed_data_process_writer**: `retry_failed_uploads_prc`
- **stale_inprogress_upload_cleanup**: `stale_inprogress_data_cleanup_prc`
- **sub_data_merge_process_01**: `amp_subscription_notification_prc`
- **xass_asset_process_01**: `xaas_asset_notification_prc`
