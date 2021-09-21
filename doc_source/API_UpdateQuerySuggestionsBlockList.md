--------

--------

# UpdateQuerySuggestionsBlockList<a name="API_UpdateQuerySuggestionsBlockList"></a>

Updates a block list used for query suggestions for an index\.

Updates to a block list might not take effect right away\. Amazon Kendra needs to refresh the entire suggestions list to apply any updates to the block list\. Other changes not related to the block list apply immediately\.

If a block list is updating, then you need to wait for the first update to finish before submitting another update\.

Amazon Kendra supports partial updates, so you only need to provide the fields you want to update\.

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

 ** [ Description ](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-Description"></a>
The description for a block list\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [ Id ](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-Id"></a>
The unique identifier of a block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [ IndexId ](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-IndexId"></a>
The identifier of the index for a block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [ Name ](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-Name"></a>
The name of a block list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z0-9](-*[a-zA-Z0-9])*`   
Required: No

 ** [ RoleArn ](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-RoleArn"></a>
The IAM \(Identity and Access Management\) role used to access the block list text file in S3\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** [ SourceS3Path ](#API_UpdateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-UpdateQuerySuggestionsBlockList-request-SourceS3Path"></a>
The S3 path where your block list text file sits in S3\.  
If you update your block list and provide the same path to the block list text file in S3, then Amazon Kendra reloads the file to refresh the block list\. Amazon Kendra does not automatically refresh your block list\. You need to call the `UpdateQuerySuggestionsBlockList` API to refresh you block list\.  
If you update your block list, then Amazon Kendra asynchronously refreshes all query suggestions with the latest content in the S3 file\. This means changes might not take effect immediately\.  
Type: [ S3Path ](API_S3Path.md) object  
Required: No

## Response Elements<a name="API_UpdateQuerySuggestionsBlockList_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateQuerySuggestionsBlockList_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** ConflictException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
  
HTTP Status Code: 400

## See Also<a name="API_UpdateQuerySuggestionsBlockList_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateQuerySuggestionsBlockList) 