--------

--------

# Salesforce Connector v1\.0<a name="data-source-v1-salesforce"></a>

Salesforce is a customer relationship management \(CRM\) tool for managing support, sales, and marketing teams\. You can use Amazon Kendra to index your Salesforce standard objects and even custom objects\.

**Important**  
Amazon Kendra uses the Salesforce API version 48\. The Salesforce API limits the number of requests that you can make per day\. If Salesforce exceeds those requests, it retries until it is able to continue\.

**Note**  
Support for Salesforce Connector v1\.0 / SalesforceConfiguration API is scheduled to end by June 2023\. We recommend using Salesforce Connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Salesforce data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v1-salesforce)
+ [Prerequisites](#prerequisites-v1-salesforce)
+ [Connection information](#data-source-procedure-v1-salesforce)
+ [Learn more](#salesforce-v1-learn-more)

## Supported features<a name="supported-features-v1-salesforce"></a>

Amazon Kendra Salesforce data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-v1-salesforce"></a>

Before you can use Amazon Kendra to index your Salesforce data source, make these changes in your Salesforce and AWS accounts\.

**In Salesforce, make sure you have:**
+ Created a Salesforce account and have copied the username and password you use to connect to Salesforce\.
+ Created a Salesforce connected app account with OAuth activated and have copied the consumer key \(client ID\) and consumer secret \(client secret\) assigned to your Salesforce connect app\.
+ Copied the Salesforce security token associated with the account used to connect to Salesforce\.
+ Copied the URL of the Salesforce server that you want to index\. Typically, this is *https://login\.salesforce\.com/services/oauth2/token*\. The server must be running a Salesforce connected app\.
+ Added credentials to your Salesforce server for a user with read\-only access to Salesforce by cloning the ReadOnly profile and then adding the View All Data and Manage Articles permissions\. These credentials identify the user making the connection and the Salesforce connected app that Amazon Kendra connects to\.

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.
+ Created an IAM role for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Salesforce authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Salesforce data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index id\.

## Connection information<a name="data-source-procedure-v1-salesforce"></a>

To connect Amazon Kendra to your Salesforce data source you must provide details of your Salesforce credentials so that Amazon Kendra can access your data\. If you have not yet configured Salesforce for Amazon Kendra see [Prerequisites](#prerequisites-v1-salesforce)\.

### <a name="salesforce-v1-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Salesforce** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Salesforce Connector v1\.0**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information: 

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\. 

   1. **Default language**— A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your shared costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Salesforce URL**—Enter your Salesforce server URL\.

   1. For **Type of authentication**, choose between **Existing** and **New** to store your Salesforce authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. 

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

        1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Salesforce\-’ is automatically added to your secret name\.

        1. For **User name**, **Password**, **Security token**, **Consumer key**, **Consumer secret**, and **Authentication URL**—Enter the authentication credential values you generated and downloaded from your Salesforce account\. 

        1. Choose **Save authentication**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. For **Crawl attachments**—Select to crawl all attached objects, articles, and feeds\.

   1. For **Standard objects**, **Knowledge articles**, and **Chatter feeds**—Select Salesforce entities or content types you want to crawl\.
**Note**  
You must provide configuration information for indexing at least one of standard objects, knowledge articles, or chatter feeds\. If you choose to crawl **Knowledge articles** you must specify the types of knowledge articles to index, the name of the articles, and whether to index the standard fields of all knowledge articles or only the fields of a custom article type\. If you choose to index custom articles, you must specify the internal name of the article type\. You can specify upto 10 article types\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Standard knowledge article**, **Standard object attachments**, and **Additional suggested field mappings** —Select from the Amazon Kendra generated default data source fields you want to map to your index\.
**Note**  
An index mapping to `_document_body` is required\. You can't change the mapping between the `Salesforce ID` field and the Amazon Kendra `_document_id `field\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Salesforce**

You must specify the following the [SalesforceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/SalesforceConfiguration.html) API:
+ **ServerUrl**—The instance URL for the Salesforce site that you want to index\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Salesforce account\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "authenticationUrl": "The OAUTH endpoint that Amazon Kendra connects to get an OAUTH token.",
      "consumerKey": "The application public key generated when you created your Salesforce application.",
      "consumerSecret": "The application private key generated when you created your Salesforce application.",
      "password": "The password associated with the user logging in to the Salesforce instance.",
      "securityToken": "The token associated with the user account logging in to the Salesforce instance.",
      "username": "The user name of the user logging in to the Salesforce instance."
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.
+ **IAM role**—Provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Salesforce connector and Amazon Kendra\. For more information, see [IAM roles for Salesforce data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You must provide configuration information for indexing at least one of standard objects, knowledge articles, or chatter feeds\.
  + **Standard objects**—If you choose to crawl **Standard objects**, you must specify the name of the standard object and the name of the field in the standard object table that contains the document contents\.
  + **Knowledge articles**—If you choose to crawl **Knowledge articles**, you must specify the types of knowledge articles to index, the states of the knowledge articles to index, and whether to index the standard fields of all knowledge articles or only the fields of a custom article type\.
  + **Chatter feeds**—If you choose to crawl **Chatter feeds**, you must specify the name of the column in the Salesforce FeedItem table that contains the content to index\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—Specify whether to include standard objects, knowledge articles, chatter feeds, attachments\. You can also specify regular expression patterns to include or exclude specific standard objects, knowledge articles, chatter feeds, attachments\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—Choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for Salesforce data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—Choose to map your Salesforce data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="salesforce-v1-learn-more"></a>

To learn more about integrating Amazon Kendra with your Salesforce data source, see:
+ [Getting started with Amazon Kendra Online connector](https://aws.amazon.com/blogs/machine-learning/getting-started-with-amazon-kendra--online-connector/)