--------

--------

# DocumentAttributeCondition<a name="API_DocumentAttributeCondition"></a>

The condition used for the target document attribute or metadata field when ingesting documents into Amazon Kendra\. You use this with [DocumentAttributeTarget to apply the condition](https://docs.aws.amazon.com/kendra/latest/dg/API_DocumentAttributeTarget.html)\.

For example, you can create the 'Department' target field and have it prefill department names associated with the documents based on information in the 'Source\_URI' field\. Set the condition that if the 'Source\_URI' field contains 'financial' in its URI value, then prefill the target field 'Department' with the target value 'Finance' for the document\.

Amazon Kendra cannot create a target field if it has not already been created as an index field\. After you create your index field, you can create a document metadata field using `DocumentAttributeTarget`\. Amazon Kendra then will map your newly created metadata field to your index field\.

## Contents<a name="API_DocumentAttributeCondition_Contents"></a>

 ** ConditionDocumentAttributeKey **   <a name="Kendra-Type-DocumentAttributeCondition-ConditionDocumentAttributeKey"></a>
The identifier of the document attribute used for the condition\.  
For example, 'Source\_URI' could be an identifier for the attribute or metadata field that contains source URIs associated with the documents\.  
Amazon Kendra currently does not support `_document_body` as an attribute key used for the condition\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[a-zA-Z0-9_][a-zA-Z0-9_-]*`   
Required: Yes

 ** ConditionOnValue **   <a name="Kendra-Type-DocumentAttributeCondition-ConditionOnValue"></a>
The value used by the operator\.  
For example, you can specify the value 'financial' for strings in the 'Source\_URI' field that partially match or contain this value\.  
Type: [DocumentAttributeValue](API_DocumentAttributeValue.md) object  
Required: No

 ** Operator **   <a name="Kendra-Type-DocumentAttributeCondition-Operator"></a>
The condition operator\.  
For example, you can use 'Contains' to partially match a string\.  
Type: String  
Valid Values:` GreaterThan | GreaterThanOrEquals | LessThan | LessThanOrEquals | Equals | NotEquals | Contains | NotContains | Exists | NotExists | BeginsWith`   
Required: Yes

## See Also<a name="API_DocumentAttributeCondition_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DocumentAttributeCondition) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DocumentAttributeCondition) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DocumentAttributeCondition) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DocumentAttributeCondition) 