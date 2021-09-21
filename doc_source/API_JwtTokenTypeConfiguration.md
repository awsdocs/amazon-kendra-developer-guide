--------

--------

# JwtTokenTypeConfiguration<a name="API_JwtTokenTypeConfiguration"></a>

Configuration information for the JWT token type\.

## Contents<a name="API_JwtTokenTypeConfiguration_Contents"></a>

<<<<<<< HEAD
 ** ClaimRegex **   <a name="Kendra-Type-JwtTokenTypeConfiguration-ClaimRegex"></a>
=======
 **ClaimRegex**   <a name="Kendra-Type-JwtTokenTypeConfiguration-ClaimRegex"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The regular expression that identifies the claim\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** GroupAttributeField **   <a name="Kendra-Type-JwtTokenTypeConfiguration-GroupAttributeField"></a>
=======
 **GroupAttributeField**   <a name="Kendra-Type-JwtTokenTypeConfiguration-GroupAttributeField"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The group attribute field\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** Issuer **   <a name="Kendra-Type-JwtTokenTypeConfiguration-Issuer"></a>
=======
 **Issuer**   <a name="Kendra-Type-JwtTokenTypeConfiguration-Issuer"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The issuer of the token\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 65\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** KeyLocation **   <a name="Kendra-Type-JwtTokenTypeConfiguration-KeyLocation"></a>
=======
 **KeyLocation**   <a name="Kendra-Type-JwtTokenTypeConfiguration-KeyLocation"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The location of the key\.  
Type: String  
Valid Values:` URL | SECRET_MANAGER`   
Required: Yes

<<<<<<< HEAD
 ** SecretManagerArn **   <a name="Kendra-Type-JwtTokenTypeConfiguration-SecretManagerArn"></a>
=======
 **SecretManagerArn**   <a name="Kendra-Type-JwtTokenTypeConfiguration-SecretManagerArn"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Amazon Resource Name \(arn\) of the secret\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

<<<<<<< HEAD
 ** URL **   <a name="Kendra-Type-JwtTokenTypeConfiguration-URL"></a>
=======
 **URL**   <a name="Kendra-Type-JwtTokenTypeConfiguration-URL"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The signing key URL\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: No

<<<<<<< HEAD
 ** UserNameAttributeField **   <a name="Kendra-Type-JwtTokenTypeConfiguration-UserNameAttributeField"></a>
=======
 **UserNameAttributeField**   <a name="Kendra-Type-JwtTokenTypeConfiguration-UserNameAttributeField"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
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