--------

--------

# BasicAuthenticationConfiguration<a name="API_BasicAuthenticationConfiguration"></a>

Provides the configuration information to connect to websites that require basic user authentication\.

## Contents<a name="API_BasicAuthenticationConfiguration_Contents"></a>

 ** Credentials **   <a name="Kendra-Type-BasicAuthenticationConfiguration-Credentials"></a>
Your secret ARN, which you can create in [ AWS Secrets Manager ](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)   
You use a secret if basic authentication credentials are required to connect to a website\. The secret stores your credentials of user name and password\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** Host **   <a name="Kendra-Type-BasicAuthenticationConfiguration-Host"></a>
The name of the website host you want to connect to using authentication credentials\.  
For example, the host name of https://a\.example\.com/page1\.html is "a\.example\.com"\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 253\.  
Pattern: `([^\s]*)`   
Required: Yes

 ** Port **   <a name="Kendra-Type-BasicAuthenticationConfiguration-Port"></a>
The port number of the website host you want to connect to using authentication credentials\.  
For example, the port for https://a\.example\.com/page1\.html is 443, the standard port for HTTPS\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 65535\.  
Required: Yes

## See Also<a name="API_BasicAuthenticationConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BasicAuthenticationConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BasicAuthenticationConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BasicAuthenticationConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BasicAuthenticationConfiguration) 