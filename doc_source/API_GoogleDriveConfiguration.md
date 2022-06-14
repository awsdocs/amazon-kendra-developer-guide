--------

--------

# GoogleDriveConfiguration<a name="API_GoogleDriveConfiguration"></a>

Provides the configuration information to connect to Google Drive as your data source\.

## Contents<a name="API_GoogleDriveConfiguration_Contents"></a>

 ** ExcludeMimeTypes **   <a name="Kendra-Type-GoogleDriveConfiguration-ExcludeMimeTypes"></a>
A list of MIME types to exclude from the index\. All documents matching the specified MIME type are excluded\.   
For a list of MIME types, see [Using a Google Workspace Drive data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-google-drive.html)\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 30 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^\P{C}*$`   
Required: No

 ** ExcludeSharedDrives **   <a name="Kendra-Type-GoogleDriveConfiguration-ExcludeSharedDrives"></a>
A list of identifiers or shared drives to exclude from the index\. All files and folders stored on the shared drive are excluded\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^\P{C}*$`   
Required: No

 ** ExcludeUserAccounts **   <a name="Kendra-Type-GoogleDriveConfiguration-ExcludeUserAccounts"></a>
A list of email addresses of the users\. Documents owned by these users are excluded from the index\. Documents shared with excluded users are indexed unless they are excluded in another way\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^\P{C}*$`   
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-GoogleDriveConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain items in your Google Drive, including shared drives and users' My Drives\. Items that match the patterns are excluded from the index\. Items that don't match the patterns are included in the index\. If an item matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the item isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** FieldMappings **   <a name="Kendra-Type-GoogleDriveConfiguration-FieldMappings"></a>
Maps Google Drive data source attributes or field names to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Google Drive fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Google Drive data source field names must exist in your Google Drive custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-GoogleDriveConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain items in your Google Drive, including shared drives and users' My Drives\. Items that match the patterns are included in the index\. Items that don't match the patterns are excluded from the index\. If an item matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the item isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-GoogleDriveConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of a AWS Secrets Managersecret that contains the credentials required to connect to Google Drive\. For more information, see [Using a Google Workspace Drive data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-google-drive.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

## See Also<a name="API_GoogleDriveConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GoogleDriveConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GoogleDriveConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GoogleDriveConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GoogleDriveConfiguration) 