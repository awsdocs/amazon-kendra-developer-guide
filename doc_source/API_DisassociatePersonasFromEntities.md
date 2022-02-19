--------

--------

# DisassociatePersonasFromEntities<a name="API_DisassociatePersonasFromEntities"></a>

Removes the specific permissions of users or groups in your AWS SSO identity source with access to your Amazon Kendra experience\. You can create an Amazon Kendra experience such as a search application\. For more information on creating a search application experience, see [Building a search experience with no code](https://docs.aws.amazon.com/kendra/latest/dg/deploying-search-experience-no-code.html)\.

## Request Syntax<a name="API_DisassociatePersonasFromEntities_RequestSyntax"></a>

```
{
   "EntityIds": [ "string" ],
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DisassociatePersonasFromEntities_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ EntityIds ](#API_DisassociatePersonasFromEntities_RequestSyntax) **   <a name="Kendra-DisassociatePersonasFromEntities-request-EntityIds"></a>
The identifiers of users or groups in your AWS SSO identity source\. For example, user IDs could be user emails\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 25 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 47\.  
Pattern: `^([0-9a-f]{10}-|)[A-Fa-f0-9]{8}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{4}-[A-Fa-f0-9]{12}$`   
Required: Yes

 ** [ Id ](#API_DisassociatePersonasFromEntities_RequestSyntax) **   <a name="Kendra-DisassociatePersonasFromEntities-request-Id"></a>
The identifier of your Amazon Kendra experience\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [ IndexId ](#API_DisassociatePersonasFromEntities_RequestSyntax) **   <a name="Kendra-DisassociatePersonasFromEntities-request-IndexId"></a>
The identifier of the index for your Amazon Kendra experience\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DisassociatePersonasFromEntities_ResponseSyntax"></a>

```
{
   "FailedEntityList": [ 
      { 
         "EntityId": "string",
         "ErrorMessage": "string"
      }
   ]
}
```

## Response Elements<a name="API_DisassociatePersonasFromEntities_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ FailedEntityList ](#API_DisassociatePersonasFromEntities_ResponseSyntax) **   <a name="Kendra-DisassociatePersonasFromEntities-response-FailedEntityList"></a>
Lists the users or groups in your AWS SSO identity source that failed to properly remove access to your Amazon Kendra experience\.  
Type: Array of [ FailedEntity ](API_FailedEntity.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 25 items\.

## Errors<a name="API_DisassociatePersonasFromEntities_Errors"></a>

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

## See Also<a name="API_DisassociatePersonasFromEntities_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DisassociatePersonasFromEntities) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DisassociatePersonasFromEntities) 