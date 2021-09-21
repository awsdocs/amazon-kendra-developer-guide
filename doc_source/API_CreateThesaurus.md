--------

--------

# CreateThesaurus<a name="API_CreateThesaurus"></a>

Creates a thesaurus for an index\. The thesaurus contains a list of synonyms in Solr format\.

## Request Syntax<a name="API_CreateThesaurus_RequestSyntax"></a>

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

## Request Parameters<a name="API_CreateThesaurus_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

<<<<<<< HEAD
 ** [ ClientToken ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-ClientToken"></a>
=======
 ** [ClientToken](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-ClientToken"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A token that you provide to identify the request to create a thesaurus\. Multiple calls to the `CreateThesaurus` operation with the same client token will create only one thesaurus\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

<<<<<<< HEAD
 ** [ Description ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-Description"></a>
=======
 ** [Description](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-Description"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The description for the new thesaurus\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

<<<<<<< HEAD
 ** [ IndexId ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-IndexId"></a>
=======
 ** [IndexId](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-IndexId"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the index for the new thesaurus\.   
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ Name ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-Name"></a>
=======
 ** [Name](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-Name"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name for the new thesaurus\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

<<<<<<< HEAD
 ** [ RoleArn ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-RoleArn"></a>
=======
 ** [RoleArn](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-RoleArn"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
An AWS Identity and Access Management \(IAM\) role that gives Amazon Kendra permissions to access thesaurus file specified in `SourceS3Path`\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

<<<<<<< HEAD
 ** [ SourceS3Path ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-SourceS3Path"></a>
The thesaurus file Amazon S3 source path\.   
Type: [ S3Path ](API_S3Path.md) object  
Required: Yes

 ** [ Tags ](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-Tags"></a>
A list of key\-value pairs that identify the thesaurus\. You can use the tags to identify and organize your resources and to control access to resources\.   
Type: Array of [ Tag ](API_Tag.md) objects  
=======
 ** [SourceS3Path](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-SourceS3Path"></a>
The thesaurus file Amazon S3 source path\.   
Type: [S3Path](API_S3Path.md) object  
Required: Yes

 ** [Tags](#API_CreateThesaurus_RequestSyntax) **   <a name="Kendra-CreateThesaurus-request-Tags"></a>
A list of key\-value pairs that identify the thesaurus\. You can use the tags to identify and organize your resources and to control access to resources\.   
Type: Array of [Tag](API_Tag.md) objects  
>>>>>>> parent of 2b1c178 (updating tutorial)
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_CreateThesaurus_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateThesaurus_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

<<<<<<< HEAD
 ** [ Id ](#API_CreateThesaurus_ResponseSyntax) **   <a name="Kendra-CreateThesaurus-response-Id"></a>
=======
 ** [Id](#API_CreateThesaurus_ResponseSyntax) **   <a name="Kendra-CreateThesaurus-response-Id"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The unique identifier of the thesaurus\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

## Errors<a name="API_CreateThesaurus_Errors"></a>

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

## See Also<a name="API_CreateThesaurus_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateThesaurus) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateThesaurus) 