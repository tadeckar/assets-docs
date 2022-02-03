+++
title = "Workflow"
+++

{{<mermaid>}}
graph LR;
  subgraph Verify Data Load
  VDL{Verify Data load}
  end
  subgraph Notify Success
  VDL --> NS(Notify)
  end
  subgraph Notify Failure
  VDL --> NF(Notify)
  end
  subgraph IBES Data Loader
    LBM(Load Bulletin Master) --> VDL
    LNE(Load Network Element) --> VDL
    LE(Load Equipments) --> VDL
    LA(Load Alerts) --> VDL
    LC(Load Contracts) --> VDL
    LF(Load Features) --> VDL
  end
  subgraph Pre Processor
    P(Preprocess) --> LBM
    P(Preprocess) --> LNE
    P(Preprocess) --> LE
    P(Preprocess) --> LA
    P(Preprocess) --> LC
    P(Preprocess) --> LF
  end
{{</mermaid>}}

The Glue workflow begins at the **Pre Processor** state. This state is `type: Pass` which allows for state that does not produce any work. Next, the **IBES Data Loader** state loads the data from S3 into the SQL DB. Finally, the **Verify Data Load** state checks that all tasks within the **IBES Data Loader** state were successful. Based on the results, state transitions to either **Notify Success** or **Notify Failure**, at which time the workflow is complete.

See [Loaders](/pages/tadeckar/assets-docs/ingestion/loaders) for more information on the tasks within the **IBES Data Loader** state.
