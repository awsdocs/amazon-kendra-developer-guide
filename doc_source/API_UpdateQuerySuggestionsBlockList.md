--------

--------

# UpdateQuerySuggestionsBlockList<a name="API_UpdateQuerySuggestionsBlockList"></a>

Updates a block list used for query suggestions for an index\.

Updates to a block list might not take effect right away\. Amazon Kendra needs to refresh the entire suggestions list to apply any updates to the block list\. Other changes not related to the block list apply immediately\.

If a block list is updating, then you need to wait for the first update to finish before submitting another update\.

Amazon Kendra supports partial updates, so you only need to provide the fields you want to update\.

 `UpdateQuerySuggestionsBlockList` is currently not supported in the AWS GovCloud \(US\-West\) region\.

## Request Syntax<a name="API_UpdateQuerySuggestionsBlockList_RequestSyntax"></a>

```
{
   "Description": "string",
   "Id": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string",
   "SourceS3Path": { 
      "Bucket": "string",
      "Key": "string"
   }
}
```

## Request Parameters<a name="API_UpdateQuerySuggestionsBlockList_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Description](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-Description"></a>
A new description for the block list\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [Id](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-Id"></a>
The identifier of the block list you want to update\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [IndexId](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-IndexId"></a>
The identifier of the index for the block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [Name](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-Name"></a>
A new name for the block list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z0-9](-*[a-zA-Z0-9])*`   
Required: No

 ** [RoleArn](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-RoleArn"></a>
The IAM \(Identity and Access Management\) role used to access the block list text file in S3\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** [SourceS3Path](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-SourceS3Path"></a>
The S3 path where your block list text file sits in S3\.  
If you update your block list and provide the same path to the block list text file in S3, then Amazon Kendra reloads the file to refresh the block list\. Amazon Kendra does not automatically refresh your block list\. You need to call the `UpdateQuerySuggestionsBlockList` API to refresh you block list\.  
If you update your block list, then Amazon Kendra asynchronously refreshes all query suggestions with the latest content in the S3 file\. This means changes might not take effect immediately\.  
Type: [S3Path](API_S3Path.md) object  
Required: No

## Response Elements<a name="API_UpdateQuerySuggestionsBlockList_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateQuerySuggestionsBlockList_Errors"></a>

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

## See Also<a name="API_UpdateQuerySuggestionsBlockList_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 