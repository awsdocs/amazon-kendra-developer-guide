--------

--------

# ProxyConfiguration<a name="API_ProxyConfiguration"></a>

Provides the configuration information for a web proxy to connect to website hosts\.

## Contents<a name="API_ProxyConfiguration_Contents"></a>

 ** Credentials **   <a name="Kendra-Type-ProxyConfiguration-Credentials"></a>
Your secret ARN, which you can create in [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)   
The credentials are optional\. You use a secret if web proxy credentials are required to connect to a website host\. Amazon Kendra currently support basic authentication to connect to a web proxy server\. The secret stores your credentials\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** Host **   <a name="Kendra-Type-ProxyConfiguration-Host"></a>
The name of the website host you want to connect to via a web proxy server\.  
For example, the host name of https://a\.example\.com/page1\.html is "a\.example\.com"\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 253\.  
Pattern: `([^\s]*)`   
Required: Yes

 ** Port **   <a name="Kendra-Type-ProxyConfiguration-Port"></a>
The port number of the website host you want to connect to via a web proxy server\.   
For example, the port for https://a\.example\.com/page1\.html is 443, the standard port for HTTPS\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65535\.  
Required: Yes

## See Also<a name="API_ProxyConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ProxyConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ProxyConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ProxyConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ProxyConfiguration) 