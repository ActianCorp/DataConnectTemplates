# Avalanche Data Loading Templates

## Overview
Actian provides executable templates for loading data into Avalanche. You can quickly configure these templates for loading data into Avalanche from different sources. You may also customize the designs to meet your specifications using DataConnect Studio.
Templates accept input in the form of macros. Macros are divided into required and optional set. You will find the required macros file applicable for a specific template in the Macros folder with the same name as the djar name. If you are configuring templates on integration manager, you don't need the macro file, integration manager automatically detects the required macros.
  
  > You can encrypt sensitive macro values (such as passwords, secret keys, and tokens for token based authentication) from Integration Manager. For information about encrypting, see **Enable Macro Encryption** section in _Integration Manager_ documentation available at [docs.actian.com](http://docs.actian.com/).

When you run the template, it creates a new table if it does not exist or inserts data to an existing table of the same name if it exists. For existing tables, a schema mismatch error may be thrown if the source and target layouts don't match.

Avalanche Data Loading Templates currently support:

- [Loading Delimited Files from Amazon S3]
- [Loading Delimited Files from Azure Blob Storage]
- [Loading Salesforce Data into Avalanche on AWS]
- [Loading Salesforce Data into Avalanche on Azure]

## Prerequisites

- Create and configure Avalanche data warehouse on the platform of your choice. Supported platforms are AWS/Microsoft Azure. 
- Confirm that the Avalanche data warehouse is running on AWS
- Obtain credentials for connecting to the Avalanche database (user name and password)
- If Integration Manager on DataCloud is used:

  - Obtain the ODBC Connection String for your Avalanche data warehouse. You can obtain this information from Avalanche portal.

- If Integration Manager On-premise is used or the templates will be run using Actian DataConnect Engine, do one of the following:

    - Create ODBC DSN (as a System DSN) with the ODBC driver shipped with latest client runtime, which can be downloaded from [https://esd.actian.com/](https://esd.actian.com/) (select Product as Actian Avalanche, Release as Client Runtime, and Platform as Windows/Linux).
    Setup ODBC DSN (as a System DSN) pointing to the Avalanche instance
    - In the connect string, replace the name of the driver based on the operating system:

        > For Windows, Driver name is **Actian CR**\
        For Linux, configure a driver entry called **Ingres** in the odbcinst.ini file (if it is not already present).

## Loading Delimited Files from Amazon S3

The Delimited_S3_to_Avalanche_AWS template is used to load delimited files stored in Amazon S3 buckets to a table in an Actian Avalanche data warehouse hosted on the AWS Cloud.

Using the macros, provide the connection string to your Avalanche data warehouse, credentials for the database and S3 bucket, and whether or not the first row of data contains a header for the column names. The connector used in the templates handles tab, comma, and pipe delimiters by default. If the source file has a different field separator, you can specify your own delimiter using a macro.

To load delimited data files from Amazon S3 to an Avalanche data warehouse using Integration Manager:

- Create a configuration using  **Delimited_S3_to_Avalanche_AWS.x.x.djar** package.

- Set the values for the required macros listed in the following table.

  >Optionally, you may specify advance configuration options. To do so, you can add the macros listed under [Optional Macros for Delimited S3/Azure Templates] section and set their values. Usually, these are not required unless you have a data file with a typical record or field separators, want to increase the sample size, or want to specify the table operation.
- Run the configuration.


| **Macro Name**               | **Description**                                                                                                         |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| \$(AVALANCHE_CONNECT_STRING) | ODBC Connection string for connecting to Avalanche database. You can obtain this information from the Avalanche portal. You can leave this empty if using DSN on prem. |
| $(AVALANCHE\_USERNAME)<br>$(AVALANCHE_PASSWORD) | Credentials used to connect to the database. |
| $(AVALANCHE\_TABLE) | Name of the table in Avalanche where the data will be written to. |
| $(AWS_ACCESS_KEY)<br>$(AWS\_SECRET\_KEY) | Credentials used to access AWS services. |
| $(AWS_BUCKET_NAME) | Name of the AWS storage bucket to pull the data from. |
  | \$(AWS_REGION) | Region ID of the location that hosts the specific S3 bucket. See [Supported AWS Regions] for more information|
  | $(HEADER) | Specifies whether first data row contains column or field names. Used to detect field names for creating a new database table. |
| $(S3_FILE_LIST) | Comma separated list of input files present in the S3 bucket. Files must have the same schema. |

To run the template directly using DataConnect Engine.
- Download **Delimited_S3_to_Avalanche_AWS.x.x.djar** package and corresponding macrodef file (**Delimited_S3_to_Avalanche_AWS.x.x.macrodef.json**) from Macros directory.
- Edit the macrodef file and provide macro values.
- Run the djengine commmand.

  ```
  djengine -l dataloading.log -mf Delimited_S3_to_Avalanche_AWS.x.x.macrodef.json Delimited_S3_to_Avalanche_AWS.x.x.djar
  ```

## Loading Delimited Files from Azure Blob Storage

The Delimited_Azure_Blob_to_Avalanche_Azure template is used to load delimited files stored in Azure Blob Storage account to a table in an Actian Avalanche data warehouse running on Azure.

Using the macros, set the connection string to your Avalanche data warehouse, credentials for the database and Azure container, and whether or not the first row of data contains a header for the column names. The connector used in the templates handles tab, comma, and pipe delimiters by default. If the source file has a different field separator, you can specify your own delimiter using a macro.

To load delimited data files from **Azure Blob Storage** to an Avalanche database using Integration Manager:

- Create a configuration using  **Delimited_Azure_Blob_to_Avalanche_Azure.x.x.djar** package.

- Set the values for the required macros listed in the following table.

  >Optionally, you may specify advance configuration options. To do so, you can add the macros listed under [Optional Macros for Delimited S3/Azure Templates] section and set their values. Usually, these are not required unless you have a data file with a typical record or field separators, want to increase the sample size, or want to specify the table operation.

- Run the configuration.

| **Macro Name**               | **Description**                                                                                                         |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| \$(AVALANCHE_CONNECT_STRING) | ODBC Connection string for connecting to Avalanche database. You can obtain this information from the Avalanche portal. You can leave this empty if using DSN on prem|
  | $(AVALANCHE\_USERNAME), $(AVALANCHE_PASSWORD) | Credentials used to connect to the Avalanche database. |
  | $(AVALANCHE\_TABLE) | Name of the table in Avalanche, where the data will be written to. |
| $(AZURE_FILE_LIST) | Comma separated list of input files present in an Azure Storage Container. |
  | $(HEADER) | Specifies whether first data row contains column/field names. Used to detect field names for creating a new database table. |
| $(AZURE_CLIENT_ID), $(AZURE\_CLIENT\_SECRET) | Credentials used to access azure services. |
| $(AZURE_TENANT_ID) | Tenant ID (Directory ID) assigned by Azure Active Directory service. |
  | $(AZURE\_CONTAINER\_NAME) | Name of the container in azure storage account which contains data files to pull the data from. |
| $(AZURE_STORAGE_ACCOUNT) | Name of the azure storage account. |


To run the template directly using DataConnect Engine.
- Download **Delimited_Azure_Blob_to_Avalanche_Azure.x.x.djar** package and corresponding macrodef file (**Delimited_Azure_Blob_to_Avalanche_Azure.x.x.macrodef.json**) from Macros directory.
- Edit the macrodef file and provide macro values.
- Run the djengine commmand.

  ```
  djengine -l dataloading.lof -mf Delimited_Azure_Blob_to_Avalanche_Azure.x.x.macrodef.json Delimited_Azure_Blob_to_Avalanche_Azure.x.x.djar
  ```

## Optional Macros for Delimited S3/Azure Templates

| **Macro Name**                     | **Description**                                                                                                                                                                    |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \$(AVALANCHE_DSN)                  | Name of the ODBC data source to use for connecting to Avalanche database. Specify this macro if you want to use a pre-configured DSN on your system instead of the connect string. |
| \$(AVALANCHE_CREATE_TABLE_QUERY)   | Create table statement to use for creating the table. Make sure partitioning is specified. Table name in the query must match the AVALANCHE_TABLE macro value.                     |
| \$(AVALANCHE_CREATE_TABLE_OPTIONS) | Use this option when you do not want to build the complete query but only want to specify options to pass to &quot;with&quot; clause of create table query. Make sure partitioning is specified. Also, this macro is ignored if AVALANCHE_CREATE_TABLE_QUERY macro is defined.
  | $(FIELD\_SEPARATOR) | Delimiter used in the source files to separate the fields. |
| $(RECORD_SEPARATOR) | Delimiter used in the source files to separate the data records. |
  | $(QUOTE\_CHARACTERS) | Character used to quote fields. For example, double quote &quot;. Use two characters if start and end quote characters are different. For example, []. |
| $(SAMPLE_SIZE) | Number of records that must be sampled for building the source schema. |
  | \$(OUTPUT_MODE) | Table operations that must be performed before inserting data. The available operations are:<br>- replace: Drops existing table and creates new table<br>- delete_append: Truncates table before inserting.<br>- append: Creates table only if it does not exist and inserts records.<br>Default is append. |
  | $(DEFAULT\_TEXT\_COL\_SIZE) | Set the default size of the text columns in the table. Set it to a reasonable value based on your data to avoid truncations. This property is also useful for inserting double-byte characters like Japanese or Chinese. Varchar is used for text data types that supports single byte characters. To support double-byte characters in varchar data type, the size of the column must be doubled using this macro. |
| $(UNICODE_CHARS) | Indicates whether the data contains Unicode characters. If set to **True** , nvarchar data type is used for text columns. |
  | \$(VW_XXX) | Specify VWLOAD options as a macro in the VW_XXX format. XXX can be any of the properties listed in the [COPY VWLOAD] section in the _Avalanche_ documentation. One macro can be added for each property. For properties such as STRICTNULLS that does not accept a value, the macro value must be the name of the property itself.<br>  For example:<br><pre>VW_NULLS = NULL<br>VW_STRICTNULLS = STRICTNULLS<br></pre><br>**Note:** FDELIM, RDELIM, QUOTE, AZURE/AWS credentials must be specified using specific macros for these properties.|
  | \$(SOURCE_FETCH_SIZE) | Size of the data (in bytes) to fetch from the source file in the s3 bucket. Default is 15000000 (15MB). |
| \$(AVALANCHE_DBADMIN_GROUP_ACCESS) | Assign table access to for the dbadmingrp group. Only applicable when new table is created. Default is True. |

>**NOTE:** If you specify one of the three macros (FIELD_SEPARATOR, RECORD SEPARATOR, or QUOTE CHARACTERS), then you must also specify the other two macros. Else, other delimiters are not auto-identified and use default values. For example, if you specify only QUOTE CHARACTER, then FIELD_SEPARATOR defaults to &quot;,&quot; and RECORD_SEPARATOR defaults to &quot;\r\n&quot;(Windows) and &quot;\n&quot;(Linux).

## Loading Salesforce Data into Avalanche on AWS

The Salesforce_to_Avalanche_AWS template is used to load data from Salesforce tables into a table in Actian Avalanche data warehouse running on AWS platform.

Using macros, provide the following:

- Salesforce connection information
- Connection string to your Avalanche data warehouse
- Credentials for the database and S3 bucket

To load Salesforce data into an Avalanche data warehouse using Integration Manager:

- Create a configuration usig **Salesforce_to_Avalanche_AWS.x.x.djar** package.
- Set the values for the required macros listed under [Required Macros for Salesforce Templates] section.
- Configure [AWS S3 Macros]. These macros are required as the template temporarily stages data on aws s3 buckets for faster data loading using [COPY VWLOAD] functionality of Avalanche.

  > Optionally, you may specify advance configuration options. you can add the optional macros defined under [Optional Macros for Salesforce Templates] section and set their values.
- Run the configuration.

To run the template directly using DataConnect Engine.
- Download **Salesforce_to_Avalanche_AWS.x.x.djar** package and corresponding macrodef file (**Salesforce_to_Avalanche_AWS.x.x.macrodef.json**) from Macros directory.
- Edit the macrodef file and provide macro values.
- Run the djengine commmand.

  ```
  djengine -l dataloading.log -mf Salesforce_to_Avalanche_AWS.x.x.macrodef.json Salesforce_to_Avalanche_AWS.x.x.djar
  ```

## Loading Salesforce Data into Avalanche on Azure

The _Salesforce_to_Avalanche_Azure_ template is used to load Salesforce data stored in Azure Storage account to a table in an Actian Avalanche data warehouse running on Azure.

Using the macros, provide the following:

- Salesforce connection information
- Connection string to your Avalanche data warehouse
- Credentials for the database and Azure container

To load data from Salesforce to an Avalanche database using Integration Manager:

- Create a configuration using **Salesforce_to_Avalanche_Azure.x.x.djar** package.
- Set the values for the required macros listed under [Required Macros for Salesforce Templates] section.
- Configure [Azure Storage Macros]. These are required as the template temporarily stages data on azure blob storage for faster data loading using COPY VWLOAD functionality of Avalanche.

  > Optionally, you may specify advance configuration options. you can add the optional macros defined under [Optional Macros for Salesforce Templates] section and set their values.
- Run the configuration.

To run the template directly using DataConnect Engine.
- Download **Salesforce_to_Avalanche_Azure.x.x.djar** package and corresponding macrodef file (**Salesforce_to_Avalanche_Azure.x.x.macrodef.json**) from Macros directory.
- Edit the macrodef file and provide macro values.
- Run the djengine commmand.

  ```
  djengine -l dataloading.log -mf Salesforce_to_Avalanche_Azure.x.x.macrodef.json Salesforce_to_Avalanche_Azure.x.x.djar
  ```

## Required Macros for Salesforce Templates

| **Macro Name**               | **Description**                                                                                                         |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| \$(AVALANCHE_CONNECT_STRING) | ODBC Connection string for connecting to Avalanche database. You can obtain this information from the Avalanche portal. You can skip this if using a DSN on-prem.|
  | $(AVALANCHE\_USERNAME), $(AVALANCHE_PASSWORD) | Credentials used to connect to the Avalanche database. |
  | $(AVALANCHE\_TABLE) | Name of the table in Avalanche, where the data will be written to. |
| $(SALESFORCE_USERNAME)<br>$(SALESFORCE\_PASSWORD) | Credentials for connecting to Salesforce. |
| $(SALESFORCE_TABLE) | Name of the table or entity in Salesforce. |
  | $(SALESFORCE\_SANDBOX\_MODE) | If set to **True** , connects to the Salesforce application in the sandbox environment. |
| $(SALESFORCE_QUERY) | Salesforce SOQL query for fetching data. Value can be the query statement itself or a path to the query file. In case of path, prefix the value with file:///.|

> **Note:** Either SALESFORCE_TABLE or SALESFORCE_QUERY macro must be specified. Query takes precedence over table.


## Optional Macros for Salesforce Templates

| **Macro Name**                     | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \$(SALESFORCE_API_VERSION)         | Salesforce API version. The default version is 42.0.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| \$(SALESFORCE_QUERY_ALL)           | If set to **True** , fetches deleted or archived records.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| \$(AVALANCHE_DSN)                  | Name of the ODBC data source for connecting to Avalanche database. Specify this macro if you want to use a pre-configured DSN on your system instead of the connect string.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| \$(AVALANCHE_CREATE_TABLE_QUERY)   | Create table statement to use for creating the table. Make sure partitioning is specified. Table name in the query must match the AVALANCHE_TABLE macro value.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| \$(AVALANCHE_CREATE_TABLE_OPTIONS) | Use this option when you do not want to build the complete query but only want to specify options to pass to "with" clause of create table query. Make sure partitioning is specified. Also, this macro is ignored if AVALANCHE_CREATE_TABLE_QUERY macro is defined.                                                                                                                                                                                                                                                                                                                                     |
| \$(OUTPUT_MODE)                    | Table operations that must be performed before inserting data. The available operations are:<br> - replace: Drops existing table and creates new table <br> - delete_append: Truncates table before inserting.<br> - append: Creates table only if it does not exist and inserts records. By default, the value is **append**.                                                                                                                                                                                                                                                                           |
| \$(DEFAULT_TEXT_COL_SIZE)          | Set the default size of the text columns in the table. Set it to a reasonable value based on your data to avoid truncations. This property is also useful for inserting double-byte characters like Japanese or Chinese. Varchar is used for text data types that supports single byte characters. To support double-byte characters in varchar data type, the size of the column must be doubled using this macro.                                                                                                                                                                                      |
| \$(UNICODE_CHARS)                  | Indicates whether the data contains Unicode characters. If set to **True** , nvarchar data type is used for text columns.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| \$(VW_XXX)                         | Specify VWLOAD options as a macro in the VW_XXX format. XXX can be any of the properties listed in the [COPY VWLOAD](https://docs.actian.com/avalanche/index.html#page/SQLLanguage%2FCOPY_VWLOAD.htm%23ww421843) section in the _Avalanche_ documentation. One macro can be added for each property. For properties such as STRICTNULLS that does not accept a value, the macro value must be the name of the property itself.<br> FDELIM, RDELIM, QUOTE, AZURE/AWS credentials must be specified using specific macros for these properties.<br>For example:VW_NULLS = NULLVW_STRICTNULLS = STRICTNULLS |
| \$(BATCH_SIZE)                     | Size of the chunk (in terms of number of records), the source is split into. The default value is 50000.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| \$(COPYVW_PARALLEL_LOAD_SIZE)      | Number of chunks to load in parallel using COPY VWLOAD. The default value is 20.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| \$(AVALANCHE_DBADMIN_GROUP_ACCESS) | Assign table access to for the dbadmingrp group. Only applicable when new table is created. Default is True. |

## AWS S3 Macros

| **Macro Name**                       | **Description**                                                                         |
| ------------------------------------ | --------------------------------------------------------------------------------------- |
| $(AWS\_ACCESS\_KEY)<br>$(AWS_SECRET_KEY) | Credentials for accessing AWS services.                                                 |
| \$(AWS_BUCKET_NAME)                  | Name of the AWS storage bucket to pull the data from.                                   |
| \$(AWS_REGION)                       | Region ID of the location that hosts the specific S3 bucket. See [Supported AWS Regions] for more information. |

## Azure Storage Macros

| **Macro Name**                               | **Description**                                                                                 |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| $(AZURE\_CLIENT\_ID), $(AZURE_CLIENT_SECRET) | Credentials used to access azure services.                                                      |
| \$(AZURE_TENANT_ID)                          | Tenant ID (Directory ID) assigned by Azure Active Directory service.                            |
| \$(AZURE_CONTAINER_NAME)                     | Name of the container in azure storage account which contains data files to pull the data from. |
| \$(AZURE_STORAGE_ACCOUNT)                    | Name of the azure storage account.                                                              |

## Supported AWS Regions
The supported regions are:
|Region Name | Region ID |
|-------|------|
|US East (N. Virginia)|us-east-1|
|US East (Ohio) | us-east-2|
|US West (Oregon)|us-west-2|
|Europe (Ireland)|eu-west-1|
|Europe (London)|eu-west-2|
|Europe (Frankfurt)|eu-central-1|
> Region information is case and format sensitive. If you do not enter the region value correctly, then the template will fail during execution.\
Also note that the Avalanche cluster and the bucket must be in the same region.

## Troubleshooting
If there are any errors during job execution, see [Troubleshooting Template Execution Errors](https://docs.actian.com/integrationmanager/2.0/index.html#page/User%2FTroubleshooting_Template_Configuration_Execution.htm%23) for the troubleshooting information.

[COPY VWLOAD]: https://docs.actian.com/avalanche/index.html#page/SQLLanguage%2FCOPY_VWLOAD.htm%23ww421843
[Azure Storage Macros]: #azure-storage-macros
[AWS S3 Macros]: #aws-s3-macros
[Required Macros for Salesforce Templates]: #required-macros-for-salesforce-templates
[Loading Delimited Files from Amazon S3]: #loading-delimited-files-from-amazon-s3
[Loading Delimited Files from Azure Blob Storage]: #loading-delimited-files-from-azure-blob-storage
[Loading Salesforce Data into Avalanche on AWS]: #loading-salesforce-data-into-avalanche-on-aws
[Loading Salesforce Data into Avalanche on Azure]: #loading-salesforce-data-into-avalanche-on-azure
[Optional Macros for Delimited S3/Azure Templates]:#optional-macros-for-delimited-s3azure-templates
[Optional Macros for Salesforce Templates]: #optional-macros-for-salesforce-templates
[Supported AWS Regions]: #Supported-AWS-Regions