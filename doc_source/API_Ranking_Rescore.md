--------

--------

# Rescore<a name="API_Ranking_Rescore"></a>

Rescores or re\-ranks search results from a search service such as OpenSearch \(self managed\)\. You use the semantic search capabilities of Amazon Kendra Intelligent Ranking to improve the search service's results\.

## Request Syntax<a name="API_Ranking_Rescore_RequestSyntax"></a>

```
{
   "Documents": [ 
      { 
         "Body": "string",
         "GroupId": "string",
         "Id": "string",
         "OriginalScore": number,
         "Title": "string",
         "TokenizedBody": [ "string" ],
         "TokenizedTitle": [ "string" ]
      }
   ],
   "RescoreExecutionPlanId": "string",
   "SearchQuery": "string"
}
```

## Request Parameters<a name="API_Ranking_Rescore_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Documents](#API_Ranking_Rescore_RequestSyntax) **   <a name="Kendra-Ranking_Rescore-request-Documents"></a>
The list of documents for Amazon Kendra Intelligent Ranking to rescore or rank on\.  
Type: Array of [Document](API_Ranking_Document.md) objects  
Array Members: Minimum number of 1 item\.  
Required: Yes

 ** [RescoreExecutionPlanId](#API_Ranking_Rescore_RequestSyntax) **   <a name="Kendra-Ranking_Rescore-request-RescoreExecutionPlanId"></a>
The identifier of the rescore execution plan\. A rescore execution plan is an Amazon Kendra Intelligent Ranking resource used for provisioning the `Rescore` API\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [SearchQuery](#API_Ranking_Rescore_RequestSyntax) **   <a name="Kendra-Ranking_Rescore-request-SearchQuery"></a>
The input query from the search service\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Required: Yes

## Response Syntax<a name="API_Ranking_Rescore_ResponseSyntax"></a>

```
{
   "RescoreId": "string",
   "ResultItems": [ 
      { 
         "DocumentId": "string",
         "Score": number
      }
   ]
}
```

## Response Elements<a name="API_Ranking_Rescore_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [RescoreId](#API_Ranking_Rescore_ResponseSyntax) **   <a name="Kendra-Ranking_Rescore-response-RescoreId"></a>
The identifier associated with the scores that Amazon Kendra Intelligent Ranking gives to the results\. Amazon Kendra Intelligent Ranking rescores or re\-ranks the results for the search service\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]` 

 ** [ResultItems](#API_Ranking_Rescore_ResponseSyntax) **   <a name="Kendra-Ranking_Rescore-response-ResultItems"></a>
A list of result items for documents with new relevancy scores\. The results are in descending order\.  
Type: Array of [RescoreResultItem](API_Ranking_RescoreResultItem.md) objects  
Array Members: Minimum number of 1 item\.

## Errors<a name="API_Ranking_Rescore_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don’t have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistencies with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra Intelligent Ranking service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
The resource you want to use doesn't exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra Intelligent Ranking service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_Ranking_Rescore_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-ranking-2022-10-19/Rescore) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/Rescore) 