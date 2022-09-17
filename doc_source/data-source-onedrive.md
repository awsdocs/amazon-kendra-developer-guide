--------

--------

# Using a Microsoft OneDrive data source<a name="data-source-onedrive"></a>

You can use your Microsoft OneDrive as a data source for Amazon Kendra\. To use OneDrive in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add OneDrive\.

For troubleshooting your Amazon Kendra Microsoft OneDrive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

You must create an index before you create the OneDrive data source\. For information, see [Creating an index](create-index.md)\. You provide the ID of the index when you create the data source\.

When you connect to OneDrive to index your documents, you choose the users whose documents should be indexed\. You also specify the Azure Active Directory domain of the organization\. You can specify regular expression patterns to include or exclude specific documents in your OneDrive\.

To connect to OneDrive, you specify connection and other information in the console or by using the [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_OneDriveConfiguration.html) object\. You provide the tenant domain that contains the OneDrive site\. You also provide a list of users whose documents should be indexed\. You can provide a list of user names, or you can provide the user names in a file stored in an S3 bucket\. If you store the list of user names in an S3 bucket, the IAM policy for the data source must provide access to the bucket and access to the key that the bucket was encrypted with, if any\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your OneDrive site\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for OneDrive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your OneDrive site\. You store your OneDrive credentials in an AWS Secrets Manager secret\. The credentials are Azure Active Directory \(AD\) application ID and secret key\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

You must create an AD application for your credentials\. You must grant the application the following permissions on the Microsoft Graph option:
+ Read files in all site collections \(File\.Read\.All\)
+ Read all users' full profile \(User\.Read\.All\)
+ Read directory data \(Directory\.Read\.All\)
+ Read all groups \(Group\.Read\.All\)
+ Read items in all site collections \(Site\.Read\.All\)

When you create the AD application, it is assigned an application ID\. You must use the AD site to register a secret key for the application\. Amazon Kendra uses the ID and key as credentials to authenticate when it connects to the OneDrive site\.

The authentication credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "username": "application ID",
    "password": "secret key"
}
```

After you create a data source, you can:
+ Modify the list of users\.
+ Change from a list of users to a list stored in an S3 bucket\.
+ Change the S3 bucket location of a list of users\. If you change the bucket location, you must also update the IAM role for the data source so that it has access to the bucket\.
+ Change the content of a user list stored in an S3 bucket\.

You also can add the following optional information:
+ Inclusion or exclusion patterns: If you specify an inclusion pattern, only content that matches the inclusion pattern is indexed\. Any file name or type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, files that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your OneDrive fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

After you sync the data source, you can't change the inclusion and exclusion patterns or the remove field mapping\. You can map additional fields\.

The following table shows the OneDrive properties that can be mapped to a suggested Amazon Kendra index field\.


| OneDrive field name | Suggested Amazon Kendra field name | 
| --- | --- | 
| body | \_document\_body | 
| createdDateTime | \_created\_at | 
| name | \_document\_title | 
| webUrl | \_document\_id | 
| createdBy\.displayName | od\_createdBy\_displayName | 
| createdBy\.id | od\_createdBy\_id | 
| createdBy\.email | oc\_createdBy\_email | 
| cTag | od\_ctag | 
| eTag | od\_etag | 
| fileSystemInfo\.createdDateTime | od\_fileSystemInfo\_createdDateTime | 
| fileSystemInfo\.lastAccessedDateTime | od\_fileSystemInfo\_lastAccessedDateTime | 
| fileSystemInfo\.lastModifiedDateTime | od\_fileSystemInfo\_lastModifiedDateTime | 
| file\.mimeType | od\_file\_mimeType | 
| lastModifiedDateTime | \_last\_updated\_at | 
| lastModifiedBy\.displayName | od\_lastModifiedBy\_displayName | 
| lastModifiedBy\.id | od\_lastModifiedBy\.id | 
| lastModifiedBy\.email | od\_lastModifiedBy\.email | 
| size | od\_size | 
| webDavUrl | oe\_webDavUrl | 