 # Fast Track for Azure - SQL Database

This folder is work in progress, please stay tuned! 

# Abstract

During this module you will learn how to import a database into Azure SQL Database using a database extract (bacpac)

# Learning Objectives

By the end of this module you will be able to:

* Import a database into Azure SQL DB from a bacpac file

## Pre-Requisites

* To complete this module you will need to:
    * Download the reference database [WorldWide-Importers-Standard.bacpac](https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Standard.bacpac)
    * A Storage account and a container in blob storage
    * The reference database uploaded to the container in blob storage
    * You should have completed the Create-blank-azure-sqldb Tutorial First or have an existing logical SQL Server created.

# Estimated time to complete this module:
Self-guided (10 minutes approx)

    
# Importing a Database

To start the import process you need to: 

* Click on the SQL Server to open the Server blade
* Press "Import Database" from the menu at the top

    ![Screenshot](media/4-import-database-into-azure-sqldb/sqldb-import-sqldb.png)

On the SQL Database blade you need to:

* Select your subscription from the drop down menu
* Browse to the .bacpac file that you uploaded into blob storage
* Change the Pricing Tier to Premium P2 for the import
* Rename the database to "WorldImporters"
* Change the Authentication to SQL Server
* Enter the useranme and password that you used to provision the logical server with
* Press OK to start the import

**NOTE**
>You should set the pricing tier when importing a database to a Premium level so that the import can complete quickly with plenty of resources.  Once imported you can scale the database down to a standard level if required.
>

![Screenshot](media/4-import-database-into-azure-sqldb/sqldb-import-db-options.png)

# Monitoring the Import Progress

Once the import is underway, you can monitor the progress by clicking on the Import/Export History tile located on the logical SQL Server blade.

![Screenshot](media/4-import-database-into-azure-sqldb/sqldb-import-export.png)

# Using SQLPackage.exe

For performance and reliability when migrating production databases and larger databases, it is recommended to use the SQLPackage.exe utility that ships with SQL Server Management Studio and SQL Server Data Tools.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

![Screenshot](media/4-import-database-into-azure-sqldb/sqldb-sqlpackage-import.png)



