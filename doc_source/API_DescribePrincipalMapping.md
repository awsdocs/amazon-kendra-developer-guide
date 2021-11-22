--------

--------

# DescribePrincipalMapping<a name="API_DescribePrincipalMapping"></a>

Describes the processing of `PUT` and `DELETE` actions for mapping users to their groups\. This includes information on the status of actions currently processing or yet to be processed, when actions were last updated, when actions were received by Amazon Kendra, the latest action that should process and apply after other actions, and useful error messages if an action could not be processed\.

 `DescribePrincipalMapping` is currently not supported in the AWS GovCloud \(US\-West\) region\.

## Request Syntax<a name="API_DescribePrincipalMapping_RequestSyntax"></a>

```
{
   "DataSourceId": "string",
   "GroupId": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribePrincipalMapping_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ DataSourceId ](#API_DescribePrincipalMapping_RequestSyntax) **   <a name="Kendra-DescribePrincipalMapping-request-DataSourceId"></a>
The identifier of the data source to check the processing of `PUT` and `DELETE` actions for mapping users to their groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** [ GroupId ](#API_DescribePrincipalMapping_RequestSyntax) **   <a name="Kendra-DescribePrincipalMapping-request-GroupId"></a>
The identifier of the group required to check the processing of `PUT` and `DELETE` actions for mapping users to their groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^\P{C}*$`   
Required: Yes

 ** [ IndexId ](#API_DescribePrincipalMapping_RequestSyntax) **   <a name="Kendra-DescribePrincipalMapping-request-IndexId"></a>
The identifier of the index required to check the processing of `PUT` and `DELETE` actions for mapping users to their groups\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribePrincipalMapping_ResponseSyntax"></a>

```
{
   "DataSourceId": "string",
   "GroupId": "string",
   "GroupOrderingIdSummaries": [ 
      { 
         "FailureReason": "string",
         "LastUpdatedAt": number,
         "OrderingId": number,
         "ReceivedAt": number,
         "Status": "string"
      }
   ],
   "IndexId": "string"
}
```

## Response Elements<a name="API_DescribePrincipalMapping_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ DataSourceId ](#API_DescribePrincipalMapping_ResponseSyntax) **   <a name="Kendra-DescribePrincipalMapping-response-DataSourceId"></a>
Shows the identifier of the data source to see information on the processing of `PUT` and `DELETE` actions for mapping users to their groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [ GroupId ](#API_DescribePrincipalMapping_ResponseSyntax) **   <a name="Kendra-DescribePrincipalMapping-response-GroupId"></a>
Shows the identifier of the group to see information on the processing of `PUT` and `DELETE` actions for mapping users to their groups\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^\P{C}*$` 

 ** [ GroupOrderingIdSummaries ](#API_DescribePrincipalMapping_ResponseSyntax) **   <a name="Kendra-DescribePrincipalMapping-response-GroupOrderingIdSummaries"></a>
Shows the following information on the processing of `PUT` and `DELETE` actions for mapping users to their groups:  
+ Status – the status can be either `PROCESSING`, `SUCCEEDED`, `DELETING`, `DELETED`, or `FAILED`\.
+ Last updated – the last date\-time an action was updated\.
+ Received – the last date\-time an action was received or submitted\.
+ Ordering ID – the latest action that should process and apply after other actions\.
+ Failure reason – the reason an action could not be processed\.
Type: Array of [ GroupOrderingIdSummary ](API_GroupOrderingIdSummary.md) objects  
Array Members: Maximum number of 10 items\.

 ** [ IndexId ](#API_DescribePrincipalMapping_ResponseSyntax) **   <a name="Kendra-DescribePrincipalMapping-response-IndexId"></a>
Shows the identifier of the index to see information on the processing of `PUT` and `DELETE` actions for mapping users to their groups\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

## Errors<a name="API_DescribePrincipalMapping_Errors"></a>

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

## See Also<a name="API_DescribePrincipalMapping_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribePrincipalMapping) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribePrincipalMapping) 