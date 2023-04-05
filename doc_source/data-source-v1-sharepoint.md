--------

--------

# SharePoint connector v1\.0<a name="data-source-v1-sharepoint"></a>

SharePoint is a collaborative website building service that you can use to customize web content and create pages, sites, document libraries, and lists\. If you are a SharePoint user, you can use Amazon Kendra to index your SharePoint data source\.

**Note**  
Support for SharePoint Connector v1\.0 / SharePointConfiguration API is scheduled to end by June 2023\. We recommend using SharePoint Connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra SharePoint data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v1-sharepoint)
+ [Prerequisites](#prerequisites-v1-sharepoint)
+ [Connection instructions](#data-source-procedure-v1-sharepoint)
+ [Learn more](#sharepoint-v1-learn-more)

## Supported features<a name="supported-features-v1-sharepoint"></a>
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-v1-sharepoint"></a>

Before you can use Amazon Kendra to index your SharePoint data source, make these changes in your SharePoint and AWS accounts\.

**In SharePoint, make sure you have:**
+ Created a SharePoint user with administrative permissions\.
+ Noted the URL of the SharePoint sites you want to index\.
+ **For SharePoint Online:**
  + Noted your basic authentication credentials containing a user name and password\.
  + **Optional: **Generated OAuth 2\.0 credentials containing a user name, password, client ID, and client secret\.
  + Deactivated **Security Defaults** in your Azure portal using an administrative user\. For more information on managing security default settings in the Azure portal, see [Microsoft documentation on how to enable/disable security defaults](https://learn.microsoft.com/en-us/microsoft-365/business-premium/m365bp-conditional-access?view=o365-worldwide&tabs=secdefaults#security-defaults-1)\.
+ **For SharePoint Server:**
  + Noted your SharePoint Server domain name \(the NetBIOS name in your Active Directory\)\. You use this, along with your SharePoint basic authentication user name and password, to connect SharePoint Server to Amazon Kendra\.
**Note**  
If you use SharePoint Server and need to convert your Access Control List \(ACL\) to email format for filtering on user context, provide the LDAP server URL and LDAP search base\. Or you can use the directory domain override\. The LDAP server URL is the full domain name and the port number \(for example, ldap://example\.com:389\)\. The LDAP search base are the domain controllers 'example' and 'com'\. With the directory domain override, you can use the email domain instead of using LDAP server URL and LDAP search base\. For example, the email domain for username@example\.com is 'example\.com'\. You can use this override if you aren't concerned about validating your domain and simply want to use your email domain\.
+ Added the following permissions to your SharePoint account:

  **For SharePoint lists**
  + Open Items—View the source of documents with server\-side file handlers\.
  + View Application Pages—View forms, views, and application pages\. Enumerate lists\.
  + View Items—View items in lists and documents in document libraries\.
  + View Versions—View past versions of a list item or document\.

  **For SharePoint websites**
  + Browse Directories—Enumerate files and folders in a website using SharePoint Designer and Web DAV interface\.
  + Browse User Information—View information about users of the website\.
  + Enumerate Permissions—Enumerate permissions on the website, list, folder, document, or list item\.
  + Open—Open a website, list, or folder to access items inside the container\.
  + Use Client Integration Features—Use SOAP, WebDAV, the client object model, or SharePoint Designer interfaces to access the website\.
  + Use Remote Interfaces—Use features that launch client applications\.
  + View Pages—View pages on a website\.
+ Checked each document is unique in SharePoint and across other data sources you plan to use for the same index\. Each data source that you want to use for an index must not contain the same document across the data sources\. Document IDs are global to an index and must be unique per index\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ Stored your SharePoint authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or Secrets Manager secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your SharePoint data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-v1-sharepoint"></a>

To connect Amazon Kendra to your SharePoint data source you must provide details of your SharePoint credentials so that Amazon Kendra can access your data\. If you have not yet configured SharePoint for Amazon Kendra see [Prerequisites](#prerequisites-v1-sharepoint)\.

### <a name="sharepoint-v1-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to SharePoint** 

1. Sign in to the AWS Management Console and open the [Amazon Kendra console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to use from the list of indexes\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Getting started** page, choose **Add data source**\.

1. On the **Add data source** page, choose **SharePoint connector**, and then choose **Add data source**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. For **Hosting method**—Choose between **SharePoint Online** and **SharePoint Server**\.

      1. For **SharePoint Online**—Enter the **Site URLs specific to your SharePoint repository**\.

      1. For **SharePoint Server**—Choose your **SharePoint version**, enter **Site URLs specific to your SharePoint repository**, and enter the Amazon S3 path to your **SSL certificate location**\.

   1. \(SharePoint Server only\) For **Web proxy**—Enter the **Host name** and **Port number** of your internal SharePoint instance\. The port number should be a numeric value between 0 and 65535\.

   1. For **Authentication**—Choose between the following options based on your use case:

      1. For SharePoint Online—Choose between **Basic authentication** and **OAuth 2\.0 authentication**\.

      1. For SharePoint Server—Choose between **None**, **LDAP**, and **Manual**\.

   1. For **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your SharePoint authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. You must enter a **Secret name**\. The prefix ‘AmazonKendra\-SharePoint\-’ is automatically added to your secret name\.

   1. Enter following other information in the **Create an AWS Secrets Manager secret window**:

      1. Choose from the following SharePoint Cloud authentication options, based on your use case:

         1. **Basic authentication**—Enter your SharePoint account user name as **User name** and SharePoint account password as **Password**\.

         1. **OAuth 2\.0 authentication**—Enter your SharePoint account user name as **User name**, SharePoint account password as **Password**, your auto\-generated unique SharePoint ID as **Client ID**, and the shared secret string used by both SharePoint and Amazon Kendra as **Client secret**\.

      1. Choose from the following SharePoint Server authentication options, based on your use case:

         1. **None**—Enter your SharePoint account user name as **User name**, your SharePoint account password as **Password**, and your **Server Domain Name**\.

         1. **LDAP**—Enter your SharePoint account user name as **User name**, SharePoint account password as **Password**, your **LDAP Server Endpoint** \(including protocol and port number, for example *ldap://example\.com:389*\), and your **LDAP Search Base** \(for example, *dc=example, dc=com*\)\.

         1. **Manual**—Enter your SharePoint account user name as **User name**, your SharePoint account password as **Password**, and your **Email Domain Override** \(email domain of directory user or group\)\.

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**— You must also add **Subnets** and **VPC security groups**\.
**Note**  
You must use a VPC if you use SharePoint Server\. Amazon VPC is optional for other SharePoint versions\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Use Change log**—Select to update your index instead of syncing all your files\.

   1. **Crawl attachments**—Select to crawl attachments\.

   1. **Use local group mappings**—Select to make sure that documents are properly filtered\.

   1. **Additional configuration**—Add regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. In **Sync run schedule** for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. **Amazon Kendra default field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1. For **Custom field mappings**—Add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to SharePoint**

You must specify the following using [SharePointConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SharePointConfiguration.html) API:
+ **SharePoint Version**—Specify the SharePoint version you use when configuring SharePoint\. This is the case no matter if you use SharePoint Server 2013, SharePoint Server 2016, SharePoint Server 2019, or SharePoint Online\.
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your SharePoint account\.The secret is stored in a JSON structure\.

  For **SharePoint Online basic authentication**, the following is the minimum JSON structure that must be in your secret:

  ```
  {
      "username": "user name",
      "password": "password"
  }
  ```

  For **SharePoint Online OAuth 2\.0 authentication**, the following is the minimum JSON structure that must be in your secret:

  ```
  {
      "username": "SharePoint account user name",
      "password": "SharePoint account password",
      "clientId": "SharePoint auto-generated unique client id",
      "clientSecret": "secret string shared by Amazon Kendra and SharePoint to authorize communications
  }
  ```

  For **SharePoint Server basic authentication**, the following is the minimum JSON structure that must be in your secret:

  ```
  {
      "username": "user name",
      "password": "password",
      "domain": "server domain name"
  }
  ```

  For **SharePoint Server LDAP authentication** \(if you need to convert your Access Control List \(ACL\) to email format for filtering on user context you can include the LDAP server URL and LDAP search base in your secret\), the following is the minimum JSON structure that must be in your secret:

  ```
  {
      "username": "user name",
      "password": "password",
      "domain": "server domain name"
      "ldapServerUrl": "ldap://example.com:389",
      "ldapSearchBase": "dc=example,dc=com"
  }
  ```

  For **SharePoint Server Manual authentication**, the following is the minimum JSON structure that must be in your secret::

  ```
  {
      "username": "user name",
      "password": "password",
      "domain": "server domain name",
      "emailDomainOverride": "example.com"
  }
  ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the SharePoint connector and Amazon Kendra\. For more information, see [IAM roles for SharePoint data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+  **Amazon VPC**—If you use SharePoint Server, specify `VpcConfiguration` as part of the data source configuration\. See [Configuring Amazon Kendra to use a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.

You can also add the following optional features:
+ **Web proxy**—Whether to connect to your SharePoint site URLs via a web proxy\. You can use this option only for SharePoint Server\.
+ **Indexing lists**—Whether Amazon Kendra should index the contents of attachments to SharePoint list items\.
+  **Change log**—Whether Amazon Kendra should use the SharePoint data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the SharePoint data source than to process the change log\. If you are syncing your SharePoint data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—You can specify whether to include or exclude content\. You can also specify regular expression patterns to include or exclude\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your SharePoint data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="sharepoint-v1-learn-more"></a>

To learn more about integrating Amazon Kendra with your SharePoint data source, see:
+ [Getting started with the Amazon Kendra SharePoint Online connector](https://aws.amazon.com/blogs/machine-learning/getting-started-with-the-amazon-kendra-sharepoint-online-connector/)