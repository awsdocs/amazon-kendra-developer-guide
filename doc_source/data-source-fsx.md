--------

--------

# Using an Amazon FSx data source<a name="data-source-fsx"></a>

Amazon FSx is a fully managed, cloud based file server system that offers shared storage capabilities\. If you are an Amazon FSx user, you can use Amazon Kendra to index your Amazon FSx data source\.

You can connect Amazon Kendra to your Amazon FSx data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [FsxConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_FsxConfiguration.html) API\.

Amazon Kendra currently only supports Amazon FSx for Windows File Server\.

For troubleshooting your Amazon Kendra Amazon FSx data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-fsx)
+ [Prerequisites](#prerequisites-fsx)
+ [Connecting Amazon Kendra to your Amazon FSx data source](#data-source-procedure-fsx)
+ [Learn more](#fsx-learn-more)

## Supported features<a name="supported-features-fsx"></a>
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-fsx"></a>

Before you can use Amazon Kendra to index your Amazon FSx data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your Amazon FSx data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have an Amazon FSx account with read and mounting permissions\.
+ In your Amazon FSx account, you have created authentication credentials for an Active Directory user account that includes your Active Directory user name and your Domain Name System \(DNS\) domain name\. For example, *user@corp\.example\.com*\. You will your username and password to connect Amazon Kendra to Amazon FSx\.
+ You have copied your Amazon FSx file system id\. You will need this to connect your Amazon Kendra index to Amazon FSx\.
+ You must also use an Amazon VPC \(AWS VPC\) where your Amazon FSx resides\.

  You can find more information on how to configure your Amazon FSx account on the [Amazon FSx Developer Guide](https://docs.aws.amazon.com/fsx/index.html) page\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your Amazon FSx data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your Amazon FSx data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your Amazon FSx data source<a name="data-source-procedure-fsx"></a>

To connect Amazon Kendra to your Amazon FSx data source you must provide details of your Amazon FSx credentials so that Amazon Kendra can access your data\. If you have not yet configured Amazon FSx for Amazon Kendra see [Prerequisites](#prerequisites-fsx)\.

### <a name="fsx-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Amazon FSx** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Amazon FSx**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Source**—**Select Amazon FSx for Windows file server**\.

   1. **Amazon FSx file system ID**—Select your file system Id or create a new directory\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Amazon FSx authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Amazon FSx\-’ is automatically added to your secret name\.

         1. For **User name**—Enter the user name for Amazon FSx Active Directory account\.

         1. For **Password**—Enter the password for the Amazon FSx Active Directory account\.

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You must use a VPC with your Amazon FSx data source\.You must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Change log**—Select to update your index instead of syncing all your files\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Amazon FSx Windows field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ FsxConfiguration API ]

**To connect Amazon Kendra to Amazon FSx**

You must specify the following using the [FsxConfiguration ](https://docs.aws.amazon.com/kendra/latest/dg/API_FsxConfiguration.html)API: 
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Amazon FSx account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "username": "user@corp.example.com",
      "password": "password"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for Amazon FSx data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Amazon FSx connector and Amazon Kendra\. For more information, see [IAM roles for Amazon FSx data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—You can choose to specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+  **Change log**—Whether Amazon Kendra should use the Amazon FSx data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Amazon FSx data source than to process the change log\. If you are syncing your Amazon FSx data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—You can specify whether to include or exclude content to be indexed\. You can also specify regular expression patterns to include or exclude types of content\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. To test user context filtering on a user, you must include the DNS domain name as part of the user name when you issue the query\. You must have administrative permissions of the Active Directory domain\. You can also test user context filtering on a group name\. For more information, see [User context filtering for Amazon FSx data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your Amazon FSx data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="fsx-learn-more"></a>

To learn more about integrating Amazon Kendra with your Amazon FSx data source, see:
+ [Securely search unstructured data on Windows file systems with the Amazon Kendra connector for Amazon FSx for Windows File Server](https://aws.amazon.com/blogs/machine-learning/securely-search-unstructured-data-on-windows-file-systems-with-amazon-kendra-connector-for-amazon-fsx-for-windows-file-server/)