--------

--------

# ExperiencesSummary<a name="API_ExperiencesSummary"></a>

Summary information for your Amazon Kendra experience\. You can create an Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Contents<a name="API_ExperiencesSummary_Contents"></a>

 ** CreatedAt **   <a name="Kendra-Type-ExperiencesSummary-CreatedAt"></a>
The date\-time your Amazon Kendra experience was created\.  
Type: Timestamp  
Required: No

 ** Endpoints **   <a name="Kendra-Type-ExperiencesSummary-Endpoints"></a>
The endpoint URLs for your Amazon Kendra experiences\. The URLs are unique and fully hosted by AWS\.  
Type: Array of [ ExperienceEndpoint ](API_ExperienceEndpoint.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 2 items\.  
Required: No

 ** Id **   <a name="Kendra-Type-ExperiencesSummary-Id"></a>
The identifier of your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** Name **   <a name="Kendra-Type-ExperiencesSummary-Name"></a>
The name of your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** Status **   <a name="Kendra-Type-ExperiencesSummary-Status"></a>
The processing status of your Amazon Kendra experience\.  
Type: String  
Valid Values:` CREATING | ACTIVE | DELETING | FAILED`   
Required: No

## See Also<a name="API_ExperiencesSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ExperiencesSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ExperiencesSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ExperiencesSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ExperiencesSummary) 