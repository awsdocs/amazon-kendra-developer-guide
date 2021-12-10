--------

--------

# CreateQuerySuggestionsBlockList<a name="API_CreateQuerySuggestionsBlockList"></a>

Creates a block list to exlcude certain queries from suggestions\.

Any query that contains words or phrases specified in the block list is blocked or filtered out from being shown as a suggestion\.

You need to provide the file location of your block list text file in your S3 bucket\. In your text file, enter each block word or phrase on a separate line\.

For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.

 `CreateQuerySuggestionsBlockList` is currently not supported in the AWS GovCloud \(US\-West\) region\.

## Request Syntax<a name="API_CreateQuerySuggestionsBlockList_RequestSyntax"></a>

```
{
   "ClientToken": "string",
   "Description": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string",
   "SourceS3Path": { 
      "Bucket": "string",
      "Key": "string"
   },
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_CreateQuerySuggestionsBlockList_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ ClientToken ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-ClientToken"></a>
A token that you provide to identify the request to create a query suggestions block list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

 ** [ Description ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-Description"></a>
A user\-friendly description for the block list\.  
For example, the description "List of all offensive words that can appear in user queries and need to be blocked from suggestions\."  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [ IndexId ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-IndexId"></a>
The identifier of the index you want to create a query suggestions block list for\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [ Name ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-Name"></a>
A user friendly name for the block list\.  
For example, the block list named 'offensive\-words' includes all offensive words that could appear in user queries and need to be blocked from suggestions\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z0-9](-*[a-zA-Z0-9])*`   
Required: Yes

 ** [ RoleArn ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-RoleArn"></a>
The IAM \(Identity and Access Management\) role used by Amazon Kendra to access the block list text file in your S3 bucket\.  
You need permissions to the role ARN \(Amazon Resource Name\)\. The role needs S3 read permissions to your file in S3 and needs to give STS \(Security Token Service\) assume role permissions to Amazon Kendra\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** [ SourceS3Path ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-SourceS3Path"></a>
The S3 path to your block list text file in your S3 bucket\.  
Each block word or phrase should be on a separate line in a text file\.  
For information on the current quota limits for block lists, see [Quotas for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html)\.  
Type: [ S3Path ](API_S3Path.md) object  
Required: Yes

 ** [ Tags ](#API_CreateQuerySuggestionsBlockList_RequestSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-request-Tags"></a>
A tag that you can assign to a block list that categorizes the block list\.  
Type: Array of [ Tag ](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_CreateQuerySuggestionsBlockList_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateQuerySuggestionsBlockList_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ Id ](#API_CreateQuerySuggestionsBlockList_ResponseSyntax) **   <a name="Kendra-CreateQuerySuggestionsBlockList-response-Id"></a>
The unique identifier of the created block list\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

## Errors<a name="API_CreateQuerySuggestionsBlockList_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** ConflictException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ServiceQuotaExceededException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
  
HTTP Status Code: 400

## See Also<a name="API_CreateQuerySuggestionsBlockList_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateQuerySuggestionsBlockList) 