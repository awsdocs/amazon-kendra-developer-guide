--------

--------

# BatchDeleteFeaturedResultsSet<a name="API_BatchDeleteFeaturedResultsSet"></a>

Removes one or more sets of featured results\. Features results are placed above all other results for certain queries\. If there's an exact match of a query, then one or more specific documents are featured in the search results\.

## Request Syntax<a name="API_BatchDeleteFeaturedResultsSet_RequestSyntax"></a>

```
{
   "FeaturedResultsSetIds": [ "string" ],
   "IndexId": "string"
}
```

## Request Parameters<a name="API_BatchDeleteFeaturedResultsSet_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [FeaturedResultsSetIds](#API_BatchDeleteFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-BatchDeleteFeaturedResultsSet-request-FeaturedResultsSetIds"></a>
The identifiers of the featured results sets that you want to delete\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 50 items\.  
Length Constraints: Fixed length of 36\.  
Pattern: `^[a-zA-Z-0-9]*`   
Required: Yes

 ** [IndexId](#API_BatchDeleteFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-BatchDeleteFeaturedResultsSet-request-IndexId"></a>
The identifier of the index used for featuring results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_BatchDeleteFeaturedResultsSet_ResponseSyntax"></a>

```
{
   "Errors": [ 
      { 
         "ErrorCode": "string",
         "ErrorMessage": "string",
         "Id": "string"
      }
   ]
}
```

## Response Elements<a name="API_BatchDeleteFeaturedResultsSet_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Errors](#API_BatchDeleteFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-BatchDeleteFeaturedResultsSet-response-Errors"></a>
The list of errors for the featured results set IDs, explaining why they couldn't be removed from the index\.  
Type: Array of [BatchDeleteFeaturedResultsSetError](API_BatchDeleteFeaturedResultsSetError.md) objects

## Errors<a name="API_BatchDeleteFeaturedResultsSet_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
The resource you want to use doesn’t exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_BatchDeleteFeaturedResultsSet_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/BatchDeleteFeaturedResultsSet) 