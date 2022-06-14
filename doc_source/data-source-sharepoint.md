--------

--------

# Using a Microsoft SharePoint data source<a name="data-source-sharepoint"></a>

You can use your Microsoft SharePoint as a data source for Amazon Kendra\. To use SharePoint in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add SharePoint\.

Amazon Kendra currently supports SharePoint Online and SharePoint Server \(versions 2013 and 2016\)\.

When you connect to SharePoint to index your documents, you specify which SharePoint URLs to include in the index\. You can specify regular expression patterns to include or exclude specific documents in your SharePoint\.

You must create an index before you create the SharePoint data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to SharePoint, you specify the connection and other information in the console or by using the [SharePointConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SharePointConfiguration.html) object\. You provide the site URLs in SharePoint you want to index\.

Before you can index your documents from your SharePoint, you must be a SharePoint user with administrative permissions\. For SharePoint lists, you must have the following permissions:
+ Open Items – View the source of documents with server\-side file handlers\.
+ View Application Pages – View forms, views and application pages\. E, an enumerate lists\.
+ View Items – View items in lists and documents in document libraries\.
+ View Versions – View past versions of a list item or document\.

For SharePoint websites, you must have the following permissions:
+ Browse Directories – Enumerate files and folders in a website using SharePoint Designer and Web DAV interfaces\.
+ Browse User Information – View information about users of the website\.
+ Enumerate Permissions – Enumerate permissions on the website, list, folder, document, or list item\.
+ Open – Open a website, list, or folder to access items inside the container\.
+ Use Client Integration Features – Use SOAP, WebDAV, the client object model, or SharePoint Designer interfaces to access the website\.
+ Use Remote Interfaces – Use features that launch client applications\.
+ View Pages – View pages on a website\.

You must specify the version of SharePoint you use when configuring SharePoint\. This is the case no matter if you use SharePoint Server 2013, SharePoint Server 2016, or SharePoint Online\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your AWS Secrets Manager secret, which stores your SharePoint authentication credentials, and the AWS Key Management Service key used to decrypt it\. You provide the ARN of an IAM role using [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. For more information about permissions, see [IAM roles for Microsoft SharePoint data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your SharePoint\. You store your SharePoint credentials in an AWS Secrets Manager secret\. If you use SharePoint Online, you only need to provide your user name and password in your secret\. If you use SharePoint Server, in addition to your user name and password, provide the server domain name\. The server domain name is the NetBIOS name in your Active Directory provider\. If you use the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or, you can use an existing Secrets Manager secret\. If you use the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

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

Amazon Kendra also crawls user and group information from the SharePoint instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for SharePoint data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-sharepoint-online)\.

If you use SharePoint Server and need to convert your Access Control List \(ACL\) to email format for filtering on user context, provide the LDAP server URL and LDAP search base, or use the directory domain override\. The LDAP server URL is the full domain name and the port number \(for example, *ldap://example\.com:389*\)\. The LDAP search base are the domain controllers 'example' and 'com'\. With the directory domain override, you can use the email domain instead of using LDAP server URL and LDAP search base\. For example, the email domain for *username@example\.com* is 'example\.com'\. You can use this override if you aren't concerned about validating your domain and simply want to use your email domain\.

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

You also can add the following optional information:
+ Whether Amazon Kendra should index the contents of attachments to SharePoint list items\.
+ Whether Amazon Kendra should use the SharePoint change log mechanism to determine if a document must be updated in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in SharePoint than to process the change log\. If you're syncing your SharePoint data source with your index for the first time, all documents are scanned\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any document with a file name or file type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your SharePoint fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](field-mapping.md)\.