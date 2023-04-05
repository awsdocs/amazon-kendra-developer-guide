--------

--------

# ListAccessControlConfigurations<a name="API_ListAccessControlConfigurations"></a>

Lists one or more access control configurations for an index\. This includes user and group access information for your documents\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.

## Request Syntax<a name="API_ListAccessControlConfigurations_RequestSyntax"></a>

```
{
   "IndexId": "string",
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListAccessControlConfigurations_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [IndexId](#API_ListAccessControlConfigurations_RequestSyntax) **   <a name="Kendra-ListAccessControlConfigurations-request-IndexId"></a>
The identifier of the index for the access control configuration\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [MaxResults](#API_ListAccessControlConfigurations_RequestSyntax) **   <a name="Kendra-ListAccessControlConfigurations-request-MaxResults"></a>
The maximum number of access control configurations to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NextToken](#API_ListAccessControlConfigurations_RequestSyntax) **   <a name="Kendra-ListAccessControlConfigurations-request-NextToken"></a>
If the previous response was incomplete \(because there's more data to retrieve\), Amazon Kendra returns a pagination token in the response\. You can use this pagination token to retrieve the next set of access control configurations\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

## Response Syntax<a name="API_ListAccessControlConfigurations_ResponseSyntax"></a>

```
{
   "AccessControlConfigurations": [ 
      { 
         "Id": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListAccessControlConfigurations_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AccessControlConfigurations](#API_ListAccessControlConfigurations_ResponseSyntax) **   <a name="Kendra-ListAccessControlConfigurations-response-AccessControlConfigurations"></a>
The details of your access control configurations\.  
Type: Array of [AccessControlConfigurationSummary](API_AccessControlConfigurationSummary.md) objects

 ** [NextToken](#API_ListAccessControlConfigurations_ResponseSyntax) **   <a name="Kendra-ListAccessControlConfigurations-response-NextToken"></a>
If the response is truncated, Amazon Kendra returns this token, which you can use in the subsequent request to retrieve the next set of access control configurations\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.

## Errors<a name="API_ListAccessControlConfigurations_Errors"></a>

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

## See Also<a name="API_ListAccessControlConfigurations_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/ListAccessControlConfigurations) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ListAccessControlConfigurations) 