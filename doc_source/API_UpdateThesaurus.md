--------

--------

# UpdateThesaurus<a name="API_UpdateThesaurus"></a>

Updates a thesaurus file associated with an index\.

## Request Syntax<a name="API_UpdateThesaurus_RequestSyntax"></a>

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

## Request Parameters<a name="API_UpdateThesaurus_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ Description ](#API_UpdateThesaurus_RequestSyntax) **   <a name="Kendra-UpdateThesaurus-request-Description"></a>
The updated description of the thesaurus\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [ Id ](#API_UpdateThesaurus_RequestSyntax) **   <a name="Kendra-UpdateThesaurus-request-Id"></a>
The identifier of the thesaurus to update\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [ IndexId ](#API_UpdateThesaurus_RequestSyntax) **   <a name="Kendra-UpdateThesaurus-request-IndexId"></a>
The identifier of the index associated with the thesaurus to update\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [ Name ](#API_UpdateThesaurus_RequestSyntax) **   <a name="Kendra-UpdateThesaurus-request-Name"></a>
The updated name of the thesaurus\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** [ RoleArn ](#API_UpdateThesaurus_RequestSyntax) **   <a name="Kendra-UpdateThesaurus-request-RoleArn"></a>
The updated role ARN of the thesaurus\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** [ SourceS3Path ](#API_UpdateThesaurus_RequestSyntax) **   <a name="Kendra-UpdateThesaurus-request-SourceS3Path"></a>
Information required to find a specific file in an Amazon S3 bucket\.  
Type: [ S3Path ](API_S3Path.md) object  
Required: No

## Response Elements<a name="API_UpdateThesaurus_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateThesaurus_Errors"></a>

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

## See Also<a name="API_UpdateThesaurus_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateThesaurus) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateThesaurus) 