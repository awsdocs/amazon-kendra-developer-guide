--------

--------

# ClearQuerySuggestions<a name="API_ClearQuerySuggestions"></a>

Clears existing query suggestions from an index\.

This deletes existing suggestions only, not the queries in the query log\. After you clear suggestions, Amazon Kendra learns new suggestions based on new queries added to the query log from the time you cleared suggestions\. If you do not see any new suggestions, then please allow Amazon Kendra to collect enough queries to learn new suggestions\.

## Request Syntax<a name="API_ClearQuerySuggestions_RequestSyntax"></a>

```
{
   "IndexId": "string"
}
```

## Request Parameters<a name="API_ClearQuerySuggestions_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [IndexId](#API_ClearQuerySuggestions_RequestSyntax) **   <a name="Kendra-ClearQuerySuggestions-request-IndexId"></a>
The identifier of the index you want to clear query suggestions from\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Elements<a name="API_ClearQuerySuggestions_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_ClearQuerySuggestions_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **AccessDeniedException**   
  
HTTP Status Code: 400

 **ConflictException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
  
HTTP Status Code: 400

## See Also<a name="API_ClearQuerySuggestions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ClearQuerySuggestions) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ClearQuerySuggestions) 