--------

--------

# ListFaqs<a name="API_ListFaqs"></a>

Gets a list of FAQ lists associated with an index\.

## Request Syntax<a name="API_ListFaqs_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListFaqs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ IndexId ](#API_ListFaqs_RequestSyntax) **   <a name="Kendra-ListFaqs-request-IndexId"></a>
=======
 ** [IndexId](#API_ListFaqs_RequestSyntax) **   <a name="Kendra-ListFaqs-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The index that contains the FAQ lists\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ MaxResults ](#API_ListFaqs_RequestSyntax) **   <a name="Kendra-ListFaqs-request-MaxResults"></a>
=======
 ** [MaxResults](#API_ListFaqs_RequestSyntax) **   <a name="Kendra-ListFaqs-request-MaxResults"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The maximum number of FAQs to return in the response\. If there are fewer results in the list, this response contains only the actual results\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

<<<<<<< HEAD
 ** [ NextToken ](#API_ListFaqs_RequestSyntax) **   <a name="Kendra-ListFaqs-request-NextToken"></a>
=======
 ** [NextToken](#API_ListFaqs_RequestSyntax) **   <a name="Kendra-ListFaqs-request-NextToken"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
If the previous response was incomplete \(because there is more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of FAQs\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

## Response Syntax<a name="API_ListFaqs_ResponseSyntax"></a>

```
{
   "FaqSummaryItems": [ 
      { 
         "CreatedAt": number,
         "FileFormat": "string",
         "Id": "string",
         "Name": "string",
         "Status": "string",
         "UpdatedAt": number
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListFaqs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ FaqSummaryItems ](#API_ListFaqs_ResponseSyntax) **   <a name="Kendra-ListFaqs-response-FaqSummaryItems"></a>
information about the FAQs associated with the specified index\.  
Type: Array of [ FaqSummary ](API_FaqSummary.md) objects

 ** [ NextToken ](#API_ListFaqs_ResponseSyntax) **   <a name="Kendra-ListFaqs-response-NextToken"></a>
=======
 ** [FaqSummaryItems](#API_ListFaqs_ResponseSyntax) **   <a name="Kendra-ListFaqs-response-FaqSummaryItems"></a>
information about the FAQs associated with the specified index\.  
Type: Array of [FaqSummary](API_FaqSummary.md) objects

 ** [NextToken](#API_ListFaqs_ResponseSyntax) **   <a name="Kendra-ListFaqs-response-NextToken"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
If the response is truncated, Amazon Kendra returns this token that you can use in the subsequent request to retrieve the next set of FAQs\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

## Errors<a name="API_ListFaqs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

<<<<<<< HEAD
 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
=======
 **AccessDeniedException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
>>>>>>> parent of 2b1c178 (updating tutorial)
  
HTTP Status Code: 400

## See Also<a name="API_ListFaqs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListFaqs) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListFaqs) 