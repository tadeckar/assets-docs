+++
title = "delete_raw_data_wfid_prc"
+++

### What does it do?
Deletes rows matching **customerId**/**wfId** from tables based on a given **mgmtSystemType**.
{{% expand "More Details" %}}
1. Deletes rows that match **customerId**/**wfId** from `base_table_partition_info`.
2. Deletes rows that match **customerId**/**wfId** from tables based on **mgmtSystemType**.
   - When **mgmtSystemType** is `DNAC`, deletes from tables: 
     - active_dnac_ne
     - alert_fn_telemetry
     - alert_hweox_telemetry
     - alert_pas_hw_eox_bulletin_dnac
     - alert_pas_sw_eox_bulletin_dnac
     - alert_psirt_telemetry
     - alert_sweox_telemetry
     - asset_feature_telemetry
     - equipment_telemetry
     - fn_bulletin_master_dnac
     - networkelement_telemetry
     - sa_bulletin_master_dnac
   - When **mgmtSystemType** is `APIC`, deletes from tables: 
     - alert_fn_dcn
     - alert_hweox_dcn
     - alert_pas_hw_eox_bulletin_dcn
     - alert_pas_sw_eox_bulletin_dcn
     - alert_psirt_dcn
     - alert_sweox_dcn
     - equipment_dcn
     - fn_bulletin_master_dcn
     - networkelement_dcn
     - sa_bulletin_master_dcn
   - When **mgmtSystemType** is `CSDFIB`, deletes from tables:
     - alert_fn_ib_data
     - alert_hweox_ib_data
     - alert_pas_hw_eox_bulletin_ib_data
     - alert_pas_sw_eox_bulletin_ib_data
     - alert_psirt_ib_data
     - alert_sweox_ib_data
     - contractcoverage_ib_data
     - equipment_ib_data
     - fn_bulletin_master_ib_data
     - networkelement_ib_data
     - sa_bulletin_master_ib_data
   - When **mgmtSystemType** is `MERAKI`, deletes from tables:
     - alert_fn_meraki
     - alert_hweox_meraki
     - alert_pas_hw_eox_bulletin_meraki
     - alert_pas_sw_eox_bulletin_meraki
     - alert_psirt_meraki
     - alert_sweox_meraki
     - contractcoverage_meraki
     - equipment_meraki
     - fn_bulletin_master_meraki
     - networkelement_meraki
     - sa_bulletin_master_meraki
   - When **mgmtSystemType** is `DCC`, deletes from tables:
     - alert_fn_dcc
     - alert_hweox_dcc
     - alert_pas_hw_eox_bulletin_dcc
     - alert_pas_sw_eox_bulletin_dcc
     - alert_psirt_dcc
     - alert_sweox_dcc
     - equipment_dcc
     - fn_bulletin_master_dcc
     - networkelement_dcc
     - sa_bulletin_master_dcc

{{% /expand %}}

### Referenced Tables
- active_dnac_ne
- alert_fn_dcc
- alert_fn_dcn
- alert_fn_ib_data
- alert_fn_meraki
- alert_fn_telemetry
- alert_hweox_dcc
- alert_hweox_dcn
- alert_hweox_ib_data
- alert_hweox_meraki
- alert_hweox_telemetry
- alert_pas_hw_eox_bulletin_dcc
- alert_pas_hw_eox_bulletin_dcn
- alert_pas_hw_eox_bulletin_dnac
- alert_pas_hw_eox_bulletin_ib_data
- alert_pas_hw_eox_bulletin_meraki
- alert_pas_sw_eox_bulletin_dcc
- alert_pas_sw_eox_bulletin_dcn
- alert_pas_sw_eox_bulletin_dnac
- alert_pas_sw_eox_bulletin_ib_data
- alert_pas_sw_eox_bulletin_meraki
- alert_psirt_dcc
- alert_psirt_dcn
- alert_psirt_ib_data
- alert_psirt_meraki
- alert_psirt_telemetry
- alert_sweox_dcc
- alert_sweox_dcn
- alert_sweox_ib_data
- alert_sweox_meraki
- alert_sweox_telemetry
- asset_feature_telemetry
- base_table_partition_info
- contractcoverage_ib_data
- contractcoverage_meraki
- equipment_dcc
- equipment_dcn
- equipment_ib_data
- equipment_meraki
- equipment_telemetry
- fn_bulletin_master_dcc
- fn_bulletin_master_dcn
- fn_bulletin_master_dnac
- fn_bulletin_master_ib_data
- fn_bulletin_master_meraki
- networkelement_dcc
- networkelement_dcn
- networkelement_ib_data
- networkelement_meraki
- networkelement_telemetry
- sa_bulletin_master_dcc
- sa_bulletin_master_dcn
- sa_bulletin_master_dnac
- sa_bulletin_master_ib_data
- sa_bulletin_master_meraki
