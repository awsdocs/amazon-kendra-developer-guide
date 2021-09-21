--------

--------

# Using a Microsoft SharePoint data source<a name="data-source-sharepoint"></a>

You can use your Microsoft SharePoint as a data source for Amazon Kendra\. When you use Amazon Kendra to index your site, you choose which SharePoint URLs to include in the index, and you specify inclusion and exclusion patterns for the documents stored on those URLs\.

Amazon Kendra currently supports SharePoint Online and SharePoint Server \(versions 2013 and 2016\)\.

Amazon Kendra requires authentication credentials to access the SharePoint site\. If you are using the console to create your data source, you can enter the credentials there or you can choose an existing AWS Secrets Manager secret that stores your credentials\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. For more information, see [ What Is AWS Secrets Manager ](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the *AWS Secrets Manager User Guide*\.

If you use SharePoint Online, you only need to provide your user name and password in your secret\.

If you use SharePoint Server, in addition to your user name and password, you need to provide the server domain name\. The server domain name is the NetBIOS name in your active directory provider\.

If you use SharePoint Server and need to convert your access control list \(ACL\) to email format for filtering on user context, you need to provide the LDAP server URL and LDAP search base, or use the directory domain override\. The LDAP server URL is the full domain name and the port number\. For example, 'ldap://example\.com:389'\. The LDAP search base are the domain controllers 'example' and 'com'\. The directory domain override allows you to use the email domain instead of using LDAP server URL and LDAP search base\. For example, the email domain for 'username@example\.com' is 'example\.com'\. You can use this override if you are not concerned about validating your domain and simply want to use your email domain\.

Amazon Kendra uses the credential information stored in your secret to access the SharePoint site in a JSON structure\.

If you use SharePoint Online, the following is the minimum JSON structure that must be in your secret:

```
{ 
        "username": "user name", 
        "password": "password"
}
```

The secret can contain more information, however, Amazon Kendra ignores other fields\.

If you use SharePoint Server, the following is the minimum JSON structure that must be in your secret:

```
{
        "username": "user name", 
        "password": "password", 
        "domain": "server domain name"
}
```

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

The SharePoint user must have administrative permission to the SharePoint sites that you want to index\. For SharePoint lists, the user must have the following permissions:
+ Open Items – View the source of documents with server\-side file handlers\.
+ View Application Pages – View forms, views and application pages\. Enumerate lists
+ View Items – View items in lists and documents in document libraries
+ View Versions – View past versions of a list item or document\.

For SharePoint websites, the user must have the following permissions:
+ Browse Directories – Enumerate files and folders in a website using SharePoint Designer and Web DAV interfaces\.
+ Browse User Information – View information about users of the website\.
+ Enumerate Permissions – Enumerate permissions on the website, list, folder, document, or list item\.
+ Open – Open a website, list, or folder to access items inside the container\.
+ Use Client Integration Features – Use SOAP, WebDAV, the client object model, or SharePoint Designer interfaces to access the website\.
+ Use Remote Interfaces – Use features that launch client applications\.
+ View Pages – View pages on a website\.

The data source IAM role must have permission to access the secret\. For more information, see [IAM roles for Microsoft SharePoint data sources](iam-roles.md#iam-roles-ds-spo)\.

You must create an index before you create the SharePoint data source\. For more information, see [Creating an index](create-index.md)\. You provide the ID of the index when you create the data source\.

You specify connection and other information in the console or using an instance of the [ SharePointConfiguration ](API_SharePointConfiguration.md) data type\. You must provide the following information: 
+ The credentials required to log in to the SharePoint site\.
+ The URLs of the SharePoint site, SharePoint site collection, or SharePoint list to index\.
+ The ARN of an IAM role that has permission to run Amazon Kendra commands\. For the required permissions, see [IAM roles for Microsoft SharePoint data sources](iam-roles.md#iam-roles-ds-spo)\.

You can optionally provide the following information:
+ Whether Amazon Kendra should index the contents of attachments to SharePoint list items\.
+ An inclusion pattern to specify the documents that should be included in the index\. If you specify an inclusion pattern, any document that does not match the pattern is not indexed\.
+ An exclusion pattern to specify the documents that should be excluded from the index\. If you specify an exclusion pattern, any document that does not match the pattern will be indexed\. If you specify both and inclusion and an exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Whether Amazon Kendra should use the SharePoint change log mechanism to determine if a document needs to be updated in the index\. You should use the change log if you don't want Amazon Kendra to scan all of the documents in the site to update the index\. If your change log is large, it may take Amazon Kendra less time to scan the site than to process the change log\.
+ Field mappings that map attributes from your SharePoint site to Amazon Kendra index fields\. For more information, see [Mapping data source fields](field-mapping.md)\.