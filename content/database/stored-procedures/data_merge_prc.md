+++
title = "data_merge_prc"
+++

### What does it do?
Calls stored procedures related to data merge.
{{% expand "More Details" %}}
1. Calls the following stored procedures sequentially:
   - [alerts_master_data_merge_prc]({{< ILink href="/database/stored-procedures/alerts_master_data_merge_prc" >}})
   - [networkelement_data_merge_prc]({{< ILink href="/database/stored-procedures/networkelement_data_merge_prc" >}})
   - [contract_data_merge_prc]({{< ILink href="/database/stored-procedures/contract_data_merge_prc" >}})
   - [equipment_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_data_merge_prc" >}})
   - psirt_alerts_data_merge_prc
   - [fn_alerts_data_merge_prc]({{< ILink href="/database/stored-procedures/fn_alerts_data_merge_prc" >}})
   - sweox_alerts_data_merge_prc
   - [hweox_alerts_data_merge_prc]({{< ILink href="/database/stored-procedures/hweox_alerts_data_merge_prc" >}})
   - [feature_data_merge_prc]({{< ILink href="/database/stored-procedures/feature_data_merge_prc" >}})
{{% /expand %}}

### Referenced Tables
- data_merge_logs


### Referenced Stored Procedures
- [alerts_master_data_merge_prc]({{< ILink href="/database/stored-procedures/alerts_master_data_merge_prc" >}})
- [contract_data_merge_prc]({{< ILink href="/database/stored-procedures/contract_data_merge_prc" >}})
- [equipment_data_merge_prc]({{< ILink href="/database/stored-procedures/equipment_data_merge_prc" >}})
- [feature_data_merge_prc]({{< ILink href="/database/stored-procedures/feature_data_merge_prc" >}})
- [fn_alerts_data_merge_prc]({{< ILink href="/database/stored-procedures/fn_alerts_data_merge_prc" >}})
- [hweox_alerts_data_merge_prc]({{< ILink href="/database/stored-procedures/hweox_alerts_data_merge_prc" >}})
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
- [networkelement_data_merge_prc]({{< ILink href="/database/stored-procedures/networkelement_data_merge_prc" >}})
- psirt_alerts_data_merge_prc
- sweox_alerts_data_merge_prc
