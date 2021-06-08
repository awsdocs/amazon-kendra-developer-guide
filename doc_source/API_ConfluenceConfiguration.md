--------

--------

# ConfluenceConfiguration<a name="API_ConfluenceConfiguration"></a>

Provides configuration information for data sources that connect to Confluence\.

## Contents<a name="API_ConfluenceConfiguration_Contents"></a>

 **AttachmentConfiguration**   <a name="Kendra-Type-ConfluenceConfiguration-AttachmentConfiguration"></a>
Specifies configuration information for indexing attachments to Confluence blogs and pages\.  
Type: [ConfluenceAttachmentConfiguration](API_ConfluenceAttachmentConfiguration.md) object  
Required: No

 **BlogConfiguration**   <a name="Kendra-Type-ConfluenceConfiguration-BlogConfiguration"></a>
 Specifies configuration information for indexing Confluence blogs\.  
Type: [ConfluenceBlogConfiguration](API_ConfluenceBlogConfiguration.md) object  
Required: No

 **ExclusionPatterns**   <a name="Kendra-Type-ConfluenceConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns that apply to a URL on the Confluence server\. An exclusion pattern can apply to a blog post, a page, a space, or an attachment\. Items that match the pattern are excluded from the index\. Items that don't match the pattern are included in the index\. If a item matches both an exclusion pattern and an inclusion pattern, the item isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 **InclusionPatterns**   <a name="Kendra-Type-ConfluenceConfiguration-InclusionPatterns"></a>
A list of regular expression patterns that apply to a URL on the Confluence server\. An inclusion pattern can apply to a blog post, a page, a space, or an attachment\. Items that match the patterns are included in the index\. Items that don't match the pattern are excluded from the index\. If an item matches both an inclusion pattern and an exclusion pattern, the item isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 **PageConfiguration**   <a name="Kendra-Type-ConfluenceConfiguration-PageConfiguration"></a>
Specifies configuration information for indexing Confluence pages\.  
Type: [ConfluencePageConfiguration](API_ConfluencePageConfiguration.md) object  
Required: No

 **SecretArn**   <a name="Kendra-Type-ConfluenceConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key/value pairs required to connect to your Confluence server\. The secret must contain a JSON structure with the following keys:  
+ username \- The user name or email address of a user with administrative privileges for the Confluence server\.
+ password \- The password associated with the user logging in to the Confluence server\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 **ServerUrl**   <a name="Kendra-Type-ConfluenceConfiguration-ServerUrl"></a>
The URL of your Confluence instance\. Use the full URL of the server\. For example, `https://server.example.com:port/`\. You can also use an IP address, for example, `https://192.168.1.113/`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: Yes

 **SpaceConfiguration**   <a name="Kendra-Type-ConfluenceConfiguration-SpaceConfiguration"></a>
Specifies configuration information for indexing Confluence spaces\.  
Type: [ConfluenceSpaceConfiguration](API_ConfluenceSpaceConfiguration.md) object  
Required: No

 **Version**   <a name="Kendra-Type-ConfluenceConfiguration-Version"></a>
Specifies the version of the Confluence installation that you are connecting to\.  
Type: String  
Valid Values:` CLOUD | SERVER`   
Required: Yes

 **VpcConfiguration**   <a name="Kendra-Type-ConfluenceConfiguration-VpcConfiguration"></a>
Specifies the information for connecting to an Amazon VPC\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

## See Also<a name="API_ConfluenceConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluenceConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluenceConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluenceConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluenceConfiguration) 