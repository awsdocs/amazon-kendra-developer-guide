--------

--------

# CreateFeaturedResultsSet<a name="API_CreateFeaturedResultsSet"></a>

Creates a set of featured results to display at the top of the search results page\. Featured results are placed above all other results for certain queries\. You map specific queries to specific documents for featuring in the results\. If a query contains an exact match, then one or more specific documents are featured in the search results\.

You can create up to 50 sets of featured results per index\. You can request to increase this limit by contacting [Support](http://aws.amazon.com/contact-us/)\.

## Request Syntax<a name="API_CreateFeaturedResultsSet_RequestSyntax"></a>

```
{
   "ClientToken": "string",
   "Description": "string",
   "FeaturedDocuments": [ 
      { 
         "Id": "string"
      }
   ],
   "FeaturedResultsSetName": "string",
   "IndexId": "string",
   "QueryTexts": [ "string" ],
   "Status": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateFeaturedResultsSet_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ClientToken](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-ClientToken"></a>
A token that you provide to identify the request to create a set of featured results\. Multiple calls to the `CreateFeaturedResultsSet` API with the same client token will create only one featured results set\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

 ** [Description](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-Description"></a>
A description for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [FeaturedDocuments](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-FeaturedDocuments"></a>
A list of document IDs for the documents you want to feature at the top of the search results page\. For more information on the list of documents, see [FeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_FeaturedResultsSet.html)\.  
Type: Array of [FeaturedDocument](API_FeaturedDocument.md) objects  
Required: No

 ** [FeaturedResultsSetName](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-FeaturedResultsSetName"></a>
A name for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][ a-zA-Z0-9_-]*`   
Required: Yes

 ** [IndexId](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-IndexId"></a>
The identifier of the index that you want to use for featuring results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [QueryTexts](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-QueryTexts"></a>
A list of queries for featuring results\. For more information on the list of queries, see [FeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_FeaturedResultsSet.html)\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 49 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Required: No

 ** [Status](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-Status"></a>
The current status of the set of featured results\. When the value is `ACTIVE`, featured results are ready for use\. You can still configure your settings before setting the status to `ACTIVE`\. You can set the status to `ACTIVE` or `INACTIVE` using the [UpdateFeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateFeaturedResultsSet.html) API\. The queries you specify for featured results must be unique per featured results set for each index, whether the status is `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE`   
Required: No

 ** [Tags](#API_CreateFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-request-Tags"></a>
A list of key\-value pairs that identify or categorize the featured results set\. You can also use tags to help control access to the featured results set\. Tag keys and values can consist of Unicode letters, digits, white space, and any of the following symbols:\_ \. : / = \+ \- @\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_CreateFeaturedResultsSet_ResponseSyntax"></a>

```
{
   "FeaturedResultsSet": { 
      "CreationTimestamp": number,
      "Description": "string",
      "FeaturedDocuments": [ 
         { 
            "Id": "string"
         }
      ],
      "FeaturedResultsSetId": "string",
      "FeaturedResultsSetName": "string",
      "LastUpdatedTimestamp": number,
      "QueryTexts": [ "string" ],
      "Status": "string"
   }
}
```

## Response Elements<a name="API_CreateFeaturedResultsSet_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [FeaturedResultsSet](#API_CreateFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-CreateFeaturedResultsSet-response-FeaturedResultsSet"></a>
Information on the set of featured results\. This includes the identifier of the featured results set, whether the featured results set is active or inactive, when the featured results set was created, and more\.  
Type: [FeaturedResultsSet](API_FeaturedResultsSet.md) object

## Errors<a name="API_CreateFeaturedResultsSet_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistences with your resources and try again\.  
HTTP Status Code: 400

 ** FeaturedResultsConflictException **   
An error message with a list of conflicting queries used across different sets of featured results\. This occurred with the request for a new featured results set\. Check that the queries you specified for featured results are unique per featured results set for each index\.  
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

## See Also<a name="API_CreateFeaturedResultsSet_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateFeaturedResultsSet) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateFeaturedResultsSet) 