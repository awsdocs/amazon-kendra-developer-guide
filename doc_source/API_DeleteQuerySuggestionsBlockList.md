--------

--------

# DeleteQuerySuggestionsBlockList<a name="API_DeleteQuerySuggestionsBlockList"></a>

Deletes a block list used for query suggestions for an index\.

A deleted block list might not take effect right away\. Amazon Kendra needs to refresh the entire suggestions list to add back the queries that were previously blocked\.

## Request Syntax<a name="API_DeleteQuerySuggestionsBlockList_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DeleteQuerySuggestionsBlockList_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_DeleteQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-DeleteQuerySuggestionsBlockList-request-Id"></a>
The unique identifier of the block list that needs to be deleted\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [IndexId](#API_DeleteQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-DeleteQuerySuggestionsBlockList-request-IndexId"></a>
The identifier of the you want to delete a block list from\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Elements<a name="API_DeleteQuerySuggestionsBlockList_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteQuerySuggestionsBlockList_Errors"></a>

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

## See Also<a name="API_DeleteQuerySuggestionsBlockList_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DeleteQuerySuggestionsBlockList) 