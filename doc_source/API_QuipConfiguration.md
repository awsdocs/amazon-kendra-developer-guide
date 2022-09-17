--------

--------

# QuipConfiguration<a name="API_QuipConfiguration"></a>

Provides the configuration information to connect to Quip as your data source\.

## Contents<a name="API_QuipConfiguration_Contents"></a>

 ** AttachmentFieldMappings **   <a name="Kendra-Type-QuipConfiguration-AttachmentFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Quip attachments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Quip fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Quip field names must exist in your Quip custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** CrawlAttachments **   <a name="Kendra-Type-QuipConfiguration-CrawlAttachments"></a>
 `TRUE` to index attachments\.  
Type: Boolean  
Required: No

 ** CrawlChatRooms **   <a name="Kendra-Type-QuipConfiguration-CrawlChatRooms"></a>
 `TRUE` to index the contents of chat rooms\.  
Type: Boolean  
Required: No

 ** CrawlFileComments **   <a name="Kendra-Type-QuipConfiguration-CrawlFileComments"></a>
 `TRUE` to index file comments\.  
Type: Boolean  
Required: No

 ** Domain **   <a name="Kendra-Type-QuipConfiguration-Domain"></a>
The Quip site domain\. For example, *https://quip\-company\.quipdomain\.com/browse*\. The domain in this example is "quipdomain"\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 63\.  
Pattern: `^(?!-)[A-Za-z0-9-].*(?<!-)$`   
Required: Yes

 ** ExclusionPatterns **   <a name="Kendra-Type-QuipConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain files in your Quip file system\. Files that match the patterns are excluded from the index\. Files that don’t match the patterns are included in the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence, and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** FolderIds **   <a name="Kendra-Type-QuipConfiguration-FolderIds"></a>
The identifiers of the Quip folders you want to index\. You can find the folder ID in your browser URL when you access your folder in Quip\. For example, *https://quip\-company\.quipdomain\.com/zlLuOVNSarTL/folder\-name*\. The folder ID in this example is "zlLuOVNSarTL"\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 500\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-QuipConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain files in your Quip file system\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence, and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** MessageFieldMappings **   <a name="Kendra-Type-QuipConfiguration-MessageFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Quip messages to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Quip fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Quip field names must exist in your Quip custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-QuipConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs that are required to connect to your Quip\. The secret must contain a JSON structure with the following keys:  
+ accessToken—The token created in Quip\. For more information, see [Authentication for a Quip data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-slack.html#quip-authentication)\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** ThreadFieldMappings **   <a name="Kendra-Type-QuipConfiguration-ThreadFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Quip threads to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Quip fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Quip field names must exist in your Quip custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** VpcConfiguration **   <a name="Kendra-Type-QuipConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud \(VPC\) to connect to your Quip\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

## See Also<a name="API_QuipConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/QuipConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/QuipConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/QuipConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/QuipConfiguration) 