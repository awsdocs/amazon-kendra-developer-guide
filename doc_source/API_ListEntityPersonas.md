--------

--------

# ListEntityPersonas<a name="API_ListEntityPersonas"></a>

Lists specific permissions of users and groups with access to your Amazon Kendra experience\.

## Request Syntax<a name="API_ListEntityPersonas_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListEntityPersonas_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_ListEntityPersonas_RequestSyntax) **   <a name="Kendra-ListEntityPersonas-request-Id"></a>
The identifier of your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [IndexId](#API_ListEntityPersonas_RequestSyntax) **   <a name="Kendra-ListEntityPersonas-request-IndexId"></a>
The identifier of the index for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [MaxResults](#API_ListEntityPersonas_RequestSyntax) **   <a name="Kendra-ListEntityPersonas-request-MaxResults"></a>
The maximum number of returned users or groups\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListEntityPersonas_RequestSyntax) **   <a name="Kendra-ListEntityPersonas-request-NextToken"></a>
If the previous response was incomplete \(because there is more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of users or groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Required: No

## Response Syntax<a name="API_ListEntityPersonas_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "SummaryItems": [ 
      { 
         "CreatedAt": number,
         "EntityId": "string",
         "Persona": "string",
         "UpdatedAt": number
      }
   ]
}
```

## Response Elements<a name="API_ListEntityPersonas_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListEntityPersonas_ResponseSyntax) **   <a name="Kendra-ListEntityPersonas-response-NextToken"></a>
If the response is truncated, Amazon Kendra returns this token, which you can use in a later request to retrieve the next set of users or groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.

 ** [SummaryItems](#API_ListEntityPersonas_ResponseSyntax) **   <a name="Kendra-ListEntityPersonas-response-SummaryItems"></a>
An array of summary information for one or more users or groups\.  
Type: Array of [PersonasSummary](API_PersonasSummary.md) objects

## Errors<a name="API_ListEntityPersonas_Errors"></a>

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

## See Also<a name="API_ListEntityPersonas_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListEntityPersonas) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListEntityPersonas) 