+++
title = "alerts_master_data_merge_prc"
+++

### What does it do?
Calls stored procedures related to alerts data merge.
{{% expand "More Details" %}}
1. Calls the following stored procedures sequentially, based on **mgmtSystemType**:
| **mgmtSystemType** | **Stored Procedure Calls**                 |
| ------------------ | --------------------------                 |
| `DNAC`             | [dnac_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dnac_sa_bulletin_master_merge_prc" >}})          |
| `DNAC`             | [dnac_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dnac_fn_bulletin_master_merge_prc" >}})          |
| `DNAC`             | [dnac_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dnac_alert_pas_hw_eox_bulletin_merge_prc" >}})   |
| `DNAC`             | [dnac_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dnac_alert_pas_sw_eox_bulletin_merge_prc" >}})   |
| `CSDFIB`           | [ib_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/ib_sa_bulletin_master_merge_prc" >}})            |
| `CSDFIB`           | [ib_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/ib_fn_bulletin_master_merge_prc" >}})            |
| `CSDFIB`           | [ib_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/ib_alert_pas_hw_eox_bulletin_merge_prc" >}})     |
| `CSDFIB`           | [ib_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/ib_alert_pas_sw_eox_bulletin_merge_prc" >}})     |
| `APIC`             | [dcn_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcn_sa_bulletin_master_merge_prc" >}})           |
| `APIC`             | [dcn_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcn_fn_bulletin_master_merge_prc" >}})           |
| `APIC`             | [dcn_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcn_alert_pas_hw_eox_bulletin_merge_prc" >}})    |
| `APIC`             | [dcn_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcn_alert_pas_sw_eox_bulletin_merge_prc" >}})    |
| `MERAKI`           | [meraki_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/meraki_sa_bulletin_master_merge_prc" >}})        |
| `MERAKI`           | [meraki_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/meraki_fn_bulletin_master_merge_prc" >}})        |
| `MERAKI`           | [meraki_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/meraki_alert_pas_hw_eox_bulletin_merge_prc" >}}) |
| `MERAKI`           | [meraki_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/meraki_alert_pas_sw_eox_bulletin_merge_prc" >}}) |
| `DCC`              | [dcc_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcc_sa_bulletin_master_merge_prc" >}})           |
| `DCC`              | [dcc_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcc_fn_bulletin_master_merge_prc" >}})           |
| `DCC`              | [dcc_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcc_alert_pas_hw_eox_bulletin_merge_prc" >}})    |
| `DCC`              | [dcc_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcc_alert_pas_sw_eox_bulletin_merge_prc" >}})    |
{{% /expand %}}

### Referenced Tables
- data_merge_logs

### Referenced Stored Procedures
- [dnac_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dnac_alert_pas_sw_eox_bulletin_merge_prc" >}})
- [dcc_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcc_alert_pas_hw_eox_bulletin_merge_prc" >}})
- [dcc_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcc_alert_pas_sw_eox_bulletin_merge_prc" >}})              
- [dcc_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcc_fn_bulletin_master_merge_prc" >}})                     
- [dcc_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcc_sa_bulletin_master_merge_prc" >}})                     
- [dcn_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcn_alert_pas_hw_eox_bulletin_merge_prc" >}})              
- [dcn_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dcn_alert_pas_sw_eox_bulletin_merge_prc" >}})              
- [dcn_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcn_fn_bulletin_master_merge_prc" >}})                     
- [dcn_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dcn_sa_bulletin_master_merge_prc" >}})                     
- [dnac_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/dnac_alert_pas_hw_eox_bulletin_merge_prc" >}})             
- [dnac_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dnac_fn_bulletin_master_merge_prc" >}})                    
- [dnac_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/dnac_sa_bulletin_master_merge_prc" >}})                    
- [ib_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/ib_alert_pas_hw_eox_bulletin_merge_prc" >}})               
- [ib_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/ib_alert_pas_sw_eox_bulletin_merge_prc" >}})               
- [ib_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/ib_fn_bulletin_master_merge_prc" >}})                      
- [ib_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/ib_sa_bulletin_master_merge_prc" >}})                      
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [meraki_alert_pas_hw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/meraki_alert_pas_hw_eox_bulletin_merge_prc" >}})           
- [meraki_alert_pas_sw_eox_bulletin_merge_prc]({{< ILink href="/database/stored-procedures/meraki_alert_pas_sw_eox_bulletin_merge_prc" >}})           
- [meraki_fn_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/meraki_fn_bulletin_master_merge_prc" >}})                  
- [meraki_sa_bulletin_master_merge_prc]({{< ILink href="/database/stored-procedures/meraki_sa_bulletin_master_merge_prc" >}})                  
