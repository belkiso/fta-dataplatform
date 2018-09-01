# Fast Track for Azure - Databricks

This folder is work in progress, please stay tuned! 

# Abstract

During this module you download a sample data file (JSON) and upload the file to Azure Blob Storage so we can create an Azure Databricks job (aka Spark Job) to work on this sample data.

# Learning Objectives

By the end of this module you will be able to:

* Download a sample data file (JSON) and upload the file to Azure Blob Storage

## Pre-Requisites

*  Azure Databricks Workspace is already created on your subscription.


# Estimated time to complete this module:
Self-guided (5 minutes approx)

# Download a sample JSON data file and save it into Azure blob storage.

1. Download this sample JSON data file from Github onto your local computer. Right-click and save as to save the raw file locally.

2. If you don't already have a storage account, create one.

* In the Azure portal, select **Create a resource**. Select the **Storage** category, and select **Storage Accounts**
* Provide a unique name for the storage account.
* Select Account Kind: **Blob Storage**
* Select a **Resource Group** name. Use the same resource group you created the Databricks workspace.

For more information, see [Create an Azure Blob storage account] (https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-account).

3. Create a storage Container in the Blob Storage account and upload the sample json file into the container. You can use the Azure portal or the [Microsoft Azure Storage Explorer] (https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer) to upload the file.

* Open the storage account in the Azure portal.
* Select **Blobs**.
* Select + **Container** to create a new empty container.
* Provide a **Name** for the container, such as *databricks*.
* Select Private (non anonymous access) access level.
* Once the container is created, select the container name.
* Select the **Upload** button.
* On the **Files** page, select the **Folder icon** to browse and select the sample file *small_radio_json.json* for upload.
* Select **Upload** to upload the file.