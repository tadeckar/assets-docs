+++
title = "sum_table_data_update_prc"
+++

### What does it do?
Calls stored procedures related to updating summary tables.
{{% expand "More Details" %}}
1. Calls the following stored procedures sequentially:
   - [networkelement_sum_vw_prc]({{< ILink href="/database/stored-procedures/networkelement_sum_vw_prc" >}})
   - equipment_sum_vw_prc
   - contractcoverage_sum_vw_prc
   - psirt_alert_sum_vw_prc
   - fn_alert_sum_vw_prc
   - hweox_alert_sum_vw_prc
   - sweox_alert_sum_vw_prc
   - [all_assets_vw_prc]({{< ILink href="/database/stored-procedures/all_assets_vw_prc" >}})
   - all_assets_track_vw_prc
   - default_group_device_sum_prc
   - contract_group_device_sum_upl_prc
   - all_csdf_contract_view_prc
   - features_sum_vw_prc
{{% /expand %}}

### Referenced Tables
- data_merge_logs

### Referenced Stored Procedures
- all_assets_track_vw_prc
- [all_assets_vw_prc]({{< ILink href="/database/stored-procedures/all_assets_vw_prc" >}})
- all_csdf_contract_view_prc
- contract_group_device_sum_upl_prc
- contractcoverage_sum_vw_prc
- default_group_device_sum_prc
- equipment_sum_vw_prc
- features_sum_vw_prc
- fn_alert_sum_vw_prc
- hweox_alert_sum_vw_prc
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [networkelement_sum_vw_prc]({{< ILink href="/database/stored-procedures/networkelement_sum_vw_prc" >}})
- psirt_alert_sum_vw_prc
- sweox_alert_sum_vw_prc
