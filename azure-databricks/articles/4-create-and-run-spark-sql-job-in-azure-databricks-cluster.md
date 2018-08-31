# Fast Track for Azure - Databricks

This folder is work in progress, please stay tuned! 

# Abstract

During this module you will learn how to create a notebook in Azure Databricks and run the notebook interactively

# Learning Objectives

By the end of this module you will be able to:

* Use the Azure Databricks portal to create a notebook
* Run the notebook interactively and observer the result of our code execution

## Pre-Requisites

*  Azure Databricks Workspace is already created on your subscription.

# Estimated time to complete this module:
Self-guided (10 minutes approx)

# Creating a notebook and run the notebook interactively

To create a notebook in Azure Databricks workspace:

1. In the left pane, click **Workspace**. From the **Workspace** drop-down, click **Create**, and then click **Notebook**

![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-1.jpg)

Alternatively, you can also create a new notebook from the main Azure Databricks Portal. Click **New Notebook** from the main portal page, as shown below.
![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-11.jpg)

2. In the **Create Notebook** dialog box, enter a name, select **Scala** as the language (by default **Python** is select, you can use **Python**, **Scala**, **SQL** or **R** as a language for your notebook)
3. Select the Spark cluster that you created earlier and then click **Create**

![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-2.jpg)

Please note that, if you have a cluster created but the cluster is not running at the moment, you won't see the cluster option in the dialog box, as shown below. In this scenario, you can attach your notebook later, after it is created, before you run it, you would just have to start your cluster first.

![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-21.jpg)


4. We will now have to associate our data source (in this notebook scenario, our Azure Blob Storage for our sample data). There are two ways to accomplish this association. You can **mount the Azure Storage account to the Databricks Filesystem (DBFS)**, or **directly access** the Azure Storage account from the application you create

We will use the following scala code snippet, to mount Azure Storage account path is mounted to /mnt/mypath in Azure Databricks File System (DBFS). Please replace *YOUR CONTAINER NAME*, *YOUR STORAGE ACCOUNT NAME*, and *YOUR STORAGE ACCOUNT ACCESS KEY* with the appropriate values for your Azure Storage account. Paste the snippet in an empty cell in the notebook and then press **SHIFT + ENTER** to run the code cell. After the mounting, in all future occurrences where you access the Azure Storage account without giving the full path. You can just use /mnt/mypath.

dbutils.fs.mount(
source = "wasbs://{YOUR CONTAINER NAME}@{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net/",
mountPoint = "/mnt/mypath",
extraConfigs = Map("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net" -> "{YOUR STORAGE ACCOUNT ACCESS KEY}"))

For instructions on how to retrieve the storage account key, see [Manage your storage access keys!] (https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account#manage-your-storage-account).

To execute the code, in the cell ("cell is where we write out code in Azure Databricks Notebook"), you can press **SHIFT + ENTER**.

Below screenshot shows another way of running the cell (the snippet of code), in your notebook

![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-3.jpg)

5. Run a SQL statement to create a temporary table using data from the sample JSON data file, *small_radio_json.json*. In the following snippet, replace the placeholder values with your container name and storage account name. Paste the snippet in a code cell in the notebook, and then press **SHIFT + ENTER**. In the snippet, path refer to the location of the sample JSON file that you uploaded to your Azure Storage account.
    %sql 
    DROP TABLE IF EXISTS radio_sample_data;
    CREATE TABLE radio_sample_data
    USING json
    OPTIONS (
    path "/mnt/mypath/small_radio_json.json"
    )

Please **note** that, in the code above, we are using magic command (%sql) to change the language context

Once the command successfully completes, you have all the data from the JSON file as a table in Databricks cluster.

The %sql language magic command enables you to run a SQL code from the notebook, even if the notebook is of another type. For more information, see [Mixing languages in a notebook!] (https://docs.azuredatabricks.net/user-guide/notebooks/index.html#mixing-languages-in-a-notebook)

6. Let's look at a snapshot of the sample JSON data to better understand the query that you run. Paste the following snippet in the code cell and press **SHIFT + ENTER**.
    %sql 
    SELECT * from radio_sample_data

You see a tabular output as shown in the following screenshot:
![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-4.jpg)

You can create a visual representation of data. We will look into the visual representation (charts etc.) in another walkthrough.

7, After reviewing the output, once you are done testing your notebook processing logic, you may want to stop the cluster so you can avoid unnecessary  compute charges.  To stop the cluster, navigate to **Clusters** tab, hover over your cluster and click on **Terminate** button, as shown below:  

![Screenshot](media\4-create-and-run-spark-sql-job-in-azure-databricks-cluster/create-and-run-spark-sql-job-in-azure-databricks-cluster-5.jpg)