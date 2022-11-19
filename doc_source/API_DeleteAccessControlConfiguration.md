--------

--------

# DeleteAccessControlConfiguration<a name="API_DeleteAccessControlConfiguration"></a>

Deletes an access control configuration that you created for your documents in an index\. This includes user and group access information for your documents\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.

## Request Syntax<a name="API_DeleteAccessControlConfiguration_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DeleteAccessControlConfiguration_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_DeleteAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-DeleteAccessControlConfiguration-request-Id"></a>
The identifier of the access control configuration you want to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9-]+`   
Required: Yes

 ** [IndexId](#API_DeleteAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-DeleteAccessControlConfiguration-request-IndexId"></a>
The identifier of the index for an access control configuration\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Elements<a name="API_DeleteAccessControlConfiguration_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteAccessControlConfiguration_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistences with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [ Support](http://aws.amazon.com/aws.amazon.com/contact-us) for help\.  
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

## See Also<a name="API_DeleteAccessControlConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DeleteAccessControlConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DeleteAccessControlConfiguration) 