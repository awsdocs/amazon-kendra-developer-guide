--------

--------

# StartDataSourceSyncJob<a name="API_StartDataSourceSyncJob"></a>

Starts a synchronization job for a data source connector\. If a synchronization job is already in progress, Amazon Kendra returns a `ResourceInUseException` exception\.

## Request Syntax<a name="API_StartDataSourceSyncJob_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_StartDataSourceSyncJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_StartDataSourceSyncJob_RequestSyntax) **   <a name="Kendra-StartDataSourceSyncJob-request-Id"></a>
The identifier of the data source connector to synchronize\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [IndexId](#API_StartDataSourceSyncJob_RequestSyntax) **   <a name="Kendra-StartDataSourceSyncJob-request-IndexId"></a>
The identifier of the index used with the data source connector\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_StartDataSourceSyncJob_ResponseSyntax"></a>

```
{
   "ExecutionId": "string"
}
```

## Response Elements<a name="API_StartDataSourceSyncJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ExecutionId](#API_StartDataSourceSyncJob_ResponseSyntax) **   <a name="Kendra-StartDataSourceSyncJob-response-ExecutionId"></a>
Identifies a particular synchronization job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.

## Errors<a name="API_StartDataSourceSyncJob_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistences with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceInUseException **   
The resource you want to use is currently in use\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
The resource you want to use doesn’t exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_StartDataSourceSyncJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/StartDataSourceSyncJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/StartDataSourceSyncJob) 