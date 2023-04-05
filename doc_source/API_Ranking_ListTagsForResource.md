--------

--------

# ListTagsForResource<a name="API_Ranking_ListTagsForResource"></a>

Gets a list of tags associated with a specified resource\. A rescore execution plan is an example of a resource that can have tags associated with it\.

## Request Syntax<a name="API_Ranking_ListTagsForResource_RequestSyntax"></a>

```
{
   "ResourceARN": "string"
}
```

## Request Parameters<a name="API_Ranking_ListTagsForResource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ResourceARN](#API_Ranking_ListTagsForResource_RequestSyntax) **   <a name="Kendra-Ranking_ListTagsForResource-request-ResourceARN"></a>
The Amazon Resource Name \(ARN\) of the rescore execution plan to get a list of tags for\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1011\.  
Required: Yes

## Response Syntax<a name="API_Ranking_ListTagsForResource_ResponseSyntax"></a>

```
{
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Response Elements<a name="API_Ranking_ListTagsForResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Tags](#API_Ranking_ListTagsForResource_ResponseSyntax) **   <a name="Kendra-Ranking_ListTagsForResource-response-Tags"></a>
A list of tags associated with the rescore execution plan\.  
Type: Array of [Tag](API_Ranking_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.

## Errors<a name="API_Ranking_ListTagsForResource_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don’t have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra Intelligent Ranking service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceUnavailableException **   
The resource you want to use is unavailable\. Please check you have provided the correct resource information and try again\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra Intelligent Ranking service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_Ranking_ListTagsForResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-ranking-2022-10-19/ListTagsForResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/ListTagsForResource) 