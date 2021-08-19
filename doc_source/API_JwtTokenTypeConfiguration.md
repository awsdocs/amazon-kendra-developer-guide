--------

--------

# JwtTokenTypeConfiguration<a name="API_JwtTokenTypeConfiguration"></a>

Configuration information for the JWT token type\.

## Contents<a name="API_JwtTokenTypeConfiguration_Contents"></a>

 **ClaimRegex**   <a name="Kendra-Type-JwtTokenTypeConfiguration-ClaimRegex"></a>
The regular expression that identifies the claim\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^\P{C}*$`   
Required: No

 **GroupAttributeField**   <a name="Kendra-Type-JwtTokenTypeConfiguration-GroupAttributeField"></a>
The group attribute field\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^\P{C}*$`   
Required: No

 **Issuer**   <a name="Kendra-Type-JwtTokenTypeConfiguration-Issuer"></a>
The issuer of the token\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 65\.  
Pattern: `^\P{C}*$`   
Required: No

 **KeyLocation**   <a name="Kendra-Type-JwtTokenTypeConfiguration-KeyLocation"></a>
The location of the key\.  
Type: String  
Valid Values:` URL | SECRET_MANAGER`   
Required: Yes

 **SecretManagerArn**   <a name="Kendra-Type-JwtTokenTypeConfiguration-SecretManagerArn"></a>
The Amazon Resource Name \(arn\) of the secret\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 **URL**   <a name="Kendra-Type-JwtTokenTypeConfiguration-URL"></a>
The signing key URL\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: No

 **UserNameAttributeField**   <a name="Kendra-Type-JwtTokenTypeConfiguration-UserNameAttributeField"></a>
The user name attribute field\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^\P{C}*$`   
Required: No

## See Also<a name="API_JwtTokenTypeConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/JwtTokenTypeConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/JwtTokenTypeConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/JwtTokenTypeConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/JwtTokenTypeConfiguration) 