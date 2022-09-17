--------

--------

# CreateExperience<a name="API_CreateExperience"></a>

Creates an Amazon Kendra experience such as a search application\. For more information on creating a search application experience, including using the Python and Java SDKs, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Request Syntax<a name="API_CreateExperience_RequestSyntax"></a>

```
{
   "ClientToken": "string",
   "Configuration": { 
      "ContentSourceConfiguration": { 
         "DataSourceIds": [ "string" ],
         "DirectPutContent": boolean,
         "FaqIds": [ "string" ]
      },
      "UserIdentityConfiguration": { 
         "IdentityAttributeName": "string"
      }
   },
   "Description": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string"
}
```

## Request Parameters<a name="API_CreateExperience_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ClientToken](#API_CreateExperience_RequestSyntax) **   <a name="Kendra-CreateExperience-request-ClientToken"></a>
A token that you provide to identify the request to create your Amazon Kendra experience\. Multiple calls to the `CreateExperience` API with the same client token creates only one Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

 ** [Configuration](#API_CreateExperience_RequestSyntax) **   <a name="Kendra-CreateExperience-request-Configuration"></a>
Configuration information for your Amazon Kendra experience\. This includes `ContentSourceConfiguration`, which specifies the data source IDs and/or FAQ IDs, and `UserIdentityConfiguration`, which specifies the user or group information to grant access to your Amazon Kendra experience\.  
Type: [ExperienceConfiguration](API_ExperienceConfiguration.md) object  
Required: No

 ** [Description](#API_CreateExperience_RequestSyntax) **   <a name="Kendra-CreateExperience-request-Description"></a>
A description for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [IndexId](#API_CreateExperience_RequestSyntax) **   <a name="Kendra-CreateExperience-request-IndexId"></a>
The identifier of the index for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [Name](#API_CreateExperience_RequestSyntax) **   <a name="Kendra-CreateExperience-request-Name"></a>
A name for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [RoleArn](#API_CreateExperience_RequestSyntax) **   <a name="Kendra-CreateExperience-request-RoleArn"></a>
The Amazon Resource Name \(ARN\) of a role with permission to access `Query` API, `QuerySuggestions` API, `SubmitFeedback` API, and IAM Identity Center that stores your user and group information\. For more information, see [IAM roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

## Response Syntax<a name="API_CreateExperience_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateExperience_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Id](#API_CreateExperience_ResponseSyntax) **   <a name="Kendra-CreateExperience-response-Id"></a>
The identifier for your created Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

## Errors<a name="API_CreateExperience_Errors"></a>

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

## See Also<a name="API_CreateExperience_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateExperience) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateExperience) 