--------

--------

# GoogleDriveConfiguration<a name="API_GoogleDriveConfiguration"></a>

Provides configuration information for data sources that connect to Google Drive\.

## Contents<a name="API_GoogleDriveConfiguration_Contents"></a>

 **ExcludeMimeTypes**   <a name="Kendra-Type-GoogleDriveConfiguration-ExcludeMimeTypes"></a>
A list of MIME types to exclude from the index\. All documents matching the specified MIME type are excluded\.   
For a list of MIME types, see [Using a Google Workspace Drive data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-google-drive.html)\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 30 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^\P{C}*$`   
Required: No

 **ExcludeSharedDrives**   <a name="Kendra-Type-GoogleDriveConfiguration-ExcludeSharedDrives"></a>
A list of identifiers or shared drives to exclude from the index\. All files and folders stored on the shared drive are excluded\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^\P{C}*$`   
Required: No

 **ExcludeUserAccounts**   <a name="Kendra-Type-GoogleDriveConfiguration-ExcludeUserAccounts"></a>
A list of email addresses of the users\. Documents owned by these users are excluded from the index\. Documents shared with excluded users are indexed unless they are excluded in another way\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^\P{C}*$`   
Required: No

 **ExclusionPatterns**   <a name="Kendra-Type-GoogleDriveConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns that apply to the path on Google Drive\. Items that match the pattern are excluded from the index from both shared drives and users' My Drives\. Items that don't match the pattern are included in the index\. If an item matches both an exclusion pattern and an inclusion pattern, it is excluded from the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 **FieldMappings**   <a name="Kendra-Type-GoogleDriveConfiguration-FieldMappings"></a>
Defines mapping between a field in the Google Drive and a Amazon Kendra index field\.  
If you are using the console, you can define index fields when creating the mapping\. If you are using the API, you must first create the field using the `UpdateIndex` operation\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 **InclusionPatterns**   <a name="Kendra-Type-GoogleDriveConfiguration-InclusionPatterns"></a>
A list of regular expression patterns that apply to path on Google Drive\. Items that match the pattern are included in the index from both shared drives and users' My Drives\. Items that don't match the pattern are excluded from the index\. If an item matches both an inclusion pattern and an exclusion pattern, it is excluded from the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 **SecretArn**   <a name="Kendra-Type-GoogleDriveConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of a AWS Secrets Managersecret that contains the credentials required to connect to Google Drive\. For more information, see [Using a Google Workspace Drive data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-google-drive.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

## See Also<a name="API_GoogleDriveConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GoogleDriveConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GoogleDriveConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GoogleDriveConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GoogleDriveConfiguration) 