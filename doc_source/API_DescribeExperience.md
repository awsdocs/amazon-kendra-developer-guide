--------

--------

# DescribeExperience<a name="API_DescribeExperience"></a>

Gets information about your Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Request Syntax<a name="API_DescribeExperience_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribeExperience_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ Id ](#API_DescribeExperience_RequestSyntax) **   <a name="Kendra-DescribeExperience-request-Id"></a>
The identifier of your Amazon Kendra experience you want to get information on\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [ IndexId ](#API_DescribeExperience_RequestSyntax) **   <a name="Kendra-DescribeExperience-request-IndexId"></a>
The identifier of the index for your Amazon Kendra experience you want to get information on\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeExperience_ResponseSyntax"></a>

```
{
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
   "CreatedAt": number,
   "Description": "string",
   "Endpoints": [ 
      { 
         "Endpoint": "string",
         "EndpointType": "string"
      }
   ],
   "ErrorMessage": "string",
   "Id": "string",
   "IndexId": "string",
   "Name": "string",
   "RoleArn": "string",
   "Status": "string",
   "UpdatedAt": number
}
```

## Response Elements<a name="API_DescribeExperience_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ Configuration ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-Configuration"></a>
Shows the configuration information for your Amazon Kendra experience\. This includes `ContentSourceConfiguration`, which specifies the data source IDs and/or FAQ IDs, and `UserIdentityConfiguration`, which specifies the user or group information to grant access to your Amazon Kendra experience\.  
Type: [ ExperienceConfiguration ](API_ExperienceConfiguration.md) object

 ** [ CreatedAt ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-CreatedAt"></a>
Shows the date\-time your Amazon Kendra experience was created\.  
Type: Timestamp

 ** [ Description ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-Description"></a>
Shows the description for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [ Endpoints ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-Endpoints"></a>
Shows the endpoint URLs for your Amazon Kendra experiences\. The URLs are unique and fully hosted by AWS\.  
Type: Array of [ ExperienceEndpoint ](API_ExperienceEndpoint.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 2 items\.

 ** [ ErrorMessage ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-ErrorMessage"></a>
The reason your Amazon Kendra experience could not properly process\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

 ** [ Id ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-Id"></a>
Shows the identifier of your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [ IndexId ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-IndexId"></a>
Shows the identifier of the index for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

 ** [ Name ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-Name"></a>
Shows the name of your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [ RoleArn ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-RoleArn"></a>
Shows the Amazon Resource Name \(ARN\) of a role with permission to access `Query` operations, `QuerySuggestions` operations, `SubmitFeedback` operations, and AWS SSO that stores your user and group information\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

 ** [ Status ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-Status"></a>
The current processing status of your Amazon Kendra experience\. When the status is `ACTIVE`, your Amazon Kendra experience is ready to use\. When the status is `FAILED`, the `ErrorMessage` field contains the reason that this failed\.  
Type: String  
Valid Values:` CREATING | ACTIVE | DELETING | FAILED` 

 ** [ UpdatedAt ](#API_DescribeExperience_ResponseSyntax) **   <a name="Kendra-DescribeExperience-response-UpdatedAt"></a>
Shows the date\-time your Amazon Kendra experience was last updated\.  
Type: Timestamp

## Errors<a name="API_DescribeExperience_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
  
HTTP Status Code: 400

 ** InternalServerException **   
  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
  
HTTP Status Code: 400

 ** ThrottlingException **   
  
HTTP Status Code: 400

 ** ValidationException **   
  
HTTP Status Code: 400

## See Also<a name="API_DescribeExperience_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeExperience) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeExperience) 