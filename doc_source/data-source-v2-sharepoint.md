--------

--------

# SharePoint connector v2\.0<a name="data-source-v2-sharepoint"></a>

SharePoint is a collaborative website building service that you can use to customize web content and create pages, sites, document libraries, and lists\. You can use Amazon Kendra to index your SharePoint data source\.

Amazon Kendra currently supports SharePoint Cloud and SharePoint Server \(2013, 2016, 2019, and Subscription Edition\)\.

**Note**  
Support for SharePoint Connector v1\.0 / SharePointConfiguration API is scheduled to end by June 2023\. We recommend using SharePoint Connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra SharePoint data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-v2-sharepoint)
+ [Prerequisites](#prerequisites-v2-sharepoint)
+ [Connection instructions](#data-source-procedure-v2-sharepoint)
+ [Notes](#sharepoint-notes)

## Supported features<a name="supported-features-v2-sharepoint"></a>

Amazon Kendra SharePoint data source connector supports the following features:
+ Field mappings
+ Identity crawling
+ User context filtering
+ Virtual private cloud \(VPC\)
+ Inclusion/exclusion patterns
+ Full sync/New or modified content sync/New, modified, or deleted content sync

## Prerequisites<a name="prerequisites-v2-sharepoint"></a>

Before you can use Amazon Kendra to index your SharePoint data source, make these changes in your SharePoint and AWS accounts\.

**In SharePoint Online, make sure you have:**
+ Copied your SharePoint instance URLs\. The format for the host URL you enter is *https://yourcompany\.sharepoint\.com/sites/mysite*\. Your URL must start with `https`\.
+ Copied the domain name of your SharePoint instance URL\.
+ Noted your basic authentication credentials containing the user name and password you use to connect to SharePoint Online\.
+ **Optional:** Configured an OAuth 2\.0 credential token that can identify Amazon Kendra containing a user name \(SharePoint account user name\), a password \(SharePoint account password\), a client ID \(a SharePoint generated unique ID used by Amazon Kendra to request an access token\), and a client secret \(a shared secret string used by both the SharePoint instance and Amazon Kendra to authorize communications\)\.
+ **If using OAuth 2\.0 authentication:** Copied the tenant ID of your SharePoint instance\.
+ Activated admin consent from a tenant and then added the following API permissions in your Azure Portal for SharePoint Online:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/data-source-v2-sharepoint.html)

  For more information on adding API permissions in the Azure portal, see [Quickstart: Configure a client application to access a web API](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-configure-app-access-web-apis)\.
**Note**  
Sites\.FullControl\.All permission is required for Amazon Kendra to crawl entities and user permissions \(ACL\) for SharePoint Online\. If Sites\.FullControl\.All is not provided for OAuth 2\.0 authentication:  
comments, attachments, and OneNote documents will be crawled without ACL details\.
documents, pages, events, and links will not be crawled from either main sites or subsites\.

**In SharePoint Server, make sure you have:**
+ Copied your SharePoint instance URLs and the domain name of your SharePoint URLs\. The format for the host URL you enter is *https://yourcompany\.sharepoint\.com/sites/mysite*\. Your URL must start with `https`\.
+ If using **Email ID with Domain from IDP** for access control:
  + Copied your SharePoint Server LDAP\.
  + Noted your custom email domain value—for example: *"amazon\.com"*\.
+ If using **Email ID with Domain from IDP** authorization, copied your:
  + LDAP Server Endpoint \(endpoint of LDAP server including protocol and port number\)\. For example: *ldap://example\.com:389*\.
  + LDAP Search Base \(search base of the LDAP user\)\. For example: *CN=Users,DC=sharepoint,DC=com*\.
  + LDAP user name and LDAP password\.
+ Either configured NTLM authentication credentials **or** configured Kerberos authentication credentials containing a user name \(SharePoint account user name\) and password \(SharePoint account password\)\.

**In your AWS account, make sure you have:**
+ [Created an Amazon Kendra index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html) and, if using the API, noted the index ID\.
+ [Created an IAM role](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds) for your data source and, if using the API, noted the ARN of the IAM role\.
+ \(For SharePoint Server only\) Stored an SSL certificate in an Amazon S3 bucket\.
+ Stored your SharePoint authentication credentials in an AWS Secrets Manager secret and, if using the API, noted the ARN of the secret\.
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.

If you don’t have an existing IAM role or secret, you can use the console to create a new IAM role and Secrets Manager secret when you connect your SharePoint data source to Amazon Kendra\. If you are using the API, you must provide the ARN of an existing IAM role and Secrets Manager secret, and an index ID\.

## Connection instructions<a name="data-source-procedure-v2-sharepoint"></a>

To connect Amazon Kendra to your SharePoint data source, you must provide details of your SharePoint credentials so that Amazon Kendra can access your data\. If you have not yet configured SharePoint for Amazon Kendra see [Prerequisites](#prerequisites-v2-sharepoint)\.

### <a name="sharepoint-v2-adding-procedure-online"></a>

------
#### [ Console: SharePoint Online ]

**To connect Amazon Kendra to SharePoint Online** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **SharePoint Connector v2\.0**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. In **Source**, for **Hosting Method**—Choose **SharePoint Online**\.

   1. **Site URLs specific to your SharePoint repository**—Enter the SharePoint host URLs\. The format for the host URLs you enter is *https://yourcompany\.sharepoint\.com/sites/mysite*\. The URL must start with `https` protocol\. Separate URLs with a new line\. You can add up to 100 URLs\.

   1. **Domain**—Enter the SharePoint domain\.

   1. For **Authentication**, choose between **Basic authentication** and **Oauth 2\.0 authentication** based on your use case\.

      1.  If using **Basic Authentication**, enter the following information:
         + For **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your SharePoint authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. Enter the following information in the window:
           + **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-SharePoint\-’ is automatically added to your secret name\.
           +  **Username**—User name for your SharePoint account\.
           + **Password**—Password for your SharePoint account\.

      1.  If using **OAuth 2\.0 authentication**, enter the following information:
         + **Tenant ID**—Tenant ID of your SharePoint account\.
         + For **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your SharePoint authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\. Enter the following information in the window:
           + **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-SharePoint\-’ is automatically added to your secret name\.
           + **Username**—User name for your SharePoint account\.
           + **Password**—Password for your SharePoint account\.
           + **Client ID**—The SharePoint auto\-generated unique ID used by Amazon Kendra to request an access token\.
           + **Client secret**—Shared secret string used by both the SharePoint instance and Amazon Kendra to authorize communications\.

   1.  **Identity crawler**—Choose to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\.
**Note**  
**Identity Crawler** is available to **OAuth 2\.0 authentication** users only\.

      You can also choose to:

      1. **Crawl Local Group Mapping**—Activate to crawl local group mapping\.

      1. **Crawl AD Group Mapping**—Activate to crawl Azure Active Directory group mapping\.

   1. \(Optional\) **Configure VPC and security group**—Select a VPC to use with your SharePoint instance\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. In **Sync scope**, choose from the following options :

      1. **Select entities**—Choose the entities you want to crawl\. You can select to crawl **All** entities or any combination of **Files**, **Attachments**, **Links** **Pages**, **Events**, **Comments**, and **List Data**\.

      1. In **Additional configuration**, for **Entity regex patterns**—Add regular expression patterns for **Links**, **Pages**, and **Events** to include specific entities instead of syncing all your documents\.

      1. **Regex patterns**—Add regular expression patterns to include or exclude files by **File path** **File name** **File type**, **OneNote section name**, and **OneNote page name** instead of syncing all your documents\. You can add up to 100\.

   1. For **Sync mode** choose how you want to update your index when your data source content changes\. When you sync your data source with Amazon Kendra for the first time, all content is synced by default\.
      + **Full sync**—Sync all content regardless of the previous sync status\.
      + **New or modified documents sync**—Sync only new or modified documents\.
      + **New, modified, or deleted documents sync**—Sync only new, modified, and deleted documents\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Events** **Pages**, **Files**, **Links**, **Attachments**, and **Comments**—Select from the Amazon Kendra generated default data source fields that you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ Console: SharePoint Server ]

**To connect Amazon Kendra to SharePoint** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.

1. On the **Add data source** page, choose **SharePoint Connector v2\.0**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. In **Name and description**, for **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. In **Language**, for **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. In **Tags**, for **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. In **Source**, for **Hosting Method**—Choose **SharePoint Server**\.

   1. **Choose SharePoint Version**—Choose between **SharePoint 2013**, **SharePoint 2016**, **SharePoint 2019**, and **SharePoint \(Subscription Edition\)**\.

   1. **Site URLs specific to your SharePoint repository**—Enter the SharePoint host URLs\. The format for the host URLs you enter is *https://yourcompany\.sharepoint\.com/sites/mysite*\. The URL must start with `https` protocol\. Separate URLs with a new line\. You can add up to 100 URLs\.

   1. **Domain**—Enter the SharePoint domain\.

   1. **SSL certificate location**—Enter the Amazon S3 path to your SSL certificate file\.

   1. \(Optional\) For **Web proxy**—Enter the host name \(without the `http://` or `https://` protocol\), and the port number used by the host URL transport protocol\. The numeric value of the port number must be between 0 and 65535\.

   1. For **Authorization**—Choose from the following access control/context filtering options:

      1. **Email ID with Domain from IDP**—Access control will be based on email ids extracted from email domains fetched from the underlying identity provider \(IDP\)\. You provide the IDP connection details in your Secrets Manager secret during **Authentication**\.

      1. **Email ID with Custom Domain**—Access control will be based on email IDs\. You want to provide the email domain value\. For example, *"amazon\.com"*\. The email domain will be used to construct the email ID for access control\. You must enter your email domain using **Add Email Domain**\.

      1. **Domain/User with Domain**—Access control will be structured using a Domain/User ID format\. You need to provide a valid Domain name\. For example: *"sharepoint2019"* to construct access control\.

   1. For **Authentication**, choose between **NTLM authentication** and **Kerberos authentication** based on your use case\. Enter the following information for your chosen authentication option \(for both **NTLM authentication** or **Kerberos authentication**\):

      1. For **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your SharePoint authentication credentials\. If you choose to create a new secret, an AWS Secrets Manager secret window opens\. Enter the following information in the window:
        + **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-SharePoint\-’ is automatically added to your secret name\.
        +  **Username**—User name for your SharePoint account\.
        + **Password**—Password for your SharePoint account\.
        + If using **Email ID with Domain from IDP**, also enter your:
          +  **LDAP Server Endpoint**—Endpoint of LDAP server, including protocol and port number\. For example: *ldap://example\.com:389*\.
          + **LDAP Search Base**—Search base of LDAP user\. For example: *CN=Users,DC=sharepoint,DC=com*\.
          + **LDAP username**—Your LDAP user name\.
          + **LDAP Password**—Your LDAP password\.

   1. **Identity crawler**—Choose to enable Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. You can also choose to:

      1. **Crawl Local Group Mapping**—Activate to crawl local group mapping\.

      1. \(For **Email ID with Domain from IDP** only\)**Crawl AD Group Mapping**—Activate to crawl Active Directory mapping\.

   1. \(Optional\) **Configure VPC and security group**—Select a VPC to use with your SharePoint instance\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. In **Sync scope**, choose from the following options :

      1. **Select entities**—Choose the entities you want to crawl\. You can select to crawl **All** entities or any combination of **Files**, **Attachments**, **Links** **Pages**, **Events**, **Comments**, and **List Data**\.

      1. In **Additional configuration**, for **Entity regex patterns**—Add regular expression patterns for **Links**, **Pages**, and **Events** to include specific entities instead of syncing all your documents\.

      1. **Regex patterns**—Add regular expression patterns to include or exclude files by **File path** **File name** **File type**, **OneNote section name**, and **OneNote page name** instead of syncing all your documents\. You can add up to 100\.

   1. For **Sync mode** choose how you want to update your index when your data source content changes\. When you sync your data source with Amazon Kendra for the first time, all content is synced by default\.
      + **Full sync**—Sync all content regardless of the previous sync status\.
      + **New or modified documents sync**—Sync only new and modified documents\.
      + **New, modified, or deleted documents sync**—Sync only new, modified, and deleted documents\.

   1. In **Sync run schedule**, for **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Events** **Pages**, **Files**, **Links**, **Attachments**, and **Comments**—Select from the Amazon Kendra generated default data source fields that you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. You can also choose to edit your information from this page\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ API ]

**To connect Amazon Kendra to SharePoint**

You must specify a JSON of the [data source schema](https://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) using the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API\. You must provide the following information:
+ **Repository Endpoint Metadata**—Specify the `tenantID` `domain` and `siteUrls` of your SharePoint instance\.
+ **Repository Additional Properties**—Specify the:
  + \(For SharePoint Server only\) `S3bucketName` and `s3certificateName` you used to store your SSL certificate\.
  + Authentication type \(`auth_Type`\) you are using, whether `OAuth2`, `OAuth2Certificate`, `Basic`, `NTLM`, or `Kerberos`\.
  + Version \(`version`\) you are using, whether `Server` or `Online`\. If you use `Server` you can futher specify the `onPremVersion` as `2013`, `2016`, `2019`, or `Subsc`\.
+ **Type**—Specify `TEMPLATE` as the Type when you call `CreateDataSource`\.
+ **Data source**—Specify the data source as `SHAREPOINTV2`\. 
+ **Secret Amazon Resource Name \(ARN\)**—Provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your SharePoint account\.

  If you use SharePoint Online, you can choose between basic authentication and OAuth 2\.0 authentication\. The following are the minimum JSON structure that must be in your secret for each authentication option:
  + **Basic authentication**

    ```
    {
        "username": " SharePoint account user name",
        "password": "SharePoint account password"
    }
    ```
  + **OAuth 2\.0 authentication**

    ```
    {
        "clientId": "SharePoint generated client id",
        "clientSecret": "SharePoint client secret",
        "userName": "SharePoint account user name",
        "password": "SharePoint account password"
    }
    ```

  If you use SharePoint Server, you can choose between NTLM and Kerberos authentication\. The following are the minimum JSON structure that must be in your secret for each authentication option:
  + **NTLM authentication **

    ```
    {
        "username": "SharePoint account user name",
        "password": "SharePoint account password"
    }
    ```
  + **NTLM authentication with **Email ID with Domain from IDP** authorization**

    ```
    {
        "userName": "SharePoint account user name",
        "password": "SharePoint account password",
        "ldapUrl": "ldap://example.com:389",
        "baseDn": "CN=Users,DC=sharepoint,DC=com",
        "ldapUser": "LDAP account user name",
        "ldapPassword": "LDAP account password"
    }
    ```
  + **Kerberos authentication**

    ```
    {
        "username": "SharePoint account user name",
        "password": "SharePoint account password"
    }
    ```
  + **Kerberos authentication with **Email ID with Domain from IDP** authorization**

    ```
    {
        "userName": "SharePoint account user name",
        "password": "SharePoint password",
        "ldapUrl": "ldap://example.com:389",
        "baseDn": "CN=Users,DC=sharepoint,DC=com",
        "ldapUser": "LDAP account user name",
        "ldapPassword": "LDAP account password"
    }
    ```
**Note**  
Be sure to regularly refresh or rotate your credentials and secret\. Provide only the necessary access level for your own security\. Re\-using credentials and secrets across data sources, and connector versions v1\.0 and v2\.0 \(where applicable\), is not recommended\.
+ **Sync mode**—Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between:
  + `FORCED_FULL_CRAWL` to crawl and sync all content to your index
  + `FULL_CRAWL` to crawl all content and sync only new, modified, or deleted content
  + `CHANGE_LOG` to crawl and sync only new and modified content\.
+ **Enable identity crawler**—Specify whether to activate identity crawler\. If identity crawler is deactivated, you must upload the principal information using the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API\.
+ **IAM role**—Specify `RoleArn` when you call `CreateDataSource` to provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the SharePoint connector and Amazon Kendra\. For more information, see [IAM roles for SharePoint data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Specific documents to index**—You can use a SharePoint query to specify the documents you want from one or more knowledge bases, including private knowledge bases\. Access to the knowledge bases is determined by the user that you use to connect to the SharePoint instance\. For more information, see [Specifying documents to index with a query](https://docs.aws.amazon.com/kendra/latest/dg/servicenow-query.html)\.
+  **Inclusion and exclusion filters**—You can specify whether to include knowledge articles, service catalogs, incidents and their attachments\.
**Note**  
Most data sources use regular expression patterns, which are inclusion or exclusion patterns referred to as filters\. If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Field mappings**—Choose to map your SharePoint data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.
+  **Virtual Private Cloud \(VPC\)**—Specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.

For a list of other important JSON keys to configure, see [Microsoft SharePoint template schema](ds-schemas.md#ds-schema-sharepoint)\.

------

## Notes<a name="sharepoint-notes"></a>
+ The connector supports custom field mappings only for the **Files** entity\.
+ For all SharePoint Server versions, the ACL token must be in lower case\. For **Email with Domain from IDP** and **Email ID with Custom Domain** ACL, for example: *user@sharepoint2019\.com*\. For **Domain/User with Domain** ACL, for example: *sharepoint2013\\user*\.
+ The connector does not support change log mode/**New or modified content sync** for SharePoint 2013\.
+ If an entity name has a `%` character in its name, the connector will skip these files due to API limitations\.
+ OneNote can only be crawled by the connector using a Tenant ID and with OAuth 2\.0 authentication activated\.
+ The connector crawls the first section of a OneNote document using its default name only, even if the document is renamed\.
+ The connector crawls links in SharePoint 2019, SharePoint Online, and Subscription Edition, only if **Pages** and **Files** are selected as entities to be crawled in addition to **Links**\.
+ The connector crawls links in SharePoint 2013 and SharePoint 2016 if **Links** is selected as an entity to be crawled\.
+ The connector crawls list attachments and comments only when **List Data** is also selected as an entity to be crawled\.
+ The connector crawls event attachments only when **Events** is also selected as an entity to be crawled\.