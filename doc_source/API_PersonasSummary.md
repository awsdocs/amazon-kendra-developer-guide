--------

--------

# PersonasSummary<a name="API_PersonasSummary"></a>

Summary information for users or groups in your AWS SSO identity source\. This applies to users and groups with specific permissions that define their level of access to your Amazon Kendra experience\. You can create an Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Contents<a name="API_PersonasSummary_Contents"></a>

 ** CreatedAt **   <a name="Kendra-Type-PersonasSummary-CreatedAt"></a>
The date\-time the summary information was created\.  
Type: Timestamp  
Required: No

 ** EntityId **   <a name="Kendra-Type-PersonasSummary-EntityId"></a>
The identifier of a user or group in your AWS SSO identity source\. For example, a user ID could be an email\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 47\.  
Pattern: `^([0-9a-f]{10}-|)[A-Fa-f0-9]{8}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{12}$`   
Required: No

 ** Persona **   <a name="Kendra-Type-PersonasSummary-Persona"></a>
The persona that defines the specific permissions of the user or group in your AWS SSO identity source\. The available personas or access roles are `Owner` and `Viewer`\. For more information on these personas, see [Providing access to your search page](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html#access-search-experience)\.  
Type: String  
Valid Values:` OWNER | VIEWER`   
Required: No

 ** UpdatedAt **   <a name="Kendra-Type-PersonasSummary-UpdatedAt"></a>
The date\-time the summary information was last updated\.  
Type: Timestamp  
Required: No

## See Also<a name="API_PersonasSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/PersonasSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/PersonasSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/PersonasSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/PersonasSummary) 