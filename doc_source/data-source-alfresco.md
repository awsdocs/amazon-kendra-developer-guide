--------

--------

# Alfresco<a name="data-source-alfresco"></a>

Alfresco OnPrem is a content management service that helps customers store and manage their content\. You can use Amazon Kendra to index your Alfresco Document library, Wiki, and Blog\.

You can connect Amazon Kendra to your Alfresco data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [AlfrescoConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AlfrescoConfiguration.html) API\.

**Note**  
Alfresco data source connector is currently in preview mode\. Basic authentication is currently supported\. If you would like to use Alfresco connector in production, contact [Support](http://aws.amazon.com/contact-us/)\. Alfresco PaaS is not currently supported\.

For troubleshooting your Amazon Kendra Alfresco data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-alfresco)
+ [Prerequisites](#prerequisites-alfresco)
+ [Connection instructions](#data-source-procedure-alfresco)
+ [Learn more](#alfresco-learn-more)

## Supported features<a name="supported-features-alfresco"></a>

Amazon Kendra Alfresco data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-alfresco"></a>

Before you can use Amazon Kendra to index your Alfresco data source, make these changes in your Alfresco and AWS accounts\.

**In Alfresco, make sure you have:**
+ Noted your Alfresco authentication credentials, which include an admin user name and password\.
+ Added a user to `ALFRESCO_ADMINISTRATORS` group\.
+ Copied your Alfresco site URL and your Alfresco site ID\.
+ Checked each document is unique in Alfresco and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored a SSL certificate in an Amazon S3 bucket\.
+ Stored your Alfresco authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions 1\.0 and 2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Alfresco data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-alfresco"></a>

To connect Amazon Kendra to your Alfresco data source, you must provide the necessary details of your Alfresco data source so that Amazon Kendra can access your data\. If you have not yet configured Alfresco for Amazon Kendra see [Prerequisites](#prerequisites-alfresco)\.

### <a name="alfresco-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Alfresco** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **Alfresco connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Alfresco site URL**—Enter your Alfresco site URL\. For example, *https://hostname:8080*\. 

   1. **SSL certificate location**—Enter the Amazon S3 path\.

   1. **Site ID**—Your Alfresco Site ID\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Alfresco authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Alfresco\-’ is automatically added to your secret name\.

         1. For **User name** and **Password**—Enter your Alfresco user name and password\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Select content to crawl**—The Alfresco entities or content types you want to crawl\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. In **Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Document library**, **Wiki**, and **Blog**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Alfresco**

You must specify the following using the [AlfrescoConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_AlfrescoConfiguration.html) API:
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your Alfresco account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Alfresco connector and Amazon Kendra\. For more information, see [IAM roles for Alfresco data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+ **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` as part of the data source configuration\. See [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\. 
+  **Inclusion and exclusion filters**—Specify whether to include or exclude certain files\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your Alfresco data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for Alfresco data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------

## Learn more<a name="alfresco-learn-more"></a>

To learn more about integrating Amazon Kendra with your Alfresco data source, see:
+ [Intelligently search Alfresco content using Amazon Kendra](https://aws.amazon.com/blogs/machine-learning/intelligently-search-alfresco-content-using-amazon-kendra/)