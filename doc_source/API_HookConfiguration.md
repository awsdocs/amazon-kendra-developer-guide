--------

--------

# HookConfiguration<a name="API_HookConfiguration"></a>

Provides the configuration information for invoking a Lambda function in AWS Lambda to alter document metadata and content when ingesting documents into Amazon Kendra\. You can configure your Lambda function using [PreExtractionHookConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CustomDocumentEnrichmentConfiguration.html) if you want to apply advanced alterations on the original or raw documents\. If you want to apply advanced alterations on the Amazon Kendra structured documents, you must configure your Lambda function using [PostExtractionHookConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CustomDocumentEnrichmentConfiguration.html)\. You can only invoke one Lambda function\. However, this function can invoke other functions it requires\.

For more information, see [Customizing document metadata during the ingestion process](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\.

## Contents<a name="API_HookConfiguration_Contents"></a>

 ** InvocationCondition **   <a name="Kendra-Type-HookConfiguration-InvocationCondition"></a>
The condition used for when a Lambda function should be invoked\.  
For example, you can specify a condition that if there are empty date\-time values, then Amazon Kendra should invoke a function that inserts the current date\-time\.  
Type: [DocumentAttributeCondition](API_DocumentAttributeCondition.md) object  
Required: No

 ** LambdaArn **   <a name="Kendra-Type-HookConfiguration-LambdaArn"></a>
The Amazon Resource Name \(ARN\) of a role with permission to run a Lambda function during ingestion\. For more information, see [IAM roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `/arn:aws[a-zA-Z-]*:lambda:[a-z]+-[a-z]+-[0-9]:[0-9]{12}:function:[a-zA-Z0-9-_]+(\/[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12})?(:[a-zA-Z0-9-_]+)?/`   
Required: Yes

 ** S3Bucket **   <a name="Kendra-Type-HookConfiguration-S3Bucket"></a>
Stores the original, raw documents or the structured, parsed documents before and after altering them\. For more information, see [Data contracts for Lambda functions](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html#cde-data-contracts-lambda)\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 63\.  
Pattern: `[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]`   
Required: Yes

## See Also<a name="API_HookConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/HookConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/HookConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/HookConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/HookConfiguration) 