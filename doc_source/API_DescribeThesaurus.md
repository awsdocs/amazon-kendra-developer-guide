--------

--------

# DescribeThesaurus<a name="API_DescribeThesaurus"></a>

Describes an existing Amazon Kendra thesaurus\.

## Request Syntax<a name="API_DescribeThesaurus_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribeThesaurus_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_DescribeThesaurus_RequestSyntax) **   <a name="Kendra-DescribeThesaurus-request-Id"></a>
The identifier of the thesaurus to describe\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [IndexId](#API_DescribeThesaurus_RequestSyntax) **   <a name="Kendra-DescribeThesaurus-request-IndexId"></a>
The identifier of the index associated with the thesaurus to describe\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeThesaurus_ResponseSyntax"></a>

```
{
   "CreatedAt": number,
   "Description": "string",
   "ErrorMessage": "string",
   "FileSizeBytes": number,
   "Id": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string",
   "SourceS3Path": { 
      "Bucket": "string",
      "Key": "string"
   },
   "Status": "string",
   "SynonymRuleCount": number,
   "TermCount": number,
   "UpdatedAt": number
}
```

## Response Elements<a name="API_DescribeThesaurus_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CreatedAt](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-CreatedAt"></a>
The Unix datetime that the thesaurus was created\.  
Type: Timestamp

 ** [Description](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-Description"></a>
The thesaurus description\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [ErrorMessage](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-ErrorMessage"></a>
When the `Status` field value is `FAILED`, the `ErrorMessage` field provides more information\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

 ** [FileSizeBytes](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-FileSizeBytes"></a>
The size of the thesaurus file in bytes\.  
Type: Long

 ** [Id](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-Id"></a>
The identifier of the thesaurus\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [IndexId](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-IndexId"></a>
The identifier of the index associated with the thesaurus to describe\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

 ** [Name](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-Name"></a>
The thesaurus name\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [RoleArn](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-RoleArn"></a>
An AWS Identity and Access Management \(IAM\) role that gives Amazon Kendra permissions to access thesaurus file specified in `SourceS3Path`\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

 ** [SourceS3Path](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-SourceS3Path"></a>
Information required to find a specific file in an Amazon S3 bucket\.  
Type: [S3Path](API_S3Path.md) object

 ** [Status](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-Status"></a>
The current status of the thesaurus\. When the value is `ACTIVE`, queries are able to use the thesaurus\. If the `Status` field value is `FAILED`, the `ErrorMessage` field provides more information\.   
If the status is `ACTIVE_BUT_UPDATE_FAILED`, it means that Amazon Kendra could not ingest the new thesaurus file\. The old thesaurus file is still active\.   
Type: String  
Valid Values:` CREATING | ACTIVE | DELETING | UPDATING | ACTIVE_BUT_UPDATE_FAILED | FAILED` 

 ** [SynonymRuleCount](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-SynonymRuleCount"></a>
The number of synonym rules in the thesaurus file\.  
Type: Long

 ** [TermCount](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-TermCount"></a>
The number of unique terms in the thesaurus file\. For example, the synonyms `a,b,c` and `a=>d`, the term count would be 4\.   
Type: Long

 ** [UpdatedAt](#API_DescribeThesaurus_ResponseSyntax) **   <a name="Kendra-DescribeThesaurus-response-UpdatedAt"></a>
The Unix datetime that the thesaurus was last updated\.  
Type: Timestamp

## Errors<a name="API_DescribeThesaurus_Errors"></a>

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

## See Also<a name="API_DescribeThesaurus_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeThesaurus) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeThesaurus) 