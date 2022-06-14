--------

--------

# FsxConfiguration<a name="API_FsxConfiguration"></a>

Provides the configuration information to connect to Amazon FSx as your data source\.

## Contents<a name="API_FsxConfiguration_Contents"></a>

 ** ExclusionPatterns **   <a name="Kendra-Type-FsxConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain files in your Amazon FSx file system\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** FieldMappings **   <a name="Kendra-Type-FsxConfiguration-FieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map Amazon FSx data source attributes or field names to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Amazon FSx fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Amazon FSx data source field names must exist in your Amazon FSx custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** FileSystemId **   <a name="Kendra-Type-FsxConfiguration-FileSystemId"></a>
The identifier of the Amazon FSx file system\.  
You can find your file system ID on the file system dashboard in the Amazon FSx console\. For information on how to create a file system in Amazon FSx console, using Windows File Server as an example, see [Amazon FSx Getting started guide](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/getting-started-step1.html)\.  
Type: String  
Length Constraints: Minimum length of 11\. Maximum length of 21\.  
Pattern: `^(fs-[0-9a-f]{8,})$`   
Required: Yes

 ** FileSystemType **   <a name="Kendra-Type-FsxConfiguration-FileSystemType"></a>
The Amazon FSx file system type\. Windows is currently the only supported type\.  
Type: String  
Valid Values:` WINDOWS`   
Required: Yes

 ** InclusionPatterns **   <a name="Kendra-Type-FsxConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain files in your Amazon FSx file system\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-FsxConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Amazon FSx file system\. Windows is currently the only supported type\. The secret must contain a JSON structure with the following keys:  
+ username—The Active Directory user name, along with the Domain Name System \(DNS\) domain name\. For example, *user@corp\.example\.com*\. The Active Directory user account must have read and mounting access to the Amazon FSx file system for Windows\.
+ password—The password of the Active Directory user account with read and mounting access to the Amazon FSx Windows file system\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** VpcConfiguration **   <a name="Kendra-Type-FsxConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud to connect to your Amazon FSx\. Your Amazon FSx instance must reside inside your VPC\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: Yes

## See Also<a name="API_FsxConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FsxConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FsxConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FsxConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FsxConfiguration) 