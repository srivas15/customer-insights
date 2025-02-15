---
title: "Export Customer Insights data to an Azure Blob Storage"
description: "Learn how to configure the connection and export to Blob storage."
ms.date: 06/30/2021
ms.reviewer: mhart
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: how-to
author: pkieffer
ms.author: philk
manager: shellyha
---

# Export segment list and other data to Azure Blob Storage (preview)

Store your Customer Insights data in a Blob storage or use it to transfer your data to other applications.

## Set up the connection to Blob Storage

1. Go to **Admin** > **Connections**.

1. Select **Add connection** and choose **Azure Blob Storage** to configure the connection.

1. Give your connection a recognizable name in the **Display name** field. The name and the type of the connection describe this connection. We recommend choosing a name that explains the purpose and target of the connection.

1. Choose who can use this connection. If you take no action, the default will be Administrators. For more information, see [Allow contributors to use a connection for exports](connections.md#allow-contributors-to-use-a-connection-for-exports).

1. Enter **Account name**, **Account key**, and **Container** for your Blob Storage account.
    - To learn more about how to find the Blob Storage account name and account key, see [Manage storage account settings in the Azure portal](/azure/storage/common/storage-account-manage).
    - To learn how to create a container, see [Create a container](/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container).

1. Select **Save** to complete the connection. 

## Configure an export

You can configure this export if you have access to a connection of this type. For more information, see [Permissions needed to configure an export](export-destinations.md#set-up-a-new-export).

> [!IMPORTANT]
> If you turned on the soft delete setting for the Azure Blob Storage account, exports will fail. Turn off soft delete to export data to blobs. For more information, see [Enable blob soft delete](/azure/storage/blobs/soft-delete-blob-enable.md)

1. Go to **Data** > **Exports**.

1. To create a new export, select **Add destination**.

1. In the **Connection for export** field, choose a connection from the Azure Blob Storage section. If you don't see this section name, then no connections of this type are available to you.

1. Select the box next to each of the entities you want to export to this destination.

1. Select **Save**.

Saving an export doesn't run the export immediately.

The export runs with every [scheduled refresh](system.md#schedule-tab).     

You can also [export data on demand](export-destinations.md#run-exports-on-demand). 

Exported data is stored in the Blob Storage container you configured. The following folder paths are automatically created in your container:

- For source entities and entities generated by the system:  
  `%ContainerName%/CustomerInsights_%instanceID%/%ExportDestinationName%/%EntityName%/%Year%/%Month%/%Day%/%HHMM%/%EntityName%_%PartitionId%.csv`  
  - Example: `Dynamics365CustomerInsights/CustomerInsights_abcd1234-4312-11f4-93dc-24f72f43e7d5/BlobExport/HighValueSegment/2020/08/24/1433/HighValueSegment_1.csv`
 
- The model.json for the exported entities will be at the %ExportDestinationName% level.  
  - Example: `Dynamics365CustomerInsights/CustomerInsights_abcd1234-4312-11f4-93dc-24f72f43e7d5/BlobExport/model.json`

[!INCLUDE[footer-include](../includes/footer-banner.md)]
