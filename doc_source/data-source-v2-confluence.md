--------

--------

# Confluence Connector v2\.0<a name="data-source-v2-confluence"></a>

Confluence is a collaborative work\-management tool designed for sharing, storing, and working on project planning, software development, and product management\. You can use Amazon Kendra to index your Confluence spaces, pages \(including nested pages\), blogs, and comments and attachments to indexed pages and blogs\.

For troubleshooting your Amazon Kendra Confluence data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v2-confluence)
+ [Prerequisites](#prerequisites-v2-confluence)
+ [Connection instructions](#data-source-procedure-v2-confluence)

## Supported features<a name="supported-features-v2-confluence"></a>

Amazon Kendra Confluence data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Virtual private cloud \(VPC\)
+ Sync all documents/ Sync only new, modified, or deleted documents
+ Inclusion/exclusion patterns

## Prerequisites<a name="prerequisites-v2-confluence"></a>

Before you can use Amazon Kendra to index your Confluence data source, make these changes in your Confluence and AWS accounts\.

**In Confluence, make sure you have:**
+ Copied your Confluence instance URL\. For example: *https://example\.confluence\.com*\. You need your Confluence instance URL to connect to Amazon Kendra\.
+ Configured basic authentication credentials containing a user name \(email ID used to log into Confluence\) and password \(Confluence API token\) to allow Amazon Kendra to connect to your Confluence instance\. For information on how to create a Confluence API token, see [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/#Create-an-API-token)\.
+ **Optional:** Configured OAuth 2\.0 credentials containing a Confluence app key, Confluence app secret, Confluence access token, and Confluence refresh token to allow Amazon Kendra to connect to your Confluence instance\. If your access token expires, you can either use the refresh token to regenerate your access token and refresh token pair\. Or, you can repeat the authorization process\. For more information on access tokens, see [Manage OAuth access tokens](https://support.atlassian.com/confluence-cloud/docs/manage-oauth-access-tokens/)\.
+ \(For Confluence Server only\) **Optional:** Configured a Personal Access Token \(PAT\) containing a Confluence token to allow Amazon Kendra to connect to your Confluence instance\. For information on how to create a PAT token, see [Using Personal Access Tokens](https://confluence.atlassian.com/enterprise/using-personal-access-tokens-1026032365.html)\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Confluence authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Confluence data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-v2-confluence"></a>

To connect Amazon Kendra to your Confluence data source, you must provide details of your Confluence credentials so that Amazon Kendra can access your data\. If you have not yet configured Confluence for Amazon Kendra see [Prerequisites](#prerequisites-v2-confluence)\.

### <a name="confluence-v2-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Confluence** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **Confluence Connector v2\.0**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. In **Source**, choose between **Confluence cloud** and **Confluence server** based on your Confluence data source hosting method\.\.

   1. **Confluence URL**—Enter the Confluence host URL\. The format for the host URL you enter is *https://example\.confluence\.com*\.

   1. Choose between **Basic authentication**, **Oauth 2\.0 authentication** and \(For Confluence server only\) **Personal Access Token authentication** based on your use case\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Confluence authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. Enter the following information in the window:

      1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Confluence\-’ is automatically added to your secret name\.

      1. If using **Basic Authentication**—Enter the **Secret name** **User name**, and **Password** \(Confluence API token\) you generated and downloaded from your Confluence account\.

         If using **OAuth2\.0 Authentication**—Enter the **Secret name**, **App key**, **App secret**, **Access token**, and **Refresh token** you created in your Confluence account\.

         \(Confluence server only\) If using **Personal Access Token authentication**—Enter the **Secret name** and **Confluence token** you created in your Confluence account\.

      1. Choose **Save and add secret**\.

   1. In **Configure VPC and security group \- optional**, for **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **Identity crawler**—Choose to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. In **Sync scope**, for **sync contents**, choose to sync from the following entity types: **Pages**, **Page comments** **Page attachments** **Blogs**, **Blog comments** **Blog attachments**, **Personal spaces** **Archived spaces**, and **Archived pages**\.
**Note**  
 **Page comments** and **Page attachments** can only be seleted if you choose to sync **Pages**\. **Blog comments** and **blog attachments** can only be seleted if you choose to sync **Blogs**\.

   1. In **Additional configuration** for **Spaces regex patterns**, specify whether to include or exclude specific spaces in your index using:
      + **Space key**—For example, *my\-space\-123*\.
      + **URL**—For example, *\.\*/MySite/MyDocuments/*\.
      + **File type**—For example, *\.pdf, \.txt*\.
      + For **Entity title regex patterns**—Specify regular expression patterns to include or exclude certain **Blogs**, **Pages**, **Comments**, and **Attachments** by titles\.

   1. For **Sync mode** choose how you want to update your index when your data source content changes\. When you sync your data source with Amazon Kendra for the first time, all content is synced by default\.
      + **Full sync**—Sync all content regardless of the previous sync status\.
      + **New, modified, or deleted content sync**—Only sync new, modified, and deleted content\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Space**, **Page**, **Blog**, **Comment** and **Attachment**—Select from the Amazon Kendra generated default data source fields that you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Confluence**

You must specify a JSON of the [data source schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\. You must provide the following information:
+ **Data source**—Specify the data source as `CONFLUENCEV2`\. 
+ **Host URL**—Specify the Confluence host instance version\. For example, *https://example\.confluence\.com*\.
+ **Auth type**—Specify the type of authentication, whether `Basic`, `OAuth2`, `Personal-token` for your Confluence instance\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+ **Sync mode**—Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between:
  + `FORCED_FULL_CRAWL` to crawl and sync all content to your index
  + `FULL_CRAWL` to crawl all content and sync only new, modified, or deleted content
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Confluence account\. If you use basic account authentication, the secret is stored in a JSON structure with the following keys: 

  ```
  {
  "username": "Confluence account user name",
  "password": "Confluence API token"
  }
  ```

  If you use OAuth 2\.0 authentication, the secret is stored in a JSON structure with the following keys:

  ```
  {
  "confluenceAppKey": "app key for your Confluence account",
  "confluenceAppSecret": "app secret from your Confluence token",
  "confluenceAccessToken": "access token created in Confluence",
  "confluenceRefreshToken": "refresh token created in Confluence"
  }
  ```

  \(For Confluence Server only\) If you use Personal Access Token authentication, the secret is stored in a JSON structure with the following keys:

  ```
  {
  "patToken": "Confluence token"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Confluence connector and Amazon Kendra\. For more information, see [IAM roles for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Inclusion and exclusion filters**—You can specify whether to include or exclude certain spaces, pages, blogs, and their comments and attachments\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+ **Enable identity crawler**—Specify whether to activate identity crawler\. If identity crawler is deactivated, you must upload the principal information using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API\.
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+  **Field mappings**—Choose to map your Confluence data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

For a list of other important JSON keys to configure, see [Confluence template schema](ds-schemas.md#ds-confluence-schema)\.

------

### Notes<a name="confluence-notes"></a>
+ Personal Access Token \(PAT\) is not available for Confluence Cloud\.