--------

--------

# SaaSConfiguration<a name="API_SaaSConfiguration"></a>

Provides the configuration information to connect to GitHub Enterprise Cloud \(SaaS\)\.

## Contents<a name="API_SaaSConfiguration_Contents"></a>

 ** HostUrl **   <a name="Kendra-Type-SaaSConfiguration-HostUrl"></a>
The GitHub host URL or API endpoint URL\. For example, *https://api\.github\.com*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: Yes

 ** OrganizationName **   <a name="Kendra-Type-SaaSConfiguration-OrganizationName"></a>
The name of the organization of the GitHub Enterprise Cloud \(SaaS\) account you want to connect to\. You can find your organization name by logging into GitHub desktop and selecting **Your organizations** under your profile picture dropdown\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 60\.  
Pattern: `^[A-Za-z0-9_.-]+$`   
Required: Yes

## See Also<a name="API_SaaSConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/SaaSConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/SaaSConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/SaaSConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/SaaSConfiguration) 