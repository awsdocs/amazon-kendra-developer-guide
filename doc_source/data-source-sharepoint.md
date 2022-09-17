--------

--------

# Using a Microsoft SharePoint data source<a name="data-source-sharepoint"></a>

You can use your Microsoft SharePoint as a data source for Amazon Kendra\. To use SharePoint in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add SharePoint\.

For troubleshooting the Amazon Kendra SharePoint data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

Amazon Kendra currently supports SharePoint Online and SharePoint Server \(versions 2013, 2016, and 2019\)\.

You must create an index before you create the SharePoint data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

Before you can index your documents from your SharePoint, you must be a SharePoint user with administrative permissions\. For SharePoint lists, you must have the following permissions:
+ Open Items—View the source of documents with server\-side file handlers\.
+ View Application Pages – View forms, views, and application pages\. Enumerate lists\.
+ View Items—View items in lists and documents in document libraries\.
+ View Versions—View past versions of a list item or document\.

For SharePoint websites, you must have the following permissions:
+ Browse Directories—Enumerate files and folders in a website using SharePoint Designer and Web DAV interfaces\.
+ Browse User Information—View information about users of the website\.
+ Enumerate Permissions—Enumerate permissions on the website, list, folder, document, or list item\.
+ Open—Open a website, list, or folder to access items inside the container\.
+ Use Client Integration Features—Use SOAP, WebDAV, the client object model, or SharePoint Designer interfaces to access the website\.
+ Use Remote Interfaces—Use features that launch client applications\.
+ View Pages—View pages on a website\.

You must also use an Amazon Virtual Private Cloud if you use SharePoint Server\.

When you connect to SharePoint to index your documents, you specify which SharePoint URLs to include in the index\. You can specify regular expression patterns to include or exclude specific documents in your SharePoint\.

To connect to SharePoint, you specify the connection and other information in the console or by using the [SharePointConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SharePointConfiguration.html) object\. You provide the site URLs in SharePoint you want to index\.

You must specify the version of SharePoint you use when configuring SharePoint\. This is the case no matter if you use SharePoint Server 2013, SharePoint Server 2016, SharePoint Server 2019, or SharePoint Online\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your AWS Secrets Manager secret\. The secret stores your SharePoint authentication credentials, and the AWS Key Management Service key used to decrypt it\. You provide the ARN of an IAM role using [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. For more information about permissions, see [IAM roles for Microsoft SharePoint data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your SharePoint instance\. See [Authentication](#sharepoint-authentication)\.

Amazon Kendra also crawls user and group information from the SharePoint instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for SharePoint data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-sharepoint-online)\.

You also can add the following optional information:
+ Whether Amazon Kendra should index the contents of attachments to SharePoint list items\.
+ Whether to connect to your Microsoft SharePoint site URLs via a web proxy\. You can use this option for SharePoint Server\.
+ Whether Amazon Kendra should use the SharePoint change log mechanism to determine if a document must be added, updated, or deleted in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in SharePoint than to process the change log\. If you're syncing your SharePoint data source with your index for the first time, all documents are scanned\.
+ Inclusion or exclusion patterns: If you specify an inclusion pattern, only content that matches the inclusion pattern is indexed\. Any document with a file name or file type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your SharePoint fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](field-mapping.md)\.

## Authentication<a name="sharepoint-authentication"></a>

There are two types of authentication that you can use with Microsoft SharePoint\. The first, basic authentication, permits Amazon Kendra to connect to the SharePoint instance using a user name and password\.

The second, OAuth, uses the OAuth 2\.0 authentication specification to identify Amazon Kendra and a user name and password\. You can use OAuth authentication for SharePoint Online\.

You must have administrative permissions to the SharePoint instance, whether you use basic authentication or OAuth authentication\.

It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.

### Basic authentication<a name="sharepoint-auth-basic"></a>

When you use basic authentication, you provide the user name and password of an administrator of your SharePoint instance\. Amazon Kendra uses these credentials to connect to SharePoint\.

You store your user name and password in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

If you use SharePoint Online, you only need to provide your user name and password in your secret\. If you use SharePoint Server, in addition to your user name and password, provide the server domain name\. The server domain name is the NetBIOS name in your Active Directory provider\.

The basic credentials are stored as a JSON string in the Secrets Manager secret\.

If you use SharePoint Online, the following is the minimum JSON structure that must be in your secret:

```
{
    "username": "user name",
    "password": "password"
}
```

If you use SharePoint Server, the following is the minimum JSON structure that must be in your secret:

```
{
    "username": "user name",
    "password": "password",
    "domain": "server domain name"
}
```

If you use SharePoint Server and need to convert your Access Control List \(ACL\) to email format for filtering on user context, provide the LDAP server URL and LDAP search base\. Or you can use the directory domain override\. The LDAP server URL is the full domain name and the port number \(for example, *ldap://example\.com:389*\)\. The LDAP search base are the domain controllers 'example' and 'com'\. With the directory domain override, you can use the email domain instead of using LDAP server URL and LDAP search base\. For example, the email domain for *username@example\.com* is 'example\.com'\. You can use this override if you aren't concerned about validating your domain and simply want to use your email domain\.

You can include the LDAP server URL and LDAP search base in your secret for SharePoint Server using the following JSON structure:

```
{
    "username": "user name",
    "password": "password",
    "domain": "server domain name",
    "ldapServerUrl": "ldap://example.com:389",
    "ldapSearchBase": "dc=example,dc=com",
    "directoryDomainOverride": "example.com"
}
```

### OAuth authentication<a name="sharepoint-auth-oauth"></a>

When you use OAuth authentication to connect to Microsoft SharePoint, you provide the client ID and secret that identifies Amazon Kendra to SharePoint Online\. You also provide a user name and password that is used to access your SharePoint instance\.

You store your client ID, client secret, user name, and password in an AWS Secrets Manager secret\. You generate the client ID and client secret in SharePoint\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The OAuth credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "user name",
    "password": "password",
    "clientId": "client id",
    "clientSecret": "client secret"
}
```

#### Generating the client ID and secret<a name="sharepoint-generate-oauth"></a>

**To create a SharePoint Online client ID and secret**

1. Log in to the Azure portal desktop application\. You must be a user with administrative permissions\.

1. Select **Azure Active Directory** in the side navigation menu\.

1. Select **App registrations** in the side navigation menu, then select **New registration**\.

1. Enter a name for your app\. For example, *kendra\_sharepoint\_app*\. You can default to only giving access to accounts in the organizational directory\. You don't need to provide a redirect URI\. Select **Register**\.

1. You are directed to the app's **Overview** page, or you can go to this page by selecting **Overview** from the side navigation menu\. Copy the **Application \(client\) ID**\. You'll need this when you create the Secrets Manager secret for the SharePoint data source\.

1. Select **Certificates & secrets** from the side navigation menu, then select **New client secret**\.

1. Enter a description and choose an expiration date option\. Select **Add**\.

1. Copy the secret\. You'll need this when you create the Secrets Manager secret for the SharePoint data source\.

1. You must grant permissions to use your app\. Only admin users can grant permissions\. Select **API permissions** from the side navigation menu, then select **Add a permission**\.

1. Choose the **SharePoint** option, then choose **Delegated permissions**\. You must choose the option for full control of all sites \(admin consent is required by default\)\. Select **Add permissions**\.