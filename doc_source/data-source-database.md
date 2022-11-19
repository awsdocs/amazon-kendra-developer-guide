--------

--------

# Using an Amazon Kendra database data source<a name="data-source-database"></a>

You can index documents that are stored in a database using a database data source\. After you provided connection information for the database, Amazon Kendra connects and indexes documents\.

Amazon Kendra supports the following databases:
+ Amazon Aurora MySQL
+ Amazon Aurora PostgreSQL
+ Amazon RDS for MySQL
+ Amazon RDS for PostgreSQL

**Note**  
Serverless Aurora databases are not supported\.

You can connect Amazon Kendra to your database data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [DatabaseConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/DatabaseTemplateConfiguration.html) API\.

For troubleshooting your Amazon Kendra database data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-database)
+ [Prerequisites](#prerequisites-database)
+ [Connecting Amazon Kendra to your database data source](#data-source-procedure-database)

## Supported features<a name="supported-features-database"></a>
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-database"></a>

Before you can use Amazon Kendra to index your database data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your database data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have created custom index fields for the datasource data in your index\. For more information on how to create an Amazon Kendra index, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+ You have copied the authentication credentials for your data source\. The credentials should be a user/password pair\. You need these to connect Amazon Kendra to your data source\.
+ You have copied the host name, port number, host address, and name of the data table that contains the database data\. For PostgreSQL, the data table must be a public table\. The host and port tell Amazon Kendra where to find the database server on the internet\. The database name and table name tell Amazon Kendra where to find the document data on the database server\.
+ You have copied the names of the columns in the data table that contain the document data and document ID, one to five columns to detect if a document has changed, and optional data table columns that map to custom index fields\. You can map any of the Amazon Kendra reserved field names to a table column\.
+ You have copied the database engine type information such as whether you use Amazon RDS for MySQL or another type\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your database data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.

## Connecting Amazon Kendra to your database data source<a name="data-source-procedure-database"></a>

To connect Amazon Kendra to your database data source you must provide details of your database credentials so that Amazon Kendra can access your data\. If you have not yet configured database for Amazon Kendra see [Prerequisites](#prerequisites-database)\.

### <a name="database-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to a database** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **database**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Endpoint**—A DNS host name, an IPv4 address, or an IPv6 address\.

   1. **Port**—A port number\.

   1. **Database**—Database name\.

   1. **Table name**—Table name\.

   1. For **Type of authentication**, choose between **Existing** and **New** to store your database authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. 

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

        1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-database\-’ is automatically added to your secret name\.

        1. For **User name** and **Password**—Enter the authentication credential values you generated and downloaded from your database account\.

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

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Amazon Kendra default field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. You must add the **Database column** values for `document_id` and `document_body` 

   1.  **Custom field mappings**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ DatabaseConfiguration API ]

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
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your database account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

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
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for database data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the database connector and Amazon Kendra\. For more information, see [IAM roles for database data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—You can choose to specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
**Note**  
You must only use a private subnet\. If your RDS instance is in a public subnet in your VPC, you can create a private subnet that has outbound access to a NAT gateway in the public subnet\. The subnets provided in the VPC configuration must be in either US West \(Oregon\), US East \(N\. Virginia\), EU \(Ireland\)\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for database data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your database data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------