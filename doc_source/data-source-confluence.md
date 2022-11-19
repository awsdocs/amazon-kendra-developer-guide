--------

--------

# Using a Confluence data source<a name="data-source-confluence"></a>

Confluence is a collaborative work\-management tool designed for sharing, storing, and working on project planning, software development, and product management\. As a Confluence user, you can organize your workspace into a site which can have multiple spaces, pages, blogs, and attachments\.

If you are a Confluence user, you can use Amazon Kendra to index your Confluence spaces, pages \(including nested pages\), blogs, and attachments to indexed pages and blogs\. You can also specify regular expression patterns to include or exclude specific blog posts, pages, spaces, or attachments in your Confluence data source\.

**Note**  
By default, Amazon Kendra doesn't index Confluence archives and personal spaces\. You can choose to index them when you create the data source\. If you don't want Amazon Kendra to index a space, mark it private in Confluence\.

Amazon Kendra supports Confluence Cloud and Confluence Server\.

You can connect Amazon Kendra to your Confluence data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [ConfluenceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConfluenceConfiguration.html) API\.

For troubleshooting your Amazon Kendra Confluence data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-confluence)
+ [Prerequisites](#prerequisites-confluence)
+ [Connecting Amazon Kendra to your Confluence data source](#data-source-procedure-confluence)
+ [Learn more](#confluence-learn-more)

## Supported features<a name="supported-features-confluence"></a>
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

## Prerequisites<a name="prerequisites-confluence"></a>

Before you can use Amazon Kendra to index your Confluence data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your Confluence data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have a Confluence administrative account in which you have granted Amazon Kendra permission to view all of the content within your Confluence instance\. You can grant the account these permissions by making it a member of the `confluence-administrators` group and granting the account `site-admin` privileges for all existing spaces, blogs, and pages\. If you use Single Sign\-On \(SSO\) with Confluence, you must enable **Show on login page** for the user name and password when you configure Confluence **Authentication methods** in Confluence Data Center\.
+ You have generated authentication credentials to connect to Amazon Kendra to Confluence Server\. You can connect Amazon Kendra to Confluence Server in two ways:
  + You can use your Confluence administrative account username and password\.
  + You can use a personal access token that you generate in your Confluence account\. For more information on generating a personal access token in your Confluence account, see [Confluence Documentation](https://confluence.atlassian.com/enterprise/using-personal-access-tokens-1026032365.html)\. 
+ You have generated authentication credentials to connect Confluence Cloud to Amazon Kendra\. The credentials required are your Confluence username and an API token as your password\. You generate the API token in your [Confluence account](https://id.atlassian.com/manage-profile/security/api-tokens)\.
**Note**  
You must be a user with administrative permissions to the Confluence instance, whether you use basic authentication or personal access token\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. 
+ You have copied the URL of your Confluence instance\. You will need this URL to connect Amazon Kendra to your Confluence data source\.

  You can find more information on how to configure your Confluence account on the [Confluence Documentation](https://support.atlassian.com/confluence-cloud/resources/) page\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your Confluence data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your Confluence data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your Confluence data source<a name="data-source-procedure-confluence"></a>

To connect Amazon Kendra to your Confluence data source you must provide details of your Confluence credentials so that Amazon Kendra can access your data\. If you have not yet configured Confluence for Amazon Kendra see [Prerequisites](#prerequisites-confluence)\.

### <a name="confluence-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Confluence** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Confluence**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. Choose between **Confluence cloud** and **Confluence server** based on your use case\.

   1. If you choose **Confluence cloud**, enter the following information:

      1. **Confluence URL**—Your Confluence URL\.

      1. **Basic authentication**—Confluence host name\.

      1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Confluence authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

         1. Enter following information in the **Create an AWS Secrets Manager secret window**:

           1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Confluence\-’ is automatically added to your secret name\.

           1. For **User name** and **Password**—Enter your Confluence user name and your Confluence API token as the password\. 

           1. Choose **Save authentication**\.

   1. If you choose **Confluence server**, enter the following information:

      1. **Confluence URL**—Your Confluence user name and password\.

      1. \(Optional\) For **Web proxy** enter the following information:

         1.  **Host name**—Host name for your Confluence account\.

         1.  **Port number**—Port used by the host URL transport protocol\.

      1. Choose between **Basic authentication** and **Personal Access Token**\.

      1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Confluence authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

         1. Enter following information in the **Create an AWS Secrets Manager secret window**:

           1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Confluence\-’ is automatically added to your secret name\.

           1. For **User name** and **Password**—Enter the authentication credential values you generated and downloaded from your Confluence account\. If using basic authentication, use your Confluence user name and password as your authentication credential\. If using personal access token, enter the details of the **Personal Access Token** you created in your Confluence account\.

           1. Choose **Save authentication**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. For **Include personal spaces** and **Include archived spaces**—Choose the optional space types to include in this data source\.

   1. For **Additional configuration**—Choose regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. You can also choose to **Crawl attachments within chosen spaces**\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Space**, **Page**, **Blog**—Select from the Amazon Kendra generated default data source fields or **Additional suggested field mappings** to add index fields\.

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ ConfluenceConfiguration API ]

**To connect Amazon Kendra to Confluence**

You must specify the following using [ConfluenceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConfluenceConfiguration.html) API:
+ **Confluence version**—You must specify the version of the Confluence instance you are using as `CLOUD` or `SERVER`\.
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Confluence account\. You provide the ARN using the `CreateDataSource` API\.

  If you are using Confluence Server, you can use either your Confluence user name and password, or your personal access token as credentials\.

  When you use your Confluence user name and password as authentication credentials, you store the following credentials as a JSON structure in your Secrets Manager secret:

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```

  If you are using a personal access token to connect Confluence Server to Amazon Kendra, you store the following credentials as a JSON structure in your Secrets Manager secret:

  ```
  {
      "patToken": "personal access token"
  }
  ```

  If you are using Confluence Cloud as a Amazon Kendra data source, you use your Confluence username and an API token generated in your Confluence account as your password\. You store the following credentials as a JSON structure in your Secrets Manager secret:

  ```
  {
      "username": "user name",
      "password": "API token generated"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Confluence connector and Amazon Kendra\. For more information, see [IAM roles for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+ **Web proxy**—Whether to connect to your Confluence URL instance via a web proxy\. You can use this option for Confluence Server\.
+  **Inclusion and exclusion filters**—You can specify whether to include spaces, blog posts, pages, spaces, or attachments\. You can also specify regular expression patterns to include or exclude specific blog posts, pages, spaces, or attachments\.Amazon Kendra indexes blogs, pages, and regular spaces by default\. If you choose to index attachments, only attachments to the indexed pages and blogs are indexed\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your Confluence data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="confluence-learn-more"></a>

To learn more about integrating Amazon Kendra with your Confluence data source, see:
+ [Configuring your Amazon Kendra Confluence Server connector ](https://aws.amazon.com/blogs/machine-learning/configuring-your-amazon-kendra-confluence-server-connector/)