--------

--------

# ListFeaturedResultsSets<a name="API_ListFeaturedResultsSets"></a>

Lists all your sets of featured results for a given index\. Features results are placed above all other results for certain queries\. If there's an exact match of a query, then one or more specific documents are featured in the search results\.

## Request Syntax<a name="API_ListFeaturedResultsSets_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListFeaturedResultsSets_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [IndexId](#API_ListFeaturedResultsSets_RequestSyntax) **   <a name="Kendra-ListFeaturedResultsSets-request-IndexId"></a>
The identifier of the index used for featuring results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [MaxResults](#API_ListFeaturedResultsSets_RequestSyntax) **   <a name="Kendra-ListFeaturedResultsSets-request-MaxResults"></a>
The maximum number of featured results sets to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListFeaturedResultsSets_RequestSyntax) **   <a name="Kendra-ListFeaturedResultsSets-request-NextToken"></a>
If the response is truncated, Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of featured results sets\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

## Response Syntax<a name="API_ListFeaturedResultsSets_ResponseSyntax"></a>

```
{
   "FeaturedResultsSetSummaryItems": [ 
      { 
         "CreationTimestamp": number,
         "FeaturedResultsSetId": "string",
         "FeaturedResultsSetName": "string",
         "LastUpdatedTimestamp": number,
         "Status": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListFeaturedResultsSets_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [FeaturedResultsSetSummaryItems](#API_ListFeaturedResultsSets_ResponseSyntax) **   <a name="Kendra-ListFeaturedResultsSets-response-FeaturedResultsSetSummaryItems"></a>
An array of summary information for one or more featured results sets\.  
Type: Array of [FeaturedResultsSetSummary](API_FeaturedResultsSetSummary.md) objects

 ** [NextToken](#API_ListFeaturedResultsSets_ResponseSyntax) **   <a name="Kendra-ListFeaturedResultsSets-response-NextToken"></a>
If the response is truncated, Amazon Kendra returns a pagination token in the response\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

## Errors<a name="API_ListFeaturedResultsSets_Errors"></a>

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

## See Also<a name="API_ListFeaturedResultsSets_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListFeaturedResultsSets) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListFeaturedResultsSets) 