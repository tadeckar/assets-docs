+++
title = "update_sum_data_process_prc"
+++

### What does it do?
Transitions **partitionStatus** of rows in `customer_partition_info`.
{{% expand "More Details" %}}
1. Get a count of rows in the `customer_partition_info` table where
   - **customerId**/**wfId** matches input and
   - **partitionStatus** is `I` (Inprogress) and
   - **partitionTag** matches input
2. If the count is > 0:
   1. Update **customerId**/**wfId** matching rows from **partitionStatus** `A` (Active) to `P` (Previous).
   2. Update **customerId**/**wfId** matching rows from **partitionStatus** `I` (Active) to `A` (Previous).
{{% /expand %}}

### Referenced Tables
- customer_partition_info
- data_merge_logs

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
