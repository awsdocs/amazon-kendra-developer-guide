--------

--------

# Confluence Connector v1\.0<a name="data-source-v1-confluence"></a>

Confluence is a collaborative work\-management tool designed for sharing, storing, and working on project planning, software development, and product management\. You can use Amazon Kendra to index your Confluence spaces, pages \(including nested pages\), blogs, and comments and attachments to indexed pages and blogs\.

**Note**  
Support for Confluence Connector v1\.0 / ConfluenceConfiguration API is scheduled to end by June 2023\. We recommend using Confluence Connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Confluence data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v1-confluence)
+ [Prerequisites](#prerequisites-v1-confluence)
+ [Connection instructions](#data-source-procedure-v1-confluence)
+ [Learn more](#confluence-v1-learn-more)

## Supported features<a name="supported-features-v1-confluence"></a>

Amazon Kendra Confluence data source connector supports the following features:
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ \(For Confluence Server only\) Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-v1-confluence"></a>

Before you can use Amazon Kendra to index your Confluence data source, make these changes in your Confluence and AWS accounts\.

**In Confluence, make sure you have:**
+ Granted Amazon Kendra permissions to view all content within your Confluence instance by:
  + Making Amazon Kendra a member of `confluence-administrators` group\.
  + Granting site\-admin privileges for all existing spaces, blogs, and pages\.
+ Copied the URL of your Confluence instance\.
+ **For SSO \(Single Sign\-On\) users:** Activated the **Show on login page** for the user name and password when you configure Confluence **Authentication methods** in Confluence Data Center\.
+ **For Confluence Server**
  + Noted your basic authentication credentials containing your Confluence administrative account user name and password to connect to Amazon Kendra\.
  + **Optional:**Generated a personal access token in your Confluence account to connect to Amazon Kendra\. For more information, see [Confluence documentation on generating personal access tokens](https://confluence.atlassian.com/enterprise/using-personal-access-tokens-1026032365.html)\.
+ **For Confluence Cloud**
  + Generated an API token in your Confluence account\. You use this API token as password and your Confluence username as your user name for your authentication credentials\. For more information on how to generate the token, see [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)\.
  + **Optional:** Generated a personal access token in your Confluence account to connect to Amazon Kendra\. For more information, see [Confluence documentation on generating personal access tokens](https://confluence.atlassian.com/enterprise/using-personal-access-tokens-1026032365.html)\.
**Note**  
You must be a user with administrative permissions to the Confluence instance, whether you use basic authentication or personal access token\.
  + Checked each document is unique in Confluence and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your Confluence authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your Confluence data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-v1-confluence"></a>

To connect Amazon Kendra to your Confluence data source, you must provide details of your Confluence credentials so that Amazon Kendra can access your data\. If you have not yet configured Confluence for Amazon Kendra see [Prerequisites](#prerequisites-v1-confluence)\.

### <a name="confluence-v1-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Confluence** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **Confluence connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

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

   1. For **Additional configuration**—Specify regular expression patterns to include or exclude certain content\. You can add up to 100 patterns\.

   1. You can also choose to **Crawl attachments within chosen spaces**\.

   1. In **Sync run schedule**, for **Frequency**—Choose how often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Space**, **Page**, **Blog**—Select from the Amazon Kendra generated default data source fields or **Additional suggested field mappings** to add index fields\.

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to Confluence**

You must specify the following using [ConfluenceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConfluenceConfiguration.html) API:
+ **Confluence version**—Specify the version of the Confluence instance you are using as `CLOUD` or `SERVER`\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Confluence account\.

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

  If you are using Confluence Cloud as a Amazon Kendra data source, you use your Confluence user name and an API token generated in your Confluence account as your password\. You store the following credentials as a JSON structure in your Secrets Manager secret:

  ```
  {
      "username": "user name",
      "password": "API token"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Confluence connector and Amazon Kendra\. For more information, see [IAM roles for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+ **Web proxy**—Whether to connect to your Confluence URL instance via a web proxy\. You can use this option for Confluence Server\.
+ \(For Confluence Server only\) **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` as part of the data source configuration\. See [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.
+  **Inclusion and exclusion filters**—Specify regular expression patterns to include or exclude certain spaces, blog posts, pages, spaces, and attachments\. If you choose to index attachments, only attachments to the indexed pages and blogs are indexed\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your Confluence data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **User context filtering**—Amazon Kendra crawls the Access Control List \(ACL\) for your data source by default\. The ACL information is used to filter search results based on the user or their group access to documents\. For more information, see [User context filtering for Confluence data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

------

## Learn more<a name="confluence-v1-learn-more"></a>

To learn more about integrating Amazon Kendra with your Confluence data source, see:
+ [Configuring your Amazon Kendra Confluence Server connector ](http://aws.amazon.com/blogs/machine-learning/configuring-your-amazon-kendra-confluence-server-connector/)