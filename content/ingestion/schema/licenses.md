+++
title = "Licenses Schema"
+++

{{< mermaid >}}
classDiagram
  class License {
    ("customerId", "string", "customerId", "string"),
    ("cavId", "string", "cavId", "string"),
    ("cavName", "string", "cavName", "string"),
    ("cavBUId", "string", "cavBUId", "string"),
    ("cavBUName", "string", "cavBUName", "string"),
    ("orgId", "string", "orgId", "string"),
    ("orgName", "string", "orgName", "string"),
    ("licenseLevel", "string", "licenseLevel", "string"),
    ("purchaseQuantity", "long", "purchasedQuantity", "integer"),
    ("licenseEndDate", "long", "licenseEndDate", "long"),
    ("licenseStatus", "string", "licenseStatus", "string"),
    ("licenseType", "string", "licenseType", "string"),
    ("sourceLicenseStatus", "string", "sourceLicenseStatus", "string"),
    ("isPDL", "boolean", "isPDL", "boolean"),
    ("wfId", "string", "wfId", "string"),
    ("generatedAt", "long", "generatedAt", "long")
  }
{{< /mermaid >}}
