--------

--------

# BoxConfiguration<a name="API_BoxConfiguration"></a>

Provides the configuration information to connect to Box as your data source\.

## Contents<a name="API_BoxConfiguration_Contents"></a>

 ** CommentFieldMappings **   <a name="Kendra-Type-BoxConfiguration-CommentFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Box comments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Box fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Box field names must exist in your Box custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** CrawlComments **   <a name="Kendra-Type-BoxConfiguration-CrawlComments"></a>
 `TRUE` to index comments\.  
Type: Boolean  
Required: No

 ** CrawlTasks **   <a name="Kendra-Type-BoxConfiguration-CrawlTasks"></a>
 `TRUE` to index the contents of tasks\.  
Type: Boolean  
Required: No

 ** CrawlWebLinks **   <a name="Kendra-Type-BoxConfiguration-CrawlWebLinks"></a>
 `TRUE` to index web links\.  
Type: Boolean  
Required: No

 ** EnterpriseId **   <a name="Kendra-Type-BoxConfiguration-EnterpriseId"></a>
The identifier of the Box Enterprise platform\. You can find the enterprise ID in the Box Developer Console settings or when you create an app in Box and download your authentication credentials\. For example, *801234567*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `^[A-Z0-9]*$`   
Required: Yes

 ** ExclusionPatterns **   <a name="Kendra-Type-BoxConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain files and folders from your Box platform\. Files and folders that match the patterns are excluded from the index\.Files and folders that don't match the patterns are included in the index\. If a file or folder matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file or folder isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** FileFieldMappings **   <a name="Kendra-Type-BoxConfiguration-FileFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Box files to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Box fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Box field names must exist in your Box custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-BoxConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain files and folders in your Box platform\. Files and folders that match the patterns are included in the index\. Files and folders that don't match the patterns are excluded from the index\. If a file or folder matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file or folder isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-BoxConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Box platform\. The secret must contain a JSON structure with the following keys:  
+ clientID—The identifier of the client OAuth 2\.0 authentication application created in Box\.
+ clientSecret—A set of characters known only to the OAuth 2\.0 authentication application created in Box\.
+ publicKeyId—The identifier of the public key contained within an identity certificate\.
+ privateKey—A set of characters that make up an encryption key\.
+ passphrase—A set of characters that act like a password\.
You create an application in Box to generate the keys or credentials required for the secret\. For more information, see [Using a Box data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-box.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** TaskFieldMappings **   <a name="Kendra-Type-BoxConfiguration-TaskFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Box tasks to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Box fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Box field names must exist in your Box custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** UseChangeLog **   <a name="Kendra-Type-BoxConfiguration-UseChangeLog"></a>
 `TRUE` to use the Slack change log to determine which documents require updating in the index\. Depending on the data source change log's size, it may take longer for Amazon Kendra to use the change log than to scan all of your documents\.  
Type: Boolean  
Required: No

 ** VpcConfiguration **   <a name="Kendra-Type-BoxConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon VPC to connect to your Box\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

 ** WebLinkFieldMappings **   <a name="Kendra-Type-BoxConfiguration-WebLinkFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Box web links to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Box fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Box field names must exist in your Box custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

## See Also<a name="API_BoxConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BoxConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BoxConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BoxConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BoxConfiguration) 