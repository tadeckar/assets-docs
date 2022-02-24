+++
title = "drop_dnac_old_partions_prc"
+++

### What does it do?
Drops partitions using the `drop_partions_prc` stored procedure given a set of parameters.
{{% expand "More Details" %}}
1. Gets a cursor over `base_table_partition_info` where **customerId**, **dnacId**, **partitionStatus**, **partitionTag**, and **mgmtSystemType**  match the given parameters.
2. Create a read loop on the cursor that calls [drop_partions_prc]({{< ILink href="/database/stored-procedures/drop_partions_prc" >}}) with arguments from each row.
{{% /expand %}}

### Referenced Tables
- base_table_partition_info

### Referenced Stored Procedures
- [drop_partions_prc]({{< ILink href="/database/stored-procedures/drop_partions_prc" >}})
