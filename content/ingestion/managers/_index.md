+++
title = "Managers"
+++

The main Glue function determines what to load using the `file_type` argument (see [File Types]({{< ILink href="/ingestion/types/file-types" >}})). This argument is passed to a "Manager" to determine how the data is handled.

The **DataFileManager** is used in all scenarios. This contains logic to return a "Request Handler", which is another "Manager" for a particular data type.

The "Request Handler" returned by the **DataFileManager** will be one of the following:
- **InventoryDataLoadManager**
- **ParquetDataLoadManager**
- **LicenseDataLoadManager** 
- **HybridSubscriptionDataLoadManager**  

Each of these implements a common interface:

`handleRequest`: Generic handler for loading data.  
`submitDataLoadRequest`:  Begins the data loading job.  
`processDataFile`: Creates a thread pool to handle data loading.  

The general flow of Manager execution is:
1. `handleRequest`
2. `start.*Processing`
3. `processDataFile`
4. `submitDataLoadRequest`

The `submitDataLoadRequest` function instantiates a [DataLoadManager]({{< ILink href="/ingestion/managers/data-load-manager" >}}) which returns a [Loader]({{< ILink href="/ingestion/loaders" >}}) class to further handle the request.

### More Info
{{% children %}}
