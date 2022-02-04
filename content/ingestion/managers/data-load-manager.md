+++
title = "DataLoadManager"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/master/glue/cp-asset-data-import-job/csco/dp/manager/DataLoadManager.py" >}}

Similar to [DataFileManager]({{< ILink href="/ingestion/managers/data-file-manager" >}}), the DataLoadManager simply picks a [Loader]({{< ILink href="/ingestion/loaders" >}}) to use given a [Data Load Type]({{< ILink href="/ingestion/types/data-load-types" >}}).
