--------

--------

# EntityPersonaConfiguration<a name="API_EntityPersonaConfiguration"></a>

Provides the configuration information of users or groups in your AWS SSO identity source for access to your Amazon Kendra experience\. Specific permissions are defined for each user or group once they are granted access to your Amazon Kendra experience\.

## Contents<a name="API_EntityPersonaConfiguration_Contents"></a>

 ** EntityId **   <a name="Kendra-Type-EntityPersonaConfiguration-EntityId"></a>
The identifier of a user or group in your AWS SSO identity source\. For example, a user ID could be an email\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 47\.  
Pattern: `^([0-9a-f]{10}-|)[A-Fa-f0-9]{8}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{12}$`   
Required: Yes

 ** Persona **   <a name="Kendra-Type-EntityPersonaConfiguration-Persona"></a>
The persona that defines the specific permissions of the user or group in your AWS SSO identity source\. The available personas or access roles are `Owner` and `Viewer`\. For more information on these personas, see [Providing access to your search page](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html#access-search-experience)\.  
Type: String  
Valid Values:` OWNER | VIEWER`   
Required: Yes

## See Also<a name="API_EntityPersonaConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/EntityPersonaConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/EntityPersonaConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/EntityPersonaConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/EntityPersonaConfiguration) 