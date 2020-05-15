--------

--------

# Using a Microsoft SharePoint data source<a name="data-source-sharepoint"></a>

You can use your Microsoft SharePoint Online site as a data source for Amazon Kendra\. When you use Amazon Kendra to index your site, you choose which SharePoint URLs to include in the index, and you specify inclusion and exclusion patterns for the documents stored on those URLs\.

Amazon Kendra requires credentials to access the SharePoint site\. The SharePoint user must have administrative permission to the SharePoint sites that you want to index\. If you are using the console to create your data source, you can enter the credentials there or you can choose an existing AWS Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The secret must contain the user name and password that Amazon Kendra uses to access the SharePoint site in a JSON structure\. The following is the minimum JSON structure that must be in the secret:

```
{
    "username": "user name",
    "password": "password"
}
```

The data source IAM role must have permission to access the secret\. For more information, see [IAM roles for Microsoft SharePoint Online data sources](iam-roles.md#iam-roles-ds-spo)\.

The secret can contain more information, however, Amazon Kendra ignores other fields\. For more information, see [ What Is AWS Secrets Manager ](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the *AWS Secrets Manager User Guide*\.

You must create an index before you create the SharePoint data source\. For more information, see [Creating an index](create-index.md)\. You provide the ID of the index when you create the data source\.

You specify connection and other information in the console or using an instance of the [SharePointConfiguration](API_SharePointConfiguration.md) data type\. You must provide the following information: 
+ The credentials required to log in to the SharePoint site\.
+ The URLs of the SharePoint site, SharePoint site collection, or SharePoint list to index\.
+ The ARN of an IAM role that has permission to run Amazon Kendra commands\. For the required permissions, see [IAM roles for Microsoft SharePoint Online data sources](iam-roles.md#iam-roles-ds-spo)\.

You can optionally provide the following information:
+ Whether Amazon Kendra should index the contents of attachments to SharePoint list items\.
+ An inclusion pattern to specify the documents that should be included in the index\. If you specify an inclusion pattern, any document that does not match the pattern will not be indexed\.
+ An exclusion pattern to specify the documents that should be excluded from the index\. If you specify an exclusion pattern, any document that does not match the pattern will be indexed\. If you specify both and inclusion and an exclusion pattern, documents that match the exclusion pattern will not be indexed even if they match the inclusion pattern\.
+ Whether Amazon Kendra should use the SharePoint change log mechanism to determine if a document needs to updated in the index\. You should use the change log if you don't want Amazon Kendra to scan all of the documents in the site to update the index\. If your change log is large, it may take Amazon Kendra less time to scan the site than to process the change log\.
+ Field mappings that map attributes from your SharePoint site to Amazon Kendra index fields\. For more information, see [Mapping data source fields](field-mapping.md)\.