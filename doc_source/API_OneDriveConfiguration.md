--------

--------

# OneDriveConfiguration<a name="API_OneDriveConfiguration"></a>

Provides the configuration information to connect to OneDrive as your data source\.

## Contents<a name="API_OneDriveConfiguration_Contents"></a>

 ** DisableLocalGroups **   <a name="Kendra-Type-OneDriveConfiguration-DisableLocalGroups"></a>
 `TRUE` to disable local groups information\.  
Type: Boolean  
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-OneDriveConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain documents in your OneDrive\. Documents that match the patterns are excluded from the index\. Documents that don't match the patterns are included in the index\. If a document matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the document isn't included in the index\.  
The pattern is applied to the file name\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** FieldMappings **   <a name="Kendra-Type-OneDriveConfiguration-FieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map OneDrive data source attributes or field names to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to OneDrive fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The OneDrive data source field names must exist in your OneDrive custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-OneDriveConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain documents in your OneDrive\. Documents that match the patterns are included in the index\. Documents that don't match the patterns are excluded from the index\. If a document matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the document isn't included in the index\.  
The pattern is applied to the file name\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** OneDriveUsers **   <a name="Kendra-Type-OneDriveConfiguration-OneDriveUsers"></a>
A list of user accounts whose documents should be indexed\.  
Type: [OneDriveUsers](API_OneDriveUsers.md) object  
Required: Yes

 ** SecretArn **   <a name="Kendra-Type-OneDriveConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Managersecret that contains the user name and password to connect to OneDrive\. The user namd should be the application ID for the OneDrive application, and the password is the application key for the OneDrive application\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** TenantDomain **   <a name="Kendra-Type-OneDriveConfiguration-TenantDomain"></a>
The Azure Active Directory domain of the organization\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Pattern: `^([a-zA-Z0-9]+(-[a-zA-Z0-9]+)*\.)+[a-z]{2,}$`   
Required: Yes

## See Also<a name="API_OneDriveConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/OneDriveConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/OneDriveConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/OneDriveConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/OneDriveConfiguration) 