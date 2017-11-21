# Fast Track for Azure - SQL Database

This folder is work in progress, please stay tuned! 

# Abstract

During this module you will learn how to capture performance metrics from a physical or virtual SQL Server and then upload that data for analysis in the DTU calculator

# Learning Objectives

By the end of this module you will be able to:
* Capture performance data from a physical or virtual machine
* Upload the data for analysis in the DTU calculator


## Pre-Requisites

* To complete this module you will need to:
    * Download the sample .csv file [here](https://raw.githubusercontent.com/Azure/fta-dataplatform/master/azure-sql-database/articles/artefacts/sql-perfmon-log.zip)

# Estimated time to complete this module:
Self-guided (5 minutes approx)

# Capturing Performance Data

The [DTU calculator](http://dtucalculator.azurewebsites.net/) is a website in Azure that allows the user to upload performance data captures in perfmon, relating to a local instance of SQL Server.  he DTU calculator analyses this data and then makes recommendations on the performance tier to use when migrating that server to Azure SQL Database.

The DTU calculator can provide guidance for Single databases as well as elastic pool

To capture the correct performance data, you should download and run the collection scripts provides on the DTU calculator website.  There are two flavors of script:
* [Command Line](http://dtucalculator.azurewebsites.net/Downloads/sql-perfmon-cl.zip)
* [PowerShell](http://dtucalculator.azurewebsites.net/Downloads/sql-perfmon-ps.zip)

The scrips are configured to capture performance data ever seconds for 1 hour in CSV format.  You can exit the script execution early but the more data the you have, the better the recommendation will be

# Uploading for Analysis

Once you have captured the performance data you can upload the CSV into the calculator using the Upload field on the Webpage.

* Unzip the sample csv file fro the pre-requisites zip file
* Upload to the calculator as a single database sample
* Enter **4** as the number of cores

# Analysis Results

Once the calculator has reviewed the data it will give an approximate recommendation on the performance tier you should select to run that database in Azure SQL DB.

![Screenshot](media/2-using-the-dtu-calculator/sqldb-DTU-Results.png)
