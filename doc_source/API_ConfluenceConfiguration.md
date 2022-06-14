--------

--------

# ConfluenceConfiguration<a name="API_ConfluenceConfiguration"></a>

Provides the configuration information to connect to Confluence as your data source\.

## Contents<a name="API_ConfluenceConfiguration_Contents"></a>

 ** AttachmentConfiguration **   <a name="Kendra-Type-ConfluenceConfiguration-AttachmentConfiguration"></a>
Configuration information for indexing attachments to Confluence blogs and pages\.  
Type: [ConfluenceAttachmentConfiguration](API_ConfluenceAttachmentConfiguration.md) object  
Required: No

 ** BlogConfiguration **   <a name="Kendra-Type-ConfluenceConfiguration-BlogConfiguration"></a>
Configuration information for indexing Confluence blogs\.  
Type: [ConfluenceBlogConfiguration](API_ConfluenceBlogConfiguration.md) object  
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-ConfluenceConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain blog posts, pages, spaces, or attachments in your Confluence\. Content that matches the patterns are excluded from the index\. Content that doesn't match the patterns is included in the index\. If content matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the content isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-ConfluenceConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain blog posts, pages, spaces, or attachments in your Confluence\. Content that matches the patterns are included in the index\. Content that doesn't match the patterns is excluded from the index\. If content matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the content isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** PageConfiguration **   <a name="Kendra-Type-ConfluenceConfiguration-PageConfiguration"></a>
Configuration information for indexing Confluence pages\.  
Type: [ConfluencePageConfiguration](API_ConfluencePageConfiguration.md) object  
Required: No

 ** SecretArn **   <a name="Kendra-Type-ConfluenceConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the user name and password required to connect to the Confluence instance\. If you use Confluence cloud, you use a generated API token as the password\. For more information, see [Using a Confluemce data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-confluence.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** ServerUrl **   <a name="Kendra-Type-ConfluenceConfiguration-ServerUrl"></a>
The URL of your Confluence instance\. Use the full URL of the server\. For example, *https://server\.example\.com:port/*\. You can also use an IP address, for example, *https://192\.168\.1\.113/*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: Yes

 ** SpaceConfiguration **   <a name="Kendra-Type-ConfluenceConfiguration-SpaceConfiguration"></a>
Configuration information for indexing Confluence spaces\.  
Type: [ConfluenceSpaceConfiguration](API_ConfluenceSpaceConfiguration.md) object  
Required: No

 ** Version **   <a name="Kendra-Type-ConfluenceConfiguration-Version"></a>
The version or the type of the Confluence installation to connect to\.  
Type: String  
Valid Values:` CLOUD | SERVER`   
Required: Yes

 ** VpcConfiguration **   <a name="Kendra-Type-ConfluenceConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud to connect to your Confluence\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

## See Also<a name="API_ConfluenceConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluenceConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluenceConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluenceConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluenceConfiguration) 