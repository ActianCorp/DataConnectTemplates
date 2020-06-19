# Overview

Actian provides Templates for loading data into Avalanche. You can quickly configure these templates for loading data from supported sources by editing the associated macro values. You may also customize the designs to your specifications using DataConnect Studio.
Avalanche Data Loading Templates currently support:

- [Loading Delimited Files from Amazon S3](#Loading-Delimited-Files-from-Amazon-S3)
- [Loading Delimited Files from Azure](#Loading-Delimited-Files-from-Azure)

## Loading Delimited Files from Amazon S3

The Delimited_S3_to_Avalanche_AWS template is used to load delimited files stored in Amazon S3 buckets to a table in an Actian Avalanche data warehouse hosted on the AWS Cloud.\
Using the macros, provide the connection string to your Avalanche data warehouse, credentials for the database and S3 bucket, and whether or not the first row of data contains a header for the column names. The connector used in the templates handles tab, comma, and pipe delimiters by default. If the source file has a different field separator, you can specify the delimiter using a macro.
When you run a configuration with this template, it creates a new table if it does not exist or inserts data to an existing table of the same name if it exists.
Before using the Template to load files from Amazon S3 to Avalanche, you must perform the following:

- Confirm that the Avalanche data warehouse is running on AWS
- Obtain credentials for connecting to the Avalanche database (user name and password)
- If Integration Manager on DataCloud is used:
  > Obtain the ODBC Connection String for your Avalanche data warehouse. You can obtain this information from Avalanche portal.
- If Integration Manager On-premise is used, do one of the following:

  - Create ODBC DSN (as a System DSN) with the ODBC driver shipped with latest client runtime, which can be downloaded from https://esd.actian.com/ (select Product as Actian Avalanche, Release as Client Runtime, and Platform as Windows/Linux).
    Setup ODBC DSN (as a System DSN) pointing to the Avalanche AWS instance.

  - In the connect string, replace the name of the driver based on the operating system:
    > For Windows, Driver=Actian CR\
    >  For Linux, configure a driver entry called Ingres in the odbcinst.ini file (if it is not already present).

- Choose a file in an S3 bucket in the same region as the Avalanche data warehouse
  > Note: The Avalanche instance and S3 buckets must be in the same region. If they are in different regions, the log shows the "Invalid Credentials" error message after process execution.
- Obtain your AWS Access Key and AWS Secret Key for accessing AWS services.

To load delimited data files from Amazon S3 to an Avalanche data warehouse

- Select the Delimited_S3_to_Avalanche_AWS configuration.
- Set the values for the following required macros and run the configuration.
  > Note: You must provide values for these macros so that the Template has the necessary information to access your data files, Avalanche warehouse, and find or create your table.\
  >  You can encrypt sensitive macro values (such as passwords, keys, and so on) from Integration Manager. For information about encrypting, see Enable Macro Encryption.

<table>
<tbody><tr><th >Macro Name</th><th >Description</th></tr><tr><td >$(AVALANCHE_CONNECT_STRING)</td><td >ODBC Connection string for connecting to Avalanche database. You can obtain this information from Avalanche portal.Note:&nbsp;&nbsp;This is required only if you are running Integration Manager on DataCloud.</td></tr><tr><td >$(AVALANCHE_USERNAME)<br>$(AVALANCHE_PASSWORD)</td><td >Credentials used to connect to the database.</td></tr><tr><td >$(AVALANCHE_TABLE)</td><td >Name of the table in Avalanche where the data will be written to.</td></tr><tr><td >$(AWS_ACCESS_KEY)$(AWS_SECRET_KEY)</td><td >Credentials used to access AWS services.</td></tr><tr><td >$(AWS_BUCKET_NAME)</td><td >Name of the AWS storage bucket to pull the data from.</td></tr><tr><td >$(AWS_REGION)</td><td >Region ID of the location that hosts the specific S3 bucket. The supported regions are:<br>US East (N. Virginia)<br>US East (Ohio)<br>US West (Oregon)<br>Europe (Ireland)<br>Europe (London)<br>Europe (Frankfurt).<br>You can specify the region in the above format or in the following format:us-east-1<br> If you do not enter the region value correctly, then the template will fail during execution. Avalanche cluster and the bucket must be in the same region.</td></tr><tr><td >$(HEADER)</td><td >Specifies whether first data row contains column or field names. Used to detect field names for creating a new database table.</td></tr><tr><td >$(S3_FILE_LIST)</td><td>Comma separated list of input files present in the S3 bucket. Files must have the same schema.</td></tr></tbody></table>

> If you want to override any of the default settings, you can add the following macros and set the values. Usually, these are not required unless you have a data file with a typical record or field separators, want to increase the sample size, or want to specify the table operation. These macros are not displayed by default. You can manually add the name and set the value to override the default value.

| Macro Name | Description |
| -----------|------------ |
| $(AVALANCHE_DSN) | Name of the ODBC data source to use for connecting to Avalanche database. Specify this macro if you want to use a pre-configured DSN on your system instead of the connect string.|
|$(FIELD_SEPARATOR)| Delimiter used in the source files to separate the fields.|
|$(RECORD_SEPARATOR) | Delimiter used in the source files to separate the data records.|
|$(QUOTE_CHARACTERS)| Character used to quote fields. For example, double quote ".<br>Use two characters if start and end quote characters are different. For example, [].|
| $(SAMPLE_SIZE) | Number of records that must be sampled for building the source schema.|
| $(OUTPUT_MODE) | Table operations that must be performed before inserting data. The available operations are: <br> - replace: Drops existing table and creates new table <br> - delete_append: Truncates table before inserting. <br> - append: Creates table only if it does not exist and inserts records.|
| $(DEFAULT_TEXT_COL_SIZE) | Set the default size of the text columns in the table. Set it to a reasonable value based on your data to avoid truncations. This value is ignored if the length identified from parsing data is greater than this value. <br> This property is also useful for inserting double-byte characters like Japanese or Chinese. Varchar is used for text data types that supports single byte characters. To support double-byte characters in varchar data type, the size of the column must be doubled using this macro.|

--------------

> **Note:** \
 If you specify one of the first three macros (FIELD_SEPARATOR, RECORD SEPARATOR, or QUOTE CHARACTERS), then you must also specify the other two macros. Else, other delimiters are not auto-identified and use default values. For example, if you specify only QUOTE CHARACTER, then FIELD_SEPARATOR defaults to "," and RECORD_SEPARATOR defaults to "\r\n"(Windows) and "\n" (Linux).

## Loading Delimited Files from Azure

The Delimited_ABFS_to_Avalanche_Azure template is used to load delimited files stored in Azure Storage account to a table in an Actian Avalanche data warehouse.\
Using the macros, set the connection string to your Avalanche data warehouse, credentials for the database and Azure data, and whether or not the first row of data contains a header for the column names. The connector used in the templates handles tab, comma, and pipe delimiters by default. If the source file has a different field separator, you can specify the delimiter using a macro.
When you run a configuration with this template, it creates a new table if it does not exist or inserts data to an existing table of the same name if it exists.
Before using the Template to load files from Amazon S3 to Avalanche, you must perform the following:

- Confirm that the Avalanche data warehouse is running
- Obtain credentials for connecting to the Avalanche database (user name and password)
- If Integration Manager on DataCloud is used:
  > Obtain the ODBC Connection String for your Avalanche data warehouse. You can obtain this information from Avalanche portal.
- If Integration Manager On-premise is used, do one of the following:

  - Create ODBC DSN (as a System DSN) with the ODBC driver shipped with latest client runtime, which can be downloaded from https://esd.actian.com/ (select Product as Actian Avalanche, Release as Client Runtime, and Platform as Windows/Linux).
    Setup ODBC DSN (as a System DSN) pointing to the Avalanche Azure instance

  - In the connect string, replace the name of the driver based on the operating system:
    > For Windows, Driver=Actian CR\
    >  For Linux, configure a driver entry called Ingres in the odbcinst.ini file (if it is not already present).

- Azure Storage account information
- Obtain credentials for accessing Azure services such as Client ID, Client Secret and Directory (tenant) ID.

To load delimited data files from ABFS to an Avalanche database
- Select the Delimited_ABFS_to_Avalanche_Azure configuration.
- Set the values for the following required macros and run the configuration.
  > Note: You must provide values for these macros so that the Template has the necessary information to access your data files, Avalanche warehouse, and find or create your table.\
  >  You can encrypt sensitive macro values (such as passwords, keys, and so on) from Integration Manager. For information about encrypting, see Enable Macro Encryption.

| Macro Name | Description |
| ---------|--------------|
|$(AVALANCHE_CONNECT_STRING)|ODBC Connection string for connecting to Avalanche database. You can obtain this information from the Avalanche portal.<br>**Note:**  This is required only if you are running Integration Manager on DataCloud.|
|$(AVALANCHE_USERNAME), $(AVALANCHE_PASSWORD)|Credentials used to connect to the Avalanche database.|
|$(AVALANCHE_TABLE)|Name of the table in Avalanche, where the data will be written to.|
|$(ABFS_FILE_LIST)|Comma separated list of input files present in an Azure Storage Container.|
|$(HEADER)|Specifies whether first data row contains column/field names. Used to detect field names for creating a new database table.|
|$(AZURE_CLIENT_ID), $(AZURE_CLIENT_SECRET)|Credentials used to access azure services.|
|$(AZURE_TENANT_ID)|Tenant ID (Directory ID) assigned by Azure Active Directory service.|
|$(AZURE_CONTAINER_NAME)|Name of the container in azure storage account which contains data files to pull the data from.|
|$(AZURE_STORAGE_ACCOUNT)| Name of the azure storage account.|

> If you want to override any of the default settings, you can add the following macros and set the values. Usually, these are not required unless you have a data file with a typical record or field separators, want to increase the sample size, or want to specify the table operation. These macros are not displayed by default. You can manually add the name and set the value to override the default value.

| Macro Name | Description |
| -----------|------------ |
| $(AVALANCHE_DSN) | Name of the ODBC data source to use for connecting to Avalanche database. Specify this macro if you want to use a pre-configured DSN on your system instead of the connect string.|
|$(FIELD_SEPARATOR)| Delimiter used in the source files to separate the fields.|
|$(RECORD_SEPARATOR) | Delimiter used in the source files to separate the data records.|
|$(QUOTE_CHARACTERS)| Character used to quote fields. For example, double quote ".<br>Use two characters if start and end quote characters are different. For example, [].|
| $(SAMPLE_SIZE) | Number of records that must be sampled for building the source schema.|
| $(OUTPUT_MODE) | Table operations that must be performed before inserting data. The available operations are: <br> - replace: Drops existing table and creates new table <br> - delete_append: Truncates table before inserting. <br> - append: Creates table only if it does not exist and inserts records.|
| $(DEFAULT_TEXT_COL_SIZE) | Set the default size of the text columns in the table. Set it to a reasonable value based on your data to avoid truncations. This value is ignored if the length identified from parsing data is greater than this value. <br> This property is also useful for inserting double-byte characters like Japanese or Chinese. Varchar is used for text data types that supports single byte characters. To support double-byte characters in varchar data type, the size of the column must be doubled using this macro.|

--------------

> **Note:** \
 If you specify one of the first three macros (FIELD_SEPARATOR, RECORD SEPARATOR, or QUOTE CHARACTERS), then you must also specify the other two macros. Else, other delimiters are not auto-identified and use default values. For example, if you specify only QUOTE CHARACTER, then FIELD_SEPARATOR defaults to "," and RECORD_SEPARATOR defaults to "\r\n"(Windows) and "\n" (Linux).

## Troubleshooting
 If there are any errors during job execution, see [Troubleshooting Template Execution Errors](https://docs.actian.com/integrationmanager/2.0/index.html#page/User%2FTroubleshooting_Template_Configuration_Execution.htm%23) for the troubleshooting information.
