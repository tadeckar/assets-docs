+++
title = "cp-assets-data-import-sf-trigger"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/505d1b955f2ccf5f2038b8023535327d4b532fda/lambda/cp-assets-data-import-sf-trigger/lambda_function.py" >}}

Receives SQS events and parses information to trigger the step-function. The step-function then routes to either the [cp-asset-csv-data-loader]({{< ILink href="/ingestion/lambdas/cp-asset-csv-data-loader" >}}) lambda function or the Glue ETL Job (starting at [DataFileManager]({{< ILink href="/ingestion/managers/data-file-manager" >}})) based on the message's **recordType**.
