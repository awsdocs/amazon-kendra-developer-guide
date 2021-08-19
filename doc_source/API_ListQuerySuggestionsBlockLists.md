--------

--------

# ListQuerySuggestionsBlockLists<a name="API_ListQuerySuggestionsBlockLists"></a>

Lists the block lists used for query suggestions for an index\.

For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.

## Request Syntax<a name="API_ListQuerySuggestionsBlockLists_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListQuerySuggestionsBlockLists_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [IndexId](#API_ListQuerySuggestionsBlockLists_RequestSyntax) **   <a name="Kendra-ListQuerySuggestionsBlockLists-request-IndexId"></a>
The identifier of the index for a list of all block lists that exist for that index\.  
For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [MaxResults](#API_ListQuerySuggestionsBlockLists_RequestSyntax) **   <a name="Kendra-ListQuerySuggestionsBlockLists-request-MaxResults"></a>
The maximum number of block lists to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListQuerySuggestionsBlockLists_RequestSyntax) **   <a name="Kendra-ListQuerySuggestionsBlockLists-request-NextToken"></a>
If the previous response was incomplete \(because there is more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of block lists \(`BlockListSummaryItems`\)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

## Response Syntax<a name="API_ListQuerySuggestionsBlockLists_ResponseSyntax"></a>

```
{
   "BlockListSummaryItems": [ 
      { 
         "CreatedAt": number,
         "Id": "string",
         "ItemCount": number,
         "Name": "string",
         "Status": "string",
         "UpdatedAt": number
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListQuerySuggestionsBlockLists_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [BlockListSummaryItems](#API_ListQuerySuggestionsBlockLists_ResponseSyntax) **   <a name="Kendra-ListQuerySuggestionsBlockLists-response-BlockListSummaryItems"></a>
Summary items for a block list\.  
This includes summary items on the block list ID, block list name, when the block list was created, when the block list was last updated, and the count of block words/phrases in the block list\.  
For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.  
Type: Array of [QuerySuggestionsBlockListSummary](API_QuerySuggestionsBlockListSummary.md) objects

 ** [NextToken](#API_ListQuerySuggestionsBlockLists_ResponseSyntax) **   <a name="Kendra-ListQuerySuggestionsBlockLists-response-NextToken"></a>
If the response is truncated, Amazon Kendra returns this token that you can use in the subsequent request to retrieve the next set of block lists\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

## Errors<a name="API_ListQuerySuggestionsBlockLists_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **AccessDeniedException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
  
HTTP Status Code: 400

## See Also<a name="API_ListQuerySuggestionsBlockLists_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListQuerySuggestionsBlockLists) 