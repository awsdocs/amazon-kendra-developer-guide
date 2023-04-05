--------

--------

# FaqSummary<a name="API_FaqSummary"></a>

Summary information for frequently asked questions and answers included in an index\.

## Contents<a name="API_FaqSummary_Contents"></a>

 ** CreatedAt **   <a name="Kendra-Type-FaqSummary-CreatedAt"></a>
The Unix timestamp when the FAQ was created\.  
Type: Timestamp  
Required: No

 ** FileFormat **   <a name="Kendra-Type-FaqSummary-FileFormat"></a>
The file type used to create the FAQ\.   
Type: String  
Valid Values:` CSV | CSV_WITH_HEADER | JSON`   
Required: No

 ** Id **   <a name="Kendra-Type-FaqSummary-Id"></a>
The identifier of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** LanguageCode **   <a name="Kendra-Type-FaqSummary-LanguageCode"></a>
The code for a language\. This shows a supported language for the FAQ document as part of the summary information for FAQs\. English is supported by default\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 10\.  
Pattern: `[a-zA-Z-]*`   
Required: No

 ** Name **   <a name="Kendra-Type-FaqSummary-Name"></a>
The name that you assigned the FAQ when you created or updated the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** Status **   <a name="Kendra-Type-FaqSummary-Status"></a>
The current status of the FAQ\. When the status is `ACTIVE` the FAQ is ready for use\.  
Type: String  
Valid Values:` CREATING | UPDATING | ACTIVE | DELETING | FAILED`   
Required: No

 ** UpdatedAt **   <a name="Kendra-Type-FaqSummary-UpdatedAt"></a>
The Unix timestamp when the FAQ was last updated\.  
Type: Timestamp  
Required: No

## See Also<a name="API_FaqSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/FaqSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/FaqSummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/FaqSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/FaqSummary) 