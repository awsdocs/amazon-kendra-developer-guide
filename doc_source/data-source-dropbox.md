--------

--------

# Dropbox<a name="data-source-dropbox"></a>

Dropbox is a file hosting service that offers cloud storage, document organization, and document templating services\. If you are a Dropbox user, you can use Amazon Kendra to index your Dropbox files, Dropbox Paper, Dropbox Paper Templates, and stored shortcuts to web pages\. You can also configure Amazon Kendra to index specific Dropbox files, Dropbox Paper, Dropbox Paper Templates, and stored shortcuts to web pages\.

Amazon Kendra supports both Dropbox and Dropbox Advanced for Dropbox Business\.

You can connect Amazon Kendra to your Dropbox data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\.

For troubleshooting your Amazon Kendra Dropbox data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-dropbox)
+ [Prerequisites](#prerequisites-dropbox)
+ [Connection instructions](#data-source-procedure-dropbox)
+ [Learn more](#dropbox-learn-more)

## Supported features<a name="supported-features-dropbox"></a>

Amazon Kendra Dropbox data source connector supports the following features:
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-dropbox"></a>

Before you can use Amazon Kendra to index your Dropbox data source, make these changes in your Dropbox and AWS accounts\.

**In Dropbox, make sure you have:**
+ Created a Dropbox Advanced account and set up an admin user\.
+ Created a Dropbox app with a unique **App name**, activated **Scoped Access**, and **Full Dropbox** permissions\.
+ Set up basic authentication credentials that include an app name, an app key, an app secret, and an access token using your admin user\.
+ Generated and copied a temporary Oauth 2\.0 access token for your Dropbox app\. This token is temporary and expires after 4 hours\.
**Note**  
It is recommended that you create a Dropbox refresh access token that never expires, rather that relying on a one\-time access token that expires after 4 hours\. A refresh access token is permanent and never expires so that you can continue to sync your data source in the future\.
+ **Recommended:** Configured a Dropbox permanent refresh token that never expires to allow Amazon Kendra to continue to sync your data source without any disruptions\.
+ Added the following Oauth scopes and read permissions:
  +  files\.content\.read
  +  files\.metadata\.read
  +  sharing\.read
  +  file\_requests\.read
  +  groups\.read
  + team\_info\.read
  +  team\_data\.content\.read

**In your AWS account, make sure you have:**
+ Created an Amazon Kendra index and, if using the API, noted the index id\.
+ Created an IAM role for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Dropbox authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Dropbox data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index id\.

## Connection instructions<a name="data-source-procedure-dropbox"></a>

To connect Amazon Kendra to your Dropbox data source you must provide details of your Dropbox credentials so that Amazon Kendra can access your data\. If you have not yet configured Dropbox for Amazon Kendra see [Prerequisites](#prerequisites-dropbox)\.

### <a name="dropbox-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Dropbox** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Dropbox**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Type of authentication token**—Choose between **Permanent Token \(recommended\)** and **Access Token \(temporary use\) **based on your use case\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Dropbox authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Dropbox\-’ is automatically added to your secret name\.

         1. For **App key**, **App secret**, and **Permanent token**—Enter the authentication credential values you generated and downloaded from your Dropbox account\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. For **Select entities or content types**—Choose entities or content types you want to crawl\.

   1. **Change log mode**—Choose to update your index instead of syncing all files\.

   1. In **Additional configuration** for **Regex patterns**—Add regular expression patterns to include or exclude specific files\.

   1. In **Sync run schedule**, for **Frequency**— Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Files**, **Dropbox Paper**, and **Dropbox Paper templates**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ TemplateConfiguration API ]

**To connect Amazon Kendra to Dropbox**

You must specify the following using [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API:
+ **Data source**—You must specify the data source as `DROPBOX`\.
+ **Data source schema**—Include a JSON that contains the data source schema\. To view the template schema, see [Data source schemas](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Dropbox account\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
  "appKey": "Dropbox app key",
  "appSecret": "Dropbox app secret",
  "accesstoken": "temporary access token or refresh access token"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\.
+ **IAM role**—Provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Dropbox connector and Amazon Kendra\. For more information, see [IAM roles for Dropbox data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+  **Change log**—Whether Amazon Kendra should use the Dropbox data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Dropbox data source than to process the change log\. If you are syncing your Dropbox data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—Specify whether to include Dropbox files\. Dropbox Paper, or Dropbox templates\. You can also specify regular expression patterns to include or exclude Dropbox files\. Dropbox Paper, or Dropbox templates\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—Choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for Dropbox data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—Choose to map your Dropbox data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

For a list of other important JSON keys to configure, see [Dropbox template schema](ds-schemas.md#ds-dropbox-schema)\.

------

## Learn more<a name="dropbox-learn-more"></a>

To learn more about integrating Amazon Kendra with your Dropbox data source, see:
+ [Index your Dropbox content using the Dropbox connector for Amazon Kendra](https://aws.amazon.com/blogs/machine-learning/index-your-dropbox-content-using-the-dropbox-connector-for-amazon-kendra/)