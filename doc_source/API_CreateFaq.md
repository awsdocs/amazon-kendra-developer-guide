--------

--------

# CreateFaq<a name="API_CreateFaq"></a>

Creates an new set of frequently asked question \(FAQ\) questions and answers\.

## Request Syntax<a name="API_CreateFaq_RequestSyntax"></a>

```
{
   "ClientToken": "string",
   "Description": "string",
   "FileFormat": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string",
   "S3Path": { 
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

## Request Parameters<a name="API_CreateFaq_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ ClientToken ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-ClientToken"></a>
=======
 ** [ClientToken](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-ClientToken"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A token that you provide to identify the request to create a FAQ\. Multiple calls to the `CreateFaqRequest` operation with the same client token will create only one FAQ\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

<<<<<<< HEAD
 ** [ Description ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Description"></a>
=======
 ** [Description](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Description"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A description of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** [ FileFormat ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-FileFormat"></a>
=======
 ** [FileFormat](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-FileFormat"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The format of the input file\. You can choose between a basic CSV format, a CSV format that includes customs attributes in a header, and a JSON format that includes custom attributes\.  
The format must match the format of the file stored in the S3 bucket identified in the `S3Path` parameter\.  
For more information, see [Adding questions and answers](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html)\.  
Type: String  
Valid Values:` CSV | CSV_WITH_HEADER | JSON`   
Required: No

<<<<<<< HEAD
 ** [ IndexId ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-IndexId"></a>
=======
 ** [IndexId](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the index that contains the FAQ\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ Name ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Name"></a>
=======
 ** [Name](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name that should be associated with the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ RoleArn ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-RoleArn"></a>
=======
 ** [RoleArn](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-RoleArn"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Amazon Resource Name \(ARN\) of a role with permission to access the S3 bucket that contains the FAQs\. For more information, see [IAM Roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

<<<<<<< HEAD
 ** [ S3Path ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-S3Path"></a>
The S3 location of the FAQ input data\.  
Type: [ S3Path ](API_S3Path.md) object  
Required: Yes

 ** [ Tags ](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Tags"></a>
A list of key\-value pairs that identify the FAQ\. You can use the tags to identify and organize your resources and to control access to resources\.  
Type: Array of [ Tag ](API_Tag.md) objects  
=======
 ** [S3Path](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-S3Path"></a>
The S3 location of the FAQ input data\.  
Type: [S3Path](API_S3Path.md) object  
Required: Yes

 ** [Tags](#API_CreateFaq_RequestSyntax) **   <a name="Kendra-CreateFaq-request-Tags"></a>
A list of key\-value pairs that identify the FAQ\. You can use the tags to identify and organize your resources and to control access to resources\.  
Type: Array of [Tag](API_Tag.md) objects  
>>>>>>> parent of 2b1c178 (updating tutorial)
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_CreateFaq_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateFaq_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ Id ](#API_CreateFaq_ResponseSyntax) **   <a name="Kendra-CreateFaq-response-Id"></a>
=======
 ** [Id](#API_CreateFaq_ResponseSyntax) **   <a name="Kendra-CreateFaq-response-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

## Errors<a name="API_CreateFaq_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

<<<<<<< HEAD
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
=======
 **AccessDeniedException**   
  
HTTP Status Code: 400

 **ConflictException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ServiceQuotaExceededException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
>>>>>>> parent of 2b1c178 (updating tutorial)
  
HTTP Status Code: 400

## See Also<a name="API_CreateFaq_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateFaq) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateFaq) 