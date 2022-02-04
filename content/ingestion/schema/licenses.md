+++
title = "Licenses Schema"
+++

{{< mermaid >}}
classDiagram
  class License {
    +Boolean isPDL
    +Long generatedAt
    +Long licenseEndDate
    +Long purchasedQuantity
    +String cavBUId
    +String cavBUName
    +String cavId
    +String cavName
    +String customerId
    +String licenseLevel
    +String licenseStatus
    +String licenseType
    +String orgId
    +String orgName
    +String sourceLicenseStatus
    +String wfId
  }
{{< /mermaid >}}
