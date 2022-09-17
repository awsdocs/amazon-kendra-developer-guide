--------

--------

# Using a Google Workspace Drive data source<a name="data-source-google-drive"></a>

You can use an Amazon Kendra data source to connect to Google Workspace Drive to index the documents stored there\. To use Google Drive in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Google Drive\.

For troubleshooting your Amazon Kendra Google Workspace Drive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

You must create an index before you create the Google Drive data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

Before you can index your documents from your Google Drive, you must first use an administrator account to create a service account\. The service account must have read\-only permission for the user and shared drives that you want to index\. The account needs the following permissions:
+ https://www\.googleapis\.com/auth/drive\.readonly
+ https://www\.googleapis\.com/auth/drive\.metadata\.readonly
+ https://www\.googleapis\.com/auth/admin\.directory\.user\.readonly
+ https://www\.googleapis\.com/auth/admin\.directory\.group\.readonly

Once you have created the service account, download the key file to your computer\. You send this key to Amazon Kendra when you create the data source\.

To connecto to Google Drive, you specify connection and other information in the console or by using the [GoogleDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GoogleDriveConfiguration.html) object\.

Amazon Kendra indexes the documents stored in shared drives as well as the documents stored in user My Drives\. By default, Amazon Kendra indexes all documents in your Google Drive\. You can exclude documents from the index based on the ID of a shared drive, the user that owns the document, the MIME type of the document, or their path\.

The Google Drive data source indexes Google Workspace documents as well as the documents listed in [Types of documents](index-document-types.md)\. The supported Google Workspace document types are: 
+ Google Docs
+ Google Slides

You must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Google Drive\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Google Drive data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Google Drive\. You store the Google Drive credentials in an AWS Secrets Manager secret\. The credentials are client \(service\) account, admin account, private key\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source, or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{
    "clientAccount": "account email",
    "adminAccount": "account email",
    "privateKey": "private key"
}
```

After you create the data source, you can:
+ Modify the Secrets Manager secret containing the credentials required to access Google Workspace\.
+ Modify the list of user accounts to exclude from indexing\.
+ Modify the list of shared drives to exclude from indexing\.
+ Modify the include and exclude regular expressions\.
+ Modify the MIME types to exclude from indexing\.

After you sync the data source, you can't remove the field mappings\. You can map additional fields\.

By default, Amazon Kendra indexes all supported documents stored on your Google Workspace Drive and any My Drives for your users\. You can exclude documents using the console or by setting the following fields of the `GoogleDriveConfiguration` parameter when you create the data source\. Exclusions are combined with a logical AND, so if a file matches any of the exclusions it isn't included in the index\.
+ `ExcludeMimeTypes`—One or more MIME types of the documents to exclude\. For example, if you specify the MIME type for Microsoft Word documents, those documents aren't indexed\.
+ `ExcludeSharedDrives`—One or more shared drive identifiers to exclude\. None of the files on the shared drive are indexed\.
+ `ExcludeUserAccounts`—One or more email addresses of user accounts to exclude from the index\. None of the files in the My Drive owned by the account are indexed\. Files shared with the user are indexed unless the owner of the file is also excluded\.
+ `ExclusionPatterns`—One or more regular expressions\. Files that match the pattern aren't indexed\.
+ `InclusionPatterns`—One or more regular expressions\. Files that match the pattern are indexed, all other files are excluded from the index\. Any file that matches another exclusion isn't indexed even if it matches the inclusion pattern\.

You can map Google Drive properties to Amazon Kendra index fields\. The following table shows the Google Drive properties that can be mapped and a suggested Amazon Kendra index field\.


| Google Drive property name | Suggested Amazon Kendra field name | 
| --- | --- | 
| createdTime | \_created\_at | 
| dataSize | gd\_data\_size | 
| displayUrl | gd\_source\_url | 
| fileExtension | \_file\_type | 
| id | \_document\_id | 
| mimeType | gd\_mime\_type | 
| modifiedTime | \_last\_updated\_at | 
| name | \_document\_title | 
| owner | gd\_owner | 
| version | gd\_version | 

The Google Drive API enables you to create custom file properties using key/value pairs\. You can map these custom properties to Amazon Kendra index fields\. You must prefix the name of the field with the string "property"\. when you specify the field name\. For example, a custom property called "author" is specified as "property\.author"\.