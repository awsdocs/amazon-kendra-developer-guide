--------

--------

# Amazon RDS/Aurora<a name="data-source-database"></a>

You can index documents that are stored in a database using a database data source\. After you provided connection information for the database, Amazon Kendra connects and indexes documents\.

Amazon Kendra supports the following databases:
+ Amazon Aurora MySQL
+ Amazon Aurora PostgreSQL
+ Amazon RDS for MySQL
+ Amazon RDS for PostgreSQL

**Note**  
Serverless Aurora databases are not supported\.

You can connect Amazon Kendra to your database data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [DatabaseConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_DatabaseConfiguration.html) API\.

For troubleshooting your Amazon Kendra database data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-database)
+ [Prerequisites](#prerequisites-database)
+ [Connection instructions](#data-source-procedure-database)

## Supported features<a name="supported-features-database"></a>

Amazon Kendra database data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-database"></a>

Before you can use Amazon Kendra to index your database data source, make these changes in your database and AWS accounts\.

**In your database, make sure you have:**
+ Noted your user\-password pair as basic authentication credentials for your data source\.
+ Copied the host name, port number, host address, and the name of the data table that contains the database data\. For PostgreSQL, the data table must be a public table\.
**Note**  
The host and port tell Amazon Kendra where to find the database server on the internet\. The database name and table name tell Amazon Kendra where to find the document data on the database server\.
+ Copied the names of the columns in the data table that contain the document data, the document ID, one to five columns to detect if a document has changed, and optional data table columns that map to custom index fields\. You can map any of the Amazon Kendra reserved field names to a table column\.
+ Copied the database engine type information such as whether you use Amazon RDS for MySQL or another type\.
+ Checked each document is unique in database and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your database authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your database data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-database"></a>

To connect Amazon Kendra to your database data source, you must provide the necessary details of your database data source so that Amazon Kendra can access your data\. If you have not yet configured database for Amazon Kendra see [Prerequisites](#prerequisites-database)\.

### <a name="database-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to a database** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **database connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Endpoint**—A DNS host name, an IPv4 address, or an IPv6 address\.

   1. **Port**—A port number\.

   1. **Database**—Database name\.

   1. **Table name**—Table name\.

   1. For **Type of authentication**, choose between **Existing** and **New** to store your database authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. 

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

        1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-database\-’ is automatically added to your secret name\.

        1. For **User name** and **Password**—Enter the authentication credential values from your database account\.

        1. Choose **Save authentication**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.
**Note**  
You must use a private subnet\. If your RDS instance is in a public subnet in your VPC, you can create a private subnet that has outbound access to a NAT gateway in the public subnet\. The subnets provided in the VPC configuration must be in either US West \(Oregon\), US East \(N\. Virginia\), EU \(Ireland\)\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. Select between **Aurora MySQL**, **MySQL**, **Aurora PostgreSQL**, and **PostgreSQL** based on your use case\.

   1. **Enclose SQL identifiers with double quotes**—Select to enclose SQL identifiers in double quotes\. For example, “columnName”\.

   1. **ACL column** and **Change detecting columns**—Use to configure the columns that Amazon Kendra uses for change detection and access control lists\.

   1. In **Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Amazon Kendra default field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. You must add the **Database column** values for `document_id` and `document_body` 

   1.  **Custom field mappings**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to a database**

You must specify the following the [DatabaseConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/databaseConfiguration.html) API:
+ **ColumnConfiguration**—Information about where the index should get the document information from the database\. For more details, see [ColumnConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ColumnConfiguration.html)\. You must specify the `DocumentDataColumnName` and `DocumentIdColumnName` fields\. The column mapped to the `DocumentIdColumnName` field must be an integer column\. The following example shows a simple column configuration for a database data source: 

  ```
  "ColumnConfiguration": {
      "ChangeDetectingColumns": [
          "LastUpdateDate",
          "LastUpdateTime"
      ],
      "DocumentDataColumnName": "TextColumn",
      "DocumentIdColumnName": "IdentifierColumn",
      "DocoumentTitleColumnName": "TitleColumn",
      "FieldMappings": [
          {
              "DataSourceFieldName": "AbstractColumn",
              "IndexFieldName": "Abstract"
          }
      ]
  }
  ```
+ **ConnectionConfiguration**—The type of database engine that runs the database\. The `DatabaseHost` field must be the Amazon Relational Database Service \(Amazon RDS\) instance endpoint for the database\. Don't use the cluster endpoint\.
+ **DatabaseEngineType**—Configuration information that's required to connect to a database\. For more details, see [ConnectionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConnectionConfiguration.html)\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your database account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```

  The secret can contain more information\. The following example shows a database configuration\.

  ```
  "DatabaseConfiguration": {
  "ConnectionConfiguration": {
  "DatabaseHost": "host.subdomain.domain.tld",
          "DatabaseName": "DocumentDatabase",
          "DatabasePort": 3306,
          "SecretArn": "arn:aws:secretmanager:region:account ID:secret/secret name",
          "TableName": "DocumentTable"
      }
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the database connector and Amazon Kendra\. For more information, see [IAM roles for database data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+ **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` as part of the data source configuration\. See [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.
**Note**  
You must only use a private subnet\. If your RDS instance is in a public subnet in your VPC, you can create a private subnet that has outbound access to a NAT gateway in the public subnet\. The subnets provided in the VPC configuration must be in either US West \(Oregon\), US East \(N\. Virginia\), EU \(Ireland\)\.
+  **Field mappings**—Choose to map your database data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for database data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------