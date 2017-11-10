# POC Scenario: Deploying SQL Server on Azure IaaS VMs

# Introduction
The intent of this document is to provide you a single page in which to find the most current guidance for deploying SQL Server into a Virtual Machine in Azure.

In this article we will look at how to deploy:

* A single Virtual Machine running SQL Server
* 2 SQL Server Virtual Machines using Always-On availability Groups
* 2 SQL Server Virtual Machines configured as a fail-over cluster



#### Additional information
* Implementation Scenarios: [SQL Server on Azure virtual machines](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)  

* High level comparision: [SQL Database (PaaS) vs. SQL Server on VMs (IaaS)](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-paas-vs-sql-server-iaas) 

* Detailed feature level comparision: [SQL Database (PaaS) vs. SQL Server on VMs (IaaS)](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-features) 

# Prerequisite 
Before starting this POC you should have:

* An understanding of IaaS fundamentals
* An Active Azure subscription
* Knowledge of SQL Server
* A working Active Directory in Azure (for always-on and Clustering POCs)


# Ramp up
Here few resources that can help you get started with running SQL Server on IaaS VMs:

* [SQL Server on an Azure Virtual Machine: Learning Path](https://azure.microsoft.com/en-us/documentation/learning-paths/sql-azure-vm/) 

* [Overview of SQL Server on Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)


# Performance best practices for SQL Server in Azure Virtual Machines

Running SQL Server in a virtual machine is very similar to running SQL Server on-prem.  There are a number of steps that need to be taken to ensure optimal performance for the SQL engine which include:

* Proper disk provisioning
* Filesystem formatting for SQL Server
* SQL engine configurations
* Database file alignment to disk

In addition to these standard items that should be configured for all SQL Servers, Azure has some additional best practises that will ensure your SQL VM runs at the optimal performance level.  These are all described in the following article.

* [Performance Best Practises for SQL Server on VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)



# Deploying a Single SQL Virtual Machine
Deplying a SQL Server VM within Azure is a simple process which can be achieved either via the portal or from the command line.  

## Provision a single SQL Server virtual machine using Azure Portal

This end-to-end tutorial shows you how to use the Azure Portal to provision a virtual machine running SQL Server. 
The Azure virtual machine gallery includes several images that contain Microsoft SQL Server. With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.

For a step-by-step tutorial please see [Provision a Single SQL Server VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision) 


## Provision a single SQL Server virtual machine using Azure PowerShell 

This tutorial shows you how to create a single Azure virtual machine using the Azure Resource Manager deployment model using Azure PowerShell cmdlets. In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery. 

For a step-by-step tutorial please see [Provision a Single SQL Server VM using PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create) 

# Deploying SQL Server in High Availability Scenarios

## Deploying SQL Server Always On availability groups on Azure virtual machines (Manually)

Deploying SQL Server and setting up Always-ON availablility groups is a common scenario for customers wanting to add high availability and scalability to their environemnt.  In Azure, this can be achieved manually or by using a pre-defined template to do all the configuration for you.

Before starting either of these you will need to ensure you have a domain so that the virtual machines can be domain joined.

For a step-by-step guide to [implementing always-on manually in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial), please follow this link

## Deploying SQL Server Always On availability groups on Azure virtual machines (Template)


This tutorial shows you how to create a SQL Server availability group with Azure Resource Manager virtual machines. The tutorial uses Azure blades to configure a template. You will review the default settings, type required settings, and update the blades in the portal as you walk through this tutorial. 

At the end of the tutorial, your SQL Server availability group solution in Azure will consist of the following elements: 

* A virtual network containing multiple subnets, including a front-end and a back-end subnet

* Two domain controllers with an Active Directory (AD) domain

* Two SQL Server VMs deployed to the back-end subnet and joined to the AD domain

* A 3-node WSFC cluster with the Node Majority quorum model

* An availability group with two synchronous-commit replicas of an availability database

The figure below is a graphical representation of the solution.
![Screenshot](media/sql-server-on-azure-vms/aoag-azurevm-template.png)

For a step-by-step tutorial please see on how to [Configure Always On availability group in Azure VM automatically - Resource Manager](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups)

# Migrate a SQL Server database to SQL Server in an Azure VM
There are a number of methods for migrating an on-premises SQL Server user database to SQL Server in an Azure VM. 

#### What are options for migrating a Database?

The primary migration methods are:

* Perform on-premises backup using compression and manually copy the backup file into the Azure virtual machine

* Perform a backup to URL and restore into the Azure virtual machine from the URL

* Detach and then copy the data and log files to Azure blob storage and then attach to SQL Server in Azure VM from URL

* Convert on-premises physical machine to Hyper-V VHD, upload to Azure Blob storage, and then deploy as new VM using uploaded VHD

* Ship hard drive using Windows Import/Export Service

* If you have an AlwaysOn deployment on-premises, use the [Add Azure Replica Wizard](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-onprem-availability) to create a replica in Azure and then failover, pointing users to the Azure database instance

* Use SQL Server [transactional replication](https://msdn.microsoft.com/library/ms151176.aspx) to configure the Azure SQL Server instance as a subscriber and then disable replication, pointing users to the Azure database instance

For more information on choosing the right migration method see [Migrate a SQL Server database to SQL Server in an Azure VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

# Security Considerations for SQL Server in Azure Virtual Machines

This topic includes overall security guidelines that help establish secure access to SQL Server instances in an Azure VM. However, in order to ensure better protection to your SQL Server database instances in Azure, we recommend that you implement the traditional on-premises security practices in addition to the security best practices for Azure.

For more information about the SQL Server security practices, see [Security Considerations for SQL Server Installations](https://docs.microsoft.com/en-us/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

Azure complies with several industry regulations and standards that can enable you to build a compliant solution with SQL Server running in a Virtual Machine. For information about regulatory compliance with Azure, see [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).


