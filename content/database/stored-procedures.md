+++
title = "Stored Procedures"
+++

Recurring Stored Procedures
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
