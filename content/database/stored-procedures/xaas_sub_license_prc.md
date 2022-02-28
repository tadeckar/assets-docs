+++
title = "xaas_sub_license_prc"
+++

### What does it do?
Inserts rows into the `device_license_view` table using values from `networkelement_sub_stg` and `subscription_stg`.
{{% expand "More Details" %}}
1. Count rows in the `device_license_view` table matching **customerId**/**wfId** from input.
2. If the count is > 0, delete all rows from `device_license_view` matching above count query where **mgmtSystemType** is `DCC_SUB`.
3. Insert rows into `device_license_view` using values from `networkelement_sub_stg` and `subscription_stg`.
4. Call the [upd_athena_xaas_solutionId_prc]({{< ILink href="/database/stored-procedures/upd_athena_xaas_solutionid_prc" >}}) stored procedure.
5. Delete rows from `device_license_view` matching **customerId** where **mgmtSystemType** is `DCC_SUB` and **wfId** is not equal to the **wfId** from input.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- device_license_view
- networkelement_sub_stg
- subscription_stg

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [upd_athena_xaas_solutionId_prc]({{< ILink href="/database/stored-procedures/upd_athena_xaas_solutionid_prc" >}})
