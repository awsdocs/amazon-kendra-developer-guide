--------

--------

# ListThesauri<a name="API_ListThesauri"></a>

Lists the Amazon Kendra thesauri associated with an index\.

## Request Syntax<a name="API_ListThesauri_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListThesauri_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [IndexId](#API_ListThesauri_RequestSyntax) **   <a name="Kendra-ListThesauri-request-IndexId"></a>
The identifier of the index associated with the thesaurus to list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [MaxResults](#API_ListThesauri_RequestSyntax) **   <a name="Kendra-ListThesauri-request-MaxResults"></a>
The maximum number of thesauri to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListThesauri_RequestSyntax) **   <a name="Kendra-ListThesauri-request-NextToken"></a>
If the previous response was incomplete \(because there is more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of thesauri \(`ThesaurusSummaryItems`\)\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

## Response Syntax<a name="API_ListThesauri_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "ThesaurusSummaryItems": [ 
      { 
         "CreatedAt": number,
         "Id": "string",
         "Name": "string",
         "Status": "string",
         "UpdatedAt": number
      }
   ]
}
```

## Response Elements<a name="API_ListThesauri_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListThesauri_ResponseSyntax) **   <a name="Kendra-ListThesauri-response-NextToken"></a>
If the response is truncated, Amazon Kendra returns this token that you can use in the subsequent request to retrieve the next set of thesauri\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

 ** [ThesaurusSummaryItems](#API_ListThesauri_ResponseSyntax) **   <a name="Kendra-ListThesauri-response-ThesaurusSummaryItems"></a>
An array of summary information for one or more thesauruses\.  
Type: Array of [ThesaurusSummary](API_ThesaurusSummary.md) objects

## Errors<a name="API_ListThesauri_Errors"></a>

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

## See Also<a name="API_ListThesauri_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListThesauri) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListThesauri) 