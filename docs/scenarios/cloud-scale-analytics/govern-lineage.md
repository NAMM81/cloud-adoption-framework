---
title: Data lineage
description: Understand data lineage for data governance.
author: mboswell
ms.author: mboswell
ms.date: 09/26/2024
ms.topic: conceptual
ms.custom: e2e-data-management, think-tank
---

# Data lineage

Data lineage plays an important role in cloud-scale analytics. Lineage shows dependencies between raw data and finished products, describing the transformations and manipulations that turn that raw data into the final data products. Data lineage spans the lifecycle of data, from its origin to its movement across the data estate. It’s used for troubleshooting, root cause analysis, data quality analysis, compliance, and impact analysis. It also adds context to datasets and products that enables data products to be discoverable and self-serviceable.

A primary of any data catalog is its ability to show the lineage between data products.

Microsoft Purview Data Catalog connects with various data processing, storage, and analytics systems to extract lineage information. The goal is to represent the movement, transformation, and operational metadata from each data system.

Azure Data Factory, Azure Synapse pipelines are recommended for ingestion solutions because they enable data lineage in Microsoft Purview. Alternate ingestion patterns should use Apache Atlas API to update data lineage as part of their data processing.

Microsoft Fabric supports lineage without requiring Microsoft Purview. If you require one place to view lineage then we recommend setting Microsoft Purview to scan a Microsoft Fabric tenant as this will automatically bring in metadata and lineage from Fabric items including Power BI into Microsoft Purview Data Catalog. For more information, see [Lineage in Fabric](/fabric/governance/lineage) and [How to get lineage from Microsoft Fabric items into Microsoft Purview](/purview/how-to-lineage-fabric)

> [!TIP]
> For more information on supported systems and best practices, see [Data Lineage in Microsoft Purview](/purview/concept-data-lineage).

## Next steps

Learn how to manage master data in Azure.

> [!div class="nextstepaction"]
> [Master data management](govern-master-data.md)
