--------

--------

# ExperienceEntitiesSummary<a name="API_ExperienceEntitiesSummary"></a>

Summary information for users or groups in your AWS SSO identity source with granted access to your Amazon Kendra experience\. You can create an Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Contents<a name="API_ExperienceEntitiesSummary_Contents"></a>

 ** DisplayData **   <a name="Kendra-Type-ExperienceEntitiesSummary-DisplayData"></a>
Information about the user entity\.  
Type: [ EntityDisplayData ](API_EntityDisplayData.md) object  
Required: No

 ** EntityId **   <a name="Kendra-Type-ExperienceEntitiesSummary-EntityId"></a>
The identifier of a user or group in your AWS SSO identity source\. For example, a user ID could be an email\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 47\.  
Pattern: `^([0-9a-f]{10}-|)[A-Fa-f0-9]{8}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{12}$`   
Required: No

 ** EntityType **   <a name="Kendra-Type-ExperienceEntitiesSummary-EntityType"></a>
Shows the type as `User` or `Group`\.  
Type: String  
Valid Values:` USER | GROUP`   
Required: No

## See Also<a name="API_ExperienceEntitiesSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ExperienceEntitiesSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ExperienceEntitiesSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ExperienceEntitiesSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ExperienceEntitiesSummary) 