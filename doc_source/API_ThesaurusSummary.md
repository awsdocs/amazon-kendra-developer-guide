--------

--------

# ThesaurusSummary<a name="API_ThesaurusSummary"></a>

An array of summary information for a thesaurus or multiple thesauri\.

## Contents<a name="API_ThesaurusSummary_Contents"></a>

 ** CreatedAt **   <a name="Kendra-Type-ThesaurusSummary-CreatedAt"></a>
The Unix timestamp when the thesaurus was created\.  
Type: Timestamp  
Required: No

 ** Id **   <a name="Kendra-Type-ThesaurusSummary-Id"></a>
The identifier of the thesaurus\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** Name **   <a name="Kendra-Type-ThesaurusSummary-Name"></a>
The name of the thesaurus\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** Status **   <a name="Kendra-Type-ThesaurusSummary-Status"></a>
The status of the thesaurus\.  
Type: String  
Valid Values:` CREATING | ACTIVE | DELETING | UPDATING | ACTIVE_BUT_UPDATE_FAILED | FAILED`   
Required: No

 ** UpdatedAt **   <a name="Kendra-Type-ThesaurusSummary-UpdatedAt"></a>
The Unix timestamp when the thesaurus was last updated\.  
Type: Timestamp  
Required: No

## See Also<a name="API_ThesaurusSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ThesaurusSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ThesaurusSummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ThesaurusSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ThesaurusSummary) 