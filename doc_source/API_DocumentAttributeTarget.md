--------

--------

# DocumentAttributeTarget<a name="API_DocumentAttributeTarget"></a>

The target document attribute or metadata field you want to alter when ingesting documents into Amazon Kendra\.

For example, you can delete customer identification numbers associated with the documents, stored in the document metadata field called 'Customer\_ID'\. You set the target key as 'Customer\_ID' and the deletion flag to `TRUE`\. This removes all customer ID values in the field 'Customer\_ID'\. This would scrub personally identifiable information from each document's metadata\.

Amazon Kendra cannot create a target field if it has not already been created as an index field\. After you create your index field, you can create a document metadata field using `DocumentAttributeTarget`\. Amazon Kendra then will map your newly created metadata field to your index field\.

You can also use this with [DocumentAttributeCondition](https://docs.aws.amazon.com/kendra/latest/dg/API_DocumentAttributeCondition.html)\.

## Contents<a name="API_DocumentAttributeTarget_Contents"></a>

 ** TargetDocumentAttributeKey **   <a name="Kendra-Type-DocumentAttributeTarget-TargetDocumentAttributeKey"></a>
The identifier of the target document attribute or metadata field\.  
For example, 'Department' could be an identifier for the target attribute or metadata field that includes the department names associated with the documents\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[a-zA-Z0-9_][a-zA-Z0-9_-]*`   
Required: No

 ** TargetDocumentAttributeValue **   <a name="Kendra-Type-DocumentAttributeTarget-TargetDocumentAttributeValue"></a>
The target value you want to create for the target attribute\.  
For example, 'Finance' could be the target value for the target attribute key 'Department'\.  
Type: [DocumentAttributeValue](API_DocumentAttributeValue.md) object  
Required: No

 ** TargetDocumentAttributeValueDeletion **   <a name="Kendra-Type-DocumentAttributeTarget-TargetDocumentAttributeValueDeletion"></a>
 `TRUE` to delete the existing target value for your specified target attribute key\. You cannot create a target value and set this to `TRUE`\. To create a target value \(`TargetDocumentAttributeValue`\), set this to `FALSE`\.  
Type: Boolean  
Required: No

## See Also<a name="API_DocumentAttributeTarget_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DocumentAttributeTarget) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DocumentAttributeTarget) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DocumentAttributeTarget) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DocumentAttributeTarget) 