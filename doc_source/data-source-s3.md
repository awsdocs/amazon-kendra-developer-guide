--------

--------

# Amazon S3<a name="data-source-s3"></a>

Amazon S3 is an object storage service that stores data as objects within buckets\. You can use Amazon Kendra to index your Amazon S3 bucket repository of documents\.

**Warning**  
Amazon Kendra doesn't use a bucket policy that grants permissions to an Amazon Kendra principal to interact with an S3 bucket\. Instead, it uses IAM roles\. Make sure that Amazon Kendra isn't included as a trusted member in your bucket policy to avoid any data security issues in accidentally granting permissions to arbitrary principals\. However, you can add a bucket policy to use an Amazon S3 bucket across different accounts\. For more information, see [Policies to use Amazon S3 across accounts](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3-cross-accounts)\. For information about IAM roles for S3 data sources, see [IAM roles](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3)\.

You can connect Amazon Kendra to your Amazon S3 data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [S3DataSourceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_S3DataSourceConfiguration.html) API\.

For troubleshooting your Amazon Kendra S3 data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-s3)
+ [Prerequisites](#prerequisites-s3)
+ [Connection instructions](#data-source-procedure-s3)
+ [Creating an Amazon S3 data source](create-ds-s3.md)
+ [Amazon S3 document metadata](s3-metadata.md)
+ [Access control for Amazon S3 data sources](s3-acl.md)

## Supported features<a name="supported-features-s3"></a>

Amazon Kendra S3 data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-s3"></a>

Before you can use Amazon Kendra to index your S3 data source, make these changes in your S3 and AWS accounts\.

**In S3, make sure you have:**
+ Copied the name of your Amazon S3 bucket name\.
**Note**  
Your bucket must be in the same region as your Amazon Kendra index and your index must have permission to access the bucket that contains your documents\.

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.
+ Created an IAM role for your data source and, if using the API, noted the ARN of the IAM role\.

If you don’t have an existing IAM role, you can use the console to create a new IAM role when you connect your S3 data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and an index id\.

## Connection instructions<a name="data-source-procedure-s3"></a>

To connect Amazon Kendra to your Amazon S3 data source you must provide details of your Amazon S3 credentials so that Amazon Kendra can access your data\. If you have not yet configured Amazon S3 for Amazon Kendra see [Prerequisites](#prerequisites-s3)\.

### <a name="s3-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Amazon S3 ** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **S3**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Enter the data source location**—The path to the Amazon S3 bucket where your data is stored\. Select **Browse S3** to choose your bucket\.

   1. \(Optional\) **Metadata files prefix folder location**—The path to the folder in which your metadata is stored\. Select **Browse S3** to locate your metadata folder\.

   1. \(Optional\) **Access control list configuration file location**—The path to the location of a file containing a JSON structure that specifies access settings for the files stored in your S3 data source\. Select **Browse S3** to locate your ACL file\.

   1. \(Optional\) **Decription key**—Select to use a decription key\. You can choose to use an existing one or create a new one\.

   1. \(Optional\) **Additional configurations**—Add patterns to include or exclude documents from your index\.All paths are relative to the data source location S3 bucket\. You can have a combined total of 100 patterns\.

   1. In**Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Amazon S3**

You must specify the following using the [S3DataSourceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_S3DataSourceConfiguration.html) API:
+  **BucketName**—The name of the bucket that contains the documents\.
+ **IAM role**—Provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the S3 connector and Amazon Kendra\. For more information, see [IAM roles for S3 data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—Specify glob patterns to include or exclude certain files\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—Choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for S3 data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------