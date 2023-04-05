--------

--------

# Zendesk<a name="data-source-zendesk"></a>

Zendesk is a customer relationship management system that helps businesses automate and enhance customer support interactions\. You can use Amazon Kendra to index your Zendesk support tickets, ticket comments, ticket attachments, help center articles, article comments, article comment attachments, guide community topics, community posts, and community post comments\.

You can filter by organization name if you want to index tickets that are only within a specific organization\. You can also choose to set a crawl date for when you want to start crawling data from Zendesk\.

You can connect Amazon Kendra to your Zendesk data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\.

For troubleshooting your Amazon Kendra Zendesk data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-zendesk)
+ [Prerequisites](#prerequisites-zendesk)
+ [Connection instructions](#data-source-procedure-zendesk)
+ [Learn more](#zendesk-learn-more)

## Supported features<a name="supported-features-zendesk"></a>

Amazon Kendra Zendesk data source connector supports the following features:
+ Change log
+ Field mapping
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-zendesk"></a>

Before you can use Amazon Kendra to index your Zendesk data source, make these changes in your Zendesk and AWS accounts\.

**In Zendesk, make sure you have:**
+ Created a Zendesk Suite \(Professional/Enterprise\) administrative account\.
+ Noted your Zendesk host URL\. For example, *https://\{sub\-domain \(https://\{host/\)\}\.zendesk\.com/*\.
+ Generated an OAuth 2\.0 credential token containing a client ID, client secret, user name, and password\. See [Zendesk documentation on generating OAuth 2\.0 tokens](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) for more information\.
+ Added the following OAuth 2\.0 scope:
  + read
+ **Optional:** Installed an SSL certificate to allow Amazon Kendra to connect\.
+ Checked each document is unique in Zendesk and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Zendesk authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Zendesk data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-zendesk"></a>

To connect Amazon Kendra to your Zendesk data source, you must provide the necessary details of your Zendesk data source so that Amazon Kendra can access your data\. If you have not yet configured Zendesk for Amazon Kendra see [Prerequisites](#prerequisites-zendesk)\.

### <a name="zendesk-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Zendesk** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **Zendesk connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Zendesk URL**—Enter your Zendesk URL\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Zendesk authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Zendesk\-’ is automatically added to your secret name\.

         1. For **Client ID**, **Client secret**, **User name**, **Password**—Enter the authentication credential values you created in your Zendesk account\.

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Select entities or content types**—The Zendesk entities or content types you want to crawl\.

   1. **Change log**—Select to update your index instead of syncing all your files\.

   1. **Organization name**—Enter the Zendesk organization names to filter your sync\.

   1. **Sync start date**—The date from which you want to index your content\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. In **Sync run schedule** for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Tickets**, **Ticket comment**, **Ticket comment attachment**, **Article**, **Article comment**, **Article comment attachment**, **Community topic**, **Community post**, **Community post comment**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Zendesk**

You must specify a JSON of the [data source schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\. You must provide the following information:
+ **Data source**—Specify the data source as `ZENDESK`\.
+ **Host URL**—Provide your Zendesk host URL as part of the connection configuration or repository endpoint details\. For example, * https://yoursubdomain\.zendesk\.com*\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials for your Zendesk account\. The secret is stored in a JSON structure with the following keys:

  ```
  {
      "hostUrl": "https://yoursubdomain.zendesk.com",
      "clientId": "kendra",
      "clientSecret": "Zendesk client secret",
      "userName": "Zendesk user name",
      "password": "Zendesk password"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Zendesk connector and Amazon Kendra\. For more information, see [IAM roles for Zendesk data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+  **Change log**—Whether Amazon Kendra should use the Zendesk data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Zendesk data source than to process the change log\. If you are syncing your Zendesk data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—Specify whether to include or exclude:
  + Support tickets, ticket comments, and/or ticket comment attachments
  + Help center articles, article attachments, and article comments
  + Guide community topics, posts, or post comments
+ 
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your Zendesk data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for Zendesk data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

 For a list of other important JSON keys to configure, see [Zendesk template schema](ds-schemas.md#ds-schema-zendesk)\.

------

## Learn more<a name="zendesk-learn-more"></a>

To learn more about integrating Amazon Kendra with your Zendesk data source, see:
+ [Discover insights from Zendesk with Amazon Kendra intelligent search](https://aws.amazon.com/blogs/machine-learning/discover-insights-from-zendesk-with-amazon-kendra-intelligent-search/)