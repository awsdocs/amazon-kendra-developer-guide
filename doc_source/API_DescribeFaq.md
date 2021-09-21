--------

--------

# DescribeFaq<a name="API_DescribeFaq"></a>

Gets information about an FAQ list\.

## Request Syntax<a name="API_DescribeFaq_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribeFaq_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ Id ](#API_DescribeFaq_RequestSyntax) **   <a name="Kendra-DescribeFaq-request-Id"></a>
=======
 ** [Id](#API_DescribeFaq_RequestSyntax) **   <a name="Kendra-DescribeFaq-request-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ IndexId ](#API_DescribeFaq_RequestSyntax) **   <a name="Kendra-DescribeFaq-request-IndexId"></a>
=======
 ** [IndexId](#API_DescribeFaq_RequestSyntax) **   <a name="Kendra-DescribeFaq-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the index that contains the FAQ\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeFaq_ResponseSyntax"></a>

```
{
   "CreatedAt": number,
   "Description": "string",
   "ErrorMessage": "string",
   "FileFormat": "string",
   "Id": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string",
   "S3Path": { 
      "Bucket": "string",
      "Key": "string"
   },
   "Status": "string",
   "UpdatedAt": number
}
```

## Response Elements<a name="API_DescribeFaq_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ CreatedAt ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-CreatedAt"></a>
The date and time that the FAQ was created\.  
Type: Timestamp

 ** [ Description ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Description"></a>
=======
 ** [CreatedAt](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-CreatedAt"></a>
The date and time that the FAQ was created\.  
Type: Timestamp

 ** [Description](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Description"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The description of the FAQ that you provided when it was created\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

<<<<<<< HEAD
 ** [ ErrorMessage ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-ErrorMessage"></a>
=======
 ** [ErrorMessage](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-ErrorMessage"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
If the `Status` field is `FAILED`, the `ErrorMessage` field contains the reason why the FAQ failed\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

<<<<<<< HEAD
 ** [ FileFormat ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-FileFormat"></a>
=======
 ** [FileFormat](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-FileFormat"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The file format used by the input files for the FAQ\.  
Type: String  
Valid Values:` CSV | CSV_WITH_HEADER | JSON` 

<<<<<<< HEAD
 ** [ Id ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Id"></a>
=======
 ** [Id](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

<<<<<<< HEAD
 ** [ IndexId ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-IndexId"></a>
=======
 ** [IndexId](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The identifier of the index that contains the FAQ\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

<<<<<<< HEAD
 ** [ Name ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Name"></a>
=======
 ** [Name](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name that you gave the FAQ when it was created\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

<<<<<<< HEAD
 ** [ RoleArn ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-RoleArn"></a>
=======
 ** [RoleArn](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-RoleArn"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Amazon Resource Name \(ARN\) of the role that provides access to the S3 bucket containing the input files for the FAQ\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

<<<<<<< HEAD
 ** [ S3Path ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-S3Path"></a>
Information required to find a specific file in an Amazon S3 bucket\.  
Type: [ S3Path ](API_S3Path.md) object

 ** [ Status ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Status"></a>
=======
 ** [S3Path](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-S3Path"></a>
Information required to find a specific file in an Amazon S3 bucket\.  
Type: [S3Path](API_S3Path.md) object

 ** [Status](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-Status"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The status of the FAQ\. It is ready to use when the status is `ACTIVE`\.  
Type: String  
Valid Values:` CREATING | UPDATING | ACTIVE | DELETING | FAILED` 

<<<<<<< HEAD
 ** [ UpdatedAt ](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-UpdatedAt"></a>
=======
 ** [UpdatedAt](#API_DescribeFaq_ResponseSyntax) **   <a name="Kendra-DescribeFaq-response-UpdatedAt"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The date and time that the FAQ was last updated\.  
Type: Timestamp

## Errors<a name="API_DescribeFaq_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

<<<<<<< HEAD
 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
=======
 **AccessDeniedException**   
  
HTTP Status Code: 400

 **InternalServerException**   
  
HTTP Status Code: 500

 **ResourceNotFoundException**   
  
HTTP Status Code: 400

 **ThrottlingException**   
  
HTTP Status Code: 400

 **ValidationException**   
>>>>>>> parent of 2b1c178 (updating tutorial)
  
HTTP Status Code: 400

## See Also<a name="API_DescribeFaq_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeFaq) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeFaq) 