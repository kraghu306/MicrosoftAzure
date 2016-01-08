HDInsight Cluster Setup and Walkthrough
===========================================

The Microsoft Azure portal is a central place where you can provision and manage your Azure resources. Azure Portal is one of the tools you can use to create either Linux-based or Windows-based Hadoop cluster in HDInsight.

In this detailed **lab**, we'll follow the process of **create either Linux-based or Windows-based Hadoop cluster in HDInsight**.

Prerequisites
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   **Client computer with Internet connectivity.**
-   **Microsoft Account / Live Id**
-   **Microsoft Azure Subscription**

Objectives
----------

To create a credit risk
assessment solution, we'll follow these steps through a series of tasks:

-   Creating HDInsight Cluster using Azure portal

-   Use Hive with HDInsight to analyze logs from websites
<!-- -->

Estimated time to complete this lab: **1-2 Hours**

###Task 1: Creating HDInsight Cluster

1.  Launch an **In-Private Browser Window** and navigate to
    <https://portal.azure.com> . The following page should load.

2.  2.	Click **NEW**, Click **Data Analytics**, and then click **HDInsight**.

    ![](media/hdinsight-cluster-setup/image1.png)

3.  Type or select the following values:

	1.  **Cluster Name**: Enter a name for the cluster. A green check 
		will appear beside the cluster name if the name is available.
    2.	**Cluster Type**: Select Hadoop. Other options inclue HBase, Storm, and Spark.
	3.	**Cluster Operating System**: Select Windows. To create a Linux-base cluster, 
		select Linux. For our demo, let’s use Windows based Cluster 
	4.	**Version**: See [HDInsight versions](https://azure.microsoft.com/en-in/documentation/articles/hdinsight-component-versioning/). 
	5.	**Subscription**: Select the Azure subscription that will be used for creating this cluster.
	6.	**Resource Group**: Select an existing or create a new resource group
    7.	**Credentials**: Configure the username and the password for the Hadoop user (HTTP user). 
		If you enable remote desktop for the cluster, you will need to configure the remote desktop 
		user username and password, and an account expiration date. Click Select at the bottom to save the changes.
		
	![](media/hdinsight-cluster-setup/image2.png)

	8.  **Data Source**: Create a new or select an existing Azure Storage account to be used 
		as the default file system for the cluster.

    ![](media/hdinsight-cluster-setup/image3.png)
	
	8.  **Selection Method**: Set this to **from all subscriptions** to enable browsing 
		of storage accounts from all your subscriptions. Set this to **Access Key** if you 
		want to enter the **Storage Name** and **Access Key** of an existing storage account.
	9.	**Select storage account/Create New**: Click Select storage account to browse and 
		select an existing storage account you want to associate with the cluster. Or, 
		click Create New to create a new storage account. 
	10.	**Choose Default Container**: Use this to enter the name of the default container to use for the cluster. 
		While you can enter any name here, we recommend using the same name as the cluster so that you can easily 
		recognize that the container is used for this specific cluster.
	11.	**Location**: The geographic region that the storage account is in, or will be created in. 
		This location will determine the cluster location. The cluster and its default storage account must 
		co-locate in the same Azure data center.
	12.	**Node Pricing Tiers**: Set the number of worker nodes that you need for the cluster. 
		The estimated cost of the cluster will be shown within the blade.

	![](media/hdinsight-cluster-setup/image4.png)
	
	13.	**Optional Configuration** to select the cluster version, as well as configure other optional 
		settings such as joining a **Virtual Network**, setting up an **External Metastore** to hold data for Hive and Oozie, 
		use Script Actions to customize a cluster to install custom components, or use additional storage accounts with the cluster.
	14.	**HDInsight Version**: Select the version you want to use for the cluster. For more information, see HDInsight cluster versions.
	15.	**Virtual Network**: Select an Azure virtual network and the subnet if you want to place the cluster into a virtual network.

	![](media/hdinsight-cluster-setup/image5.png)

	##### ***NOTE:***

> *Windows based HDInsight cluster can only be placed into a classical virtual network.*

	16.	**External Metastores**: Specify an Azure SQL database to store Hive and Oozie metadata associated with the cluster.

	##### ***NOTE:***

> *Metastore configuration is not available for HBase cluster types.*
	
	![](media/hdinsight-cluster-setup/image6.png)

	For **Use an existing SQL DB for Hive** metadata, click **Yes**, select a SQL database, and then provide the username/password for the database. 
	Repeat these steps if you want to **Use an existing SQL DB for Oozie** metadata. Click **Select** till you are back on the **Optional Configuration** blade.

	##### ***NOTE:***

> *The Azure SQL database used for the metastore must allow connectivity to other Azure services, 
> including Azure HDInsight. On the Azure SQL database dashboard, on the right side, click the server name. 
> This is the server on which the SQL database instance is running. Once you are on the server view, 
> click **Configure**, and then for **Azure Services**, click **Yes**, and then click **Save**.*	
	
	17.	**Script Actions** if you want to use a custom script to customize a cluster, as the cluster is being created. 
		For more information about script actions, see [Customize HDInsight clusters using Script Action] (https://azure.microsoft.com/en-in/documentation/articles/hdinsight-hadoop-customize-cluster/). 
		On the Script Actions blade provide the details as shown in the screen capture.
	
	![](media/hdinsight-cluster-setup/image7.png)
	
	18.	**Azure Storage Keys**: Specify additional storage accounts to associate with the cluster. 
		In the Azure Storage Keys blade, click Add a storage key, and then select an existing storage account or create a new account.
	
	![](media/hdinsight-cluster-setup/image8.png)
	
4.  Click **Create**. Selecting **Pin to Startboard** will add a tile for cluster to the Startboard of your Portal. The icon will indicate that the cluster is being created, and will change to display the HDInsight icon once creation has completed.

It will take some time for the cluster to be created, usually around 15 minutes. Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the provisioning process.

5.  Once the creation completes, click the tile for the cluster from the Startboard to launch the cluster blade. The cluster blade provides essential information about the cluster such as the name, the resource group it belongs to, the location, the operating system, URL for the cluster dashboard, etc.

	![](media/hdinsight-cluster-setup/image9.png)

Use the following to understand the icons at the top of this blade, and in the **Essentials** section:
	1.	**Settings** and **All Settings**: Displays the **Settings** blade for the cluster, which allows you to access detailed configuration information for the cluster.
	
	2.	**Dashboard, Cluster Dashboard, and URL**: These are all ways to access the cluster dashboard, which is a Web portal to run jobs on the cluster.
	
	3.	**Remote Desktop**: Enables you to enable/disable remote desktop on the cluster nodes.

### 

### Task 	2: Use Hive with HDInsight to analyze logs from websites

Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.

In this demo, we will use an existing HDInsight cluster (created above) to analyze website log files to get insight into the frequency of visits to the website from external websites in a day. We will also show a summary of website errors that the users experience. You will demonstrate how to:
-	Connect to Azure Blob storage, which contains website log files.
-	Create HIVE tables to query those logs.
-	Create HIVE queries to analyze the data.
-	Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data

Prerequisites
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   You must have provisioned a Hadoop cluster on Azure HDInsight. For instructions, see [Provision HDInsight Clusters] 
	(https://azure.microsoft.com/en-in/documentation/articles/hdinsight-provision-clusters/).
-	You must have Microsoft Excel 2013 or Excel 2010 installed.
-	You must have [Microsoft Hive ODBC Driver] (https://www.microsoft.com/en-us/download/details.aspx?id=40886) to import data from Hive into Excel.

To run the sample:

1.  From the [Azure Portal](https://portal.azure.com), from the Startboard (if you pinned the cluster there), 
	click the cluster tile on which you want to run the sample.
    
2.	From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, 
	and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**. 
	Alternatively, you can directly open the dashboard by using the following URL:
	
	**https://<clustername>.azurehdinsight.net**
	
When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.	
	
3.	From the web page that opens, click the **Getting Started Gallery** tab, 
	and then under the **Samples** category, click the **Website Log Analysis** sample.
	
4. Follow the instructions provided on the web page to finish the sample.
	------

##Summary

In this lab you learned how to create either Linux-based or Windows-based Hadoop cluster in HDInsight.


