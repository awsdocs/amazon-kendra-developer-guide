--------

--------

# DescribeFeaturedResultsSet<a name="API_DescribeFeaturedResultsSet"></a>

Gets information about a set of featured results\. Features results are placed above all other results for certain queries\. If there's an exact match of a query, then one or more specific documents are featured in the search results\.

## Request Syntax<a name="API_DescribeFeaturedResultsSet_RequestSyntax"></a>

```
{
   "FeaturedResultsSetId": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribeFeaturedResultsSet_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [FeaturedResultsSetId](#API_DescribeFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-request-FeaturedResultsSetId"></a>
The identifier of the set of featured results that you want to get information on\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[a-zA-Z-0-9]*`   
Required: Yes

 ** [IndexId](#API_DescribeFeaturedResultsSet_RequestSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-request-IndexId"></a>
The identifier of the index used for featuring results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeFeaturedResultsSet_ResponseSyntax"></a>

```
{
   "CreationTimestamp": number,
   "Description": "string",
   "FeaturedDocumentsMissing": [ 
      { 
         "Id": "string"
      }
   ],
   "FeaturedDocumentsWithMetadata": [ 
      { 
         "Id": "string",
         "Title": "string",
         "URI": "string"
      }
   ],
   "FeaturedResultsSetId": "string",
   "FeaturedResultsSetName": "string",
   "LastUpdatedTimestamp": number,
   "QueryTexts": [ "string" ],
   "Status": "string"
}
```

## Response Elements<a name="API_DescribeFeaturedResultsSet_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreationTimestamp](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-CreationTimestamp"></a>
The Unix timestamp when the set of the featured results was created\.  
Type: Long

 ** [Description](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-Description"></a>
The description for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [FeaturedDocumentsMissing](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-FeaturedDocumentsMissing"></a>
The list of document IDs that don't exist but you have specified as featured documents\. Amazon Kendra cannot feature these documents if they don't exist in the index\. You can check the status of a document and its ID or check for documents with status errors using the [BatchGetDocumentStatus](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchGetDocumentStatus.html) API\.  
Type: Array of [FeaturedDocumentMissing](API_FeaturedDocumentMissing.md) objects

 ** [FeaturedDocumentsWithMetadata](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-FeaturedDocumentsWithMetadata"></a>
The list of document IDs for the documents you want to feature with their metadata information\. For more information on the list of featured documents, see [FeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_FeaturedResultsSet.html)\.  
Type: Array of [FeaturedDocumentWithMetadata](API_FeaturedDocumentWithMetadata.md) objects

 ** [FeaturedResultsSetId](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-FeaturedResultsSetId"></a>
The identifier of the set of featured results\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `^[a-zA-Z-0-9]*` 

 ** [FeaturedResultsSetName](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-FeaturedResultsSetName"></a>
The name for the set of featured results\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][ a-zA-Z0-9_-]*` 

 ** [LastUpdatedTimestamp](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-LastUpdatedTimestamp"></a>
The timestamp when the set of featured results was last updated\.  
Type: Long

 ** [QueryTexts](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-QueryTexts"></a>
The list of queries for featuring results\. For more information on the list of queries, see [FeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_FeaturedResultsSet.html)\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 49 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.

 ** [Status](#API_DescribeFeaturedResultsSet_ResponseSyntax) **   <a name="Kendra-DescribeFeaturedResultsSet-response-Status"></a>
The current status of the set of featured results\. When the value is `ACTIVE`, featured results are ready for use\. You can still configure your settings before setting the status to `ACTIVE`\. You can set the status to `ACTIVE` or `INACTIVE` using the [UpdateFeaturedResultsSet](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateFeaturedResultsSet.html) API\. The queries you specify for featured results must be unique per featured results set for each index, whether the status is `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | INACTIVE` 

## Errors<a name="API_DescribeFeaturedResultsSet_Errors"></a>

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

## See Also<a name="API_DescribeFeaturedResultsSet_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeFeaturedResultsSet) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeFeaturedResultsSet) 