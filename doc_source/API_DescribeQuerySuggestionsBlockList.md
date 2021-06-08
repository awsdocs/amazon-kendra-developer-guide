--------

--------

# DescribeQuerySuggestionsBlockList<a name="API_DescribeQuerySuggestionsBlockList"></a>

Describes a block list used for query suggestions for an index\.

This is used to check the current settings that are applied to a block list\.

## Request Syntax<a name="API_DescribeQuerySuggestionsBlockList_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribeQuerySuggestionsBlockList_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_DescribeQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-request-Id"></a>
The unique identifier of the block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [IndexId](#API_DescribeQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-request-IndexId"></a>
The identifier of the index for the block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeQuerySuggestionsBlockList_ResponseSyntax"></a>

```
{
   "CreatedAt": number,
   "Description": "string",
   "ErrorMessage": "string",
   "FileSizeBytes": number,
   "Id": "string",
   "IndexId": "string",
   "ItemCount": number,
   "Name": "string",
   "RoleArn": "string",
   "SourceS3Path": { 
      "Bucket": "string",
      "Key": "string"
   },
   "Status": "string",
   "UpdatedAt": number
}
```

## Response Elements<a name="API_DescribeQuerySuggestionsBlockList_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreatedAt](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-CreatedAt"></a>
Shows the date\-time a block list for query suggestions was last created\.  
Type: Timestamp

 ** [Description](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-Description"></a>
Shows the description for the block list\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [ErrorMessage](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-ErrorMessage"></a>
Shows the error message with details when there are issues in processing the block list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

 ** [FileSizeBytes](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-FileSizeBytes"></a>
Shows the current size of the block list text file in S3\.  
Type: Long

 ** [Id](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-Id"></a>
Shows the unique identifier of the block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

 ** [IndexId](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-IndexId"></a>
Shows the identifier of the index for the block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

 ** [ItemCount](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-ItemCount"></a>
Shows the current number of valid, non\-empty words or phrases in the block list text file\.  
Type: Integer

 ** [Name](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-Name"></a>
Shows the name of the block list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z0-9](-*[a-zA-Z0-9])*` 

 ** [RoleArn](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-RoleArn"></a>
Shows the current IAM \(Identity and Access Management\) role used by Amazon Kendra to access the block list text file in S3\.  
The role needs S3 read permissions to your file in S3 and needs to give STS \(Security Token Service\) assume role permissions to Amazon Kendra\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

 ** [SourceS3Path](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-SourceS3Path"></a>
Shows the current S3 path to your block list text file in your S3 bucket\.  
Each block word or phrase should be on a separate line in a text file\.  
For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.  
Type: [S3Path](API_S3Path.md) object

 ** [Status](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-Status"></a>
Shows whether the current status of the block list is `ACTIVE` or `INACTIVE`\.  
Type: String  
Valid Values:` ACTIVE | CREATING | DELETING | UPDATING | ACTIVE_BUT_UPDATE_FAILED | FAILED` 

 ** [UpdatedAt](#API_DescribeQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-DescribeQuerySuggestionsBlockList-response-UpdatedAt"></a>
Shows the date\-time a block list for query suggestions was last updated\.  
Type: Timestamp

## Errors<a name="API_DescribeQuerySuggestionsBlockList_Errors"></a>

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

## See Also<a name="API_DescribeQuerySuggestionsBlockList_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeQuerySuggestionsBlockList) 