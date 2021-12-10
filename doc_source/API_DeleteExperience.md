--------

--------

# DeleteExperience<a name="API_DeleteExperience"></a>

Deletes your Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Request Syntax<a name="API_DeleteExperience_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DeleteExperience_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ Id ](#API_DeleteExperience_RequestSyntax) **   <a name="Kendra-DeleteExperience-request-Id"></a>
The identifier of your Amazon Kendra experience you want to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [ IndexId ](#API_DeleteExperience_RequestSyntax) **   <a name="Kendra-DeleteExperience-request-IndexId"></a>
The identifier of the index for your Amazon Kendra experience you want to delete\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Elements<a name="API_DeleteExperience_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteExperience_Errors"></a>

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

## See Also<a name="API_DeleteExperience_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DeleteExperience) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DeleteExperience) 