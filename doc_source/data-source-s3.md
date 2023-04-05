--------

--------

# Amazon S3<a name="data-source-s3"></a>

Amazon S3 is an object storage service that stores data as objects within buckets\. You can use Amazon Kendra to index your Amazon S3 bucket repository of documents\.

**Warning**  
Amazon Kendra doesn't use a bucket policy that grants permissions to an Amazon Kendra principal to interact with an S3 bucket\. Instead, it uses IAM roles\. Make sure that Amazon Kendra isn't included as a trusted member in your bucket policy to avoid any data security issues in accidentally granting permissions to arbitrary principals\. However, you can add a bucket policy to use an Amazon S3 bucket across different accounts\. For more information, see [Policies to use Amazon S3 across accounts](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3-cross-accounts) \(within the S3 IAM roles tab, under **IAM roles for data sources**\)\. For information about IAM roles for S3 data sources, see [IAM roles](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3)\.

To connect to Amazon S3, you specify the connection and other information in the console, by using [S3DataSourceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_S3DataSourceConfiguration.html) or by using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html)\. If you use the TemplateConfiguration object, you can use a VPC to connect to your data source\. You specify VpcConfiguration when you call CreateDataSource\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.

**Note**  
 `S3DataSourceConfiguration` API doesn't support configuring a VPC\. Only `TemplateConfiguration` API and the console support VPC configuration\.

For troubleshooting your Amazon Kendra S3 data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-s3)
+ [Prerequisites](#prerequisites-s3)
+ [Connection instructions](#data-source-procedure-s3)
+ [Creating an Amazon S3 data source](create-ds-s3.md)
+ [Amazon S3 document metadata](s3-metadata.md)
+ [Access control for Amazon S3 data sources](s3-acl.md)

## Supported features<a name="supported-features-s3"></a>

**S3Configuration API**
+ Field mappings
+ User context filtering
+ Inclusion/exclusion patterns

**Console/TemplateConfiguration API**
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)
+ Sync all documents/Sync only new, modified, or deleted documents

## Prerequisites<a name="prerequisites-s3"></a>

Before you can use Amazon Kendra to index your S3 data source, make these changes in your S3 and AWS accounts\.

**In S3, make sure you have:**
+ Copied the name of your Amazon S3 bucket name\.
**Note**  
Your bucket must be in the same region as your Amazon Kendra index and your index must have permission to access the bucket that contains your documents\.
+ Checked each document is unique in S3 and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.

If you don’t have an existing IAM role, you can use the console to create a new IAM role when you connect your S3 data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and an index ID\.

## Connection instructions<a name="data-source-procedure-s3"></a>

To connect Amazon Kendra to your S3 data source, you must provide the necessary details of your S3 data source so that Amazon Kendra can access your data\. If you have not yet configured S3 for Amazon Kendra see [Prerequisites](#prerequisites-s3)\.

### <a name="s3-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Amazon S3 ** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **S3 connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following optional information:

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. In **Sync scope**, for **Data source location**—The path to the Amazon S3 bucket where your data is stored\. Select **Browse S3** to choose your bucket\.

   1. \(Optional\) **Metadata files prefix folder location**—The path to the folder in which your metadata is stored\. Select **Browse S3** to locate your metadata folder\.

   1. \(Optional\) **Access control list configuration file location**—The path to the location of a file containing a JSON structure that specifies access settings for the files stored in your S3 data source\. Select **Browse S3** to locate your ACL file\.

   1. \(Optional\) **Select decryption key**—Select to use a decryption key\. You can choose to use an existing AWS KMS key or create a new one\.

   1. \(Optional\) In **Additional configuration**, for **Regex patterns**—Add regular expression patterns to include or exclude documents from your index\. All paths are relative to the data source location S3 bucket\. You can add up to 100 patterns\. 

   1. In **Sync mode**, choose between **Full sync mode** and **New, modified, or deleted content sync** to determine how your index updates when your data source content changes\. When you sync your data source with Amazon Kendra for the first time, all content is synced by default\.

   1. In **Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following optional information:

   1. **S3 field mapping**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—Choose to add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ TemplateConfiguration API ]

**To connect Amazon Kendra to Amazon S3**

You must specify a JSON of the [data source schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\. You must provide the following information:
+ **BucketName**—The name of the bucket that contains the documents\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the S3 connector and Amazon Kendra\. For more information, see [IAM roles for S3 data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—Specify whether to include or exclude certain file names, file types, file paths, and use glob patterns \(patterns that can expand a wildcard pattern into a list of path names that match the given pattern\)\. Examples of glob patterns include:
  + `/myapp/config/*`—All files inside config directory
  + `/**/*.png`—All \.png files in all directories
  + `/**/*.{png,ico,md}`—All \.png, \.ico or \.md files in all directories
  + `/myapp/src/**/*.ts`—All \.ts files inside src directory \(and all its subdirectories\)
  + `**/!(*.module).ts`—All \.ts files but not \.module\.ts
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your S3 data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+ **Document metadata configuration**—Add document metadata files that contain information such as the document access control information, source URI, document author, and custom attributes\. Each metadata file contains metadata about a single document\.

For a list of other important JSON keys to configure, see [Amazon S3 template schema](ds-schemas.md#ds-s3-schema)\.

------
#### [ S3DataSourceConfiguration API ]

**To connect Amazon Kendra to Amazon S3**

You must specify the following using the [S3DataSourceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_S3DataSourceConfiguration.html) API:
+  **BucketName**—The name of the bucket that contains the documents\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the S3 connector and Amazon Kendra\. For more information, see [IAM roles for S3 data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—Specify whether to include or exclude certain content using prefixes, file name, file type, file path, and glob patterns \(patterns that can expand a wildcard pattern into a list of path names that match the given pattern\)\. Examples of glob patterns include:
  + `/myapp/config/*`—All files inside config directory
  + `/**/*.png`—All \.png files in all directories
  + `/**/*.{png,ico,md}`—All \.png, \.ico or \.md files in all directories
  + `/myapp/src/**/*.ts`—All \.ts files inside src directory \(and all its subdirectories\)
  + `**/!(*.module).ts`—All \.ts files but not \.module\.ts
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.

------

### Learn more<a name="s3-learn-more"></a>

To learn more about integrating Amazon Kendra with your S3 data source, see:
+ [Search for answers accurately using Amazon KendraAmazon Kendra Connector with VPC support](https://aws.amazon.com/blogs/machine-learning/search-for-answers-accurately-using-amazon-kendra-s3-connector-with-vpc-support/)