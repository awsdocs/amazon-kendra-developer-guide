--------

--------

# CustomDocumentEnrichmentConfiguration<a name="API_CustomDocumentEnrichmentConfiguration"></a>

Provides the configuration information for altering document metadata and content during the document ingestion process\.

For more information, see [Customizing document metadata during the ingestion process](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\.

## Contents<a name="API_CustomDocumentEnrichmentConfiguration_Contents"></a>

 ** InlineConfigurations **   <a name="Kendra-Type-CustomDocumentEnrichmentConfiguration-InlineConfigurations"></a>
Configuration information to alter document attributes or metadata fields and content when ingesting documents into Amazon Kendra\.  
Type: Array of [ InlineCustomDocumentEnrichmentConfiguration ](API_InlineCustomDocumentEnrichmentConfiguration.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Required: No

 ** PostExtractionHookConfiguration **   <a name="Kendra-Type-CustomDocumentEnrichmentConfiguration-PostExtractionHookConfiguration"></a>
Configuration information for invoking a Lambda function in AWS Lambda on the structured documents with their metadata and text extracted\. You can use a Lambda function to apply advanced logic for creating, modifying, or deleting document metadata and content\. For more information, see [Advanced data manipulation](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html#advanced-data-manipulation)\.  
Type: [ HookConfiguration ](API_HookConfiguration.md) object  
Required: No

 ** PreExtractionHookConfiguration **   <a name="Kendra-Type-CustomDocumentEnrichmentConfiguration-PreExtractionHookConfiguration"></a>
Configuration information for invoking a Lambda function in AWS Lambda on the original or raw documents before extracting their metadata and text\. You can use a Lambda function to apply advanced logic for creating, modifying, or deleting document metadata and content\. For more information, see [Advanced data manipulation](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html#advanced-data-manipulation)\.  
Type: [ HookConfiguration ](API_HookConfiguration.md) object  
Required: No

 ** RoleArn **   <a name="Kendra-Type-CustomDocumentEnrichmentConfiguration-RoleArn"></a>
The Amazon Resource Name \(ARN\) of a role with permission to run `PreExtractionHookConfiguration` and `PostExtractionHookConfiguration` for altering document metadata and content during the document ingestion process\. For more information, see [IAM roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

## See Also<a name="API_CustomDocumentEnrichmentConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CustomDocumentEnrichmentConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CustomDocumentEnrichmentConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CustomDocumentEnrichmentConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CustomDocumentEnrichmentConfiguration) 