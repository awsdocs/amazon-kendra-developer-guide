--------

--------

# Using an Amazon FSx data source<a name="data-source-fsx"></a>

You can use your Amazon FSx file system as a data source for Amazon Kendra\. To use Amazon FSx in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Amazon FSx\.

Amazon Kendra currently only supports Amazon FSx for Windows File Server\.

When you connect to Amazon FSx to index your documents, you specify the Amazon FSx file system ID\. You can specify regular expression patterns to include or exclude specific documents in your Amazon FSx file system\.

You must create an index before you create the Amazon FSx data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Amazon FSx, you specify the connection and other information in the console or by using the [FsxConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_FsxConfiguration.html) object\. You provide the file system ID of the Amazon FSx you want to index\.

Before you can index your documents from your Amazon FSx file system, you must create an Amazon FSx file system with read and mounting permissions\. You must also use an Amazon Virtual Private Cloud \(VPC\) where your Amazon FSx resides\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Amazon FSx file system\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Amazon FSx data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Amazon FSx file system\. You store your Amazon FSx credentials in an AWS Secrets Manager secret\. The credentials are a user name and password for an Active Directory user account with read and mounting access to the Amazon FSx file system for Windows\. You must include the Active Directory user name, along with the Domain Name System \(DNS\) domain name\. For example, *user@corp\.example\.com*\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
"username": "user@corp.example.com",
"password": "password"
}
```

Amazon Kendra also crawls user and group information from the Amazon FSx instance\. You must have administrative permissions of the Active Directory domain\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Amazon FSx data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-fsx)\.

To test user context filtering on a user, you must include the DNS domain name as part of the user name when you issue the query\. You can also test user context filtering on a group name\. You must only use lowercase characters for the user name or group name, despite if Active Directory uses upper case characters\. For example, if the Active Directory user is *Admin* and the DNS is *corp\.example\.com*, the user name to test user context filtering in Amazon Kendra should be *admin@corp\.example\.com*\. If the Active Directory group is *Management*, the group name to test user context filtering in Amazon Kendra should be *management*\.

You also can add the following optional information:
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any document with a file name or file type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Amazon FSx fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.