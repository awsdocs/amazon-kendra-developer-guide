--------

--------

# EntityConfiguration<a name="API_EntityConfiguration"></a>

Provides the configuration information of users or groups in your AWS SSO identity source to grant access your Amazon Kendra experience\.

## Contents<a name="API_EntityConfiguration_Contents"></a>

 ** EntityId **   <a name="Kendra-Type-EntityConfiguration-EntityId"></a>
The identifier of a user or group in your AWS SSO identity source\. For example, a user ID could be an email\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 47\.  
Pattern: `^([0-9a-f]{10}-|)[A-Fa-f0-9]{8}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{12}$`   
Required: Yes

 ** EntityType **   <a name="Kendra-Type-EntityConfiguration-EntityType"></a>
Specifies whether you are configuring a `User` or a `Group`\.  
Type: String  
Valid Values:` USER | GROUP`   
Required: Yes

## See Also<a name="API_EntityConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/EntityConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/EntityConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/EntityConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/EntityConfiguration) 