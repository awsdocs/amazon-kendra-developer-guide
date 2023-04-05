--------

--------

# CreateRescoreExecutionPlan<a name="API_Ranking_CreateRescoreExecutionPlan"></a>

Creates a rescore execution plan\. A rescore execution plan is an Amazon Kendra Intelligent Ranking resource used for provisioning the `Rescore` API\. You set the number of capacity units that you require for Amazon Kendra Intelligent Ranking to rescore or re\-rank a search service's results\.

For an example of using the `CreateRescoreExecutionPlan` API, including using the Python and Java SDKs, see [Semantically ranking a search service's results](https://docs.aws.amazon.com/kendra/latest/dg/search-service-rerank.html)\.

## Request Syntax<a name="API_Ranking_CreateRescoreExecutionPlan_RequestSyntax"></a>

```
{
   "CapacityUnits": { 
      "RescoreCapacityUnits": number
   },
   "ClientToken": "string",
   "Description": "string",
   "Name": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ]
}
```

## Request Parameters<a name="API_Ranking_CreateRescoreExecutionPlan_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CapacityUnits](#API_Ranking_CreateRescoreExecutionPlan_RequestSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-request-CapacityUnits"></a>
You can set additional capacity units to meet the needs of your rescore execution plan\. You are given a single capacity unit by default\. If you want to use the default capacity, you don't set additional capacity units\. For more information on the default capacity and additional capacity units, see [Adjusting capacity](https://docs.aws.amazon.com/kendra/latest/dg/adjusting-capacity.html)\.  
Type: [CapacityUnitsConfiguration](API_Ranking_CapacityUnitsConfiguration.md) object  
Required: No

 ** [ClientToken](#API_Ranking_CreateRescoreExecutionPlan_RequestSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-request-ClientToken"></a>
A token that you provide to identify the request to create a rescore execution plan\. Multiple calls to the `CreateRescoreExecutionPlanRequest` API with the same client token will create only one rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `^$|[\x00-\x7F]+`   
Required: No

 ** [Description](#API_Ranking_CreateRescoreExecutionPlan_RequestSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-request-Description"></a>
A description for the rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [Name](#API_Ranking_CreateRescoreExecutionPlan_RequestSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-request-Name"></a>
A name for the rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [Tags](#API_Ranking_CreateRescoreExecutionPlan_RequestSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-request-Tags"></a>
A list of key\-value pairs that identify or categorize your rescore execution plan\. You can also use tags to help control access to the rescore execution plan\. Tag keys and values can consist of Unicode letters, digits, white space, and any of the following symbols: \_ \. : / = \+ \- @\.  
Type: Array of [Tag](API_Ranking_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_Ranking_CreateRescoreExecutionPlan_ResponseSyntax"></a>

```
{
   "Arn": "string",
   "Id": "string"
}
```

## Response Elements<a name="API_Ranking_CreateRescoreExecutionPlan_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Arn](#API_Ranking_CreateRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-response-Arn"></a>
The Amazon Resource Name \(ARN\) of the rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

 ** [Id](#API_Ranking_CreateRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_CreateRescoreExecutionPlan-response-Id"></a>
The identifier of the rescore execution plan\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

## Errors<a name="API_Ranking_CreateRescoreExecutionPlan_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don’t have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistencies with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra Intelligent Ranking service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ServiceQuotaExceededException **   
You have exceeded the set limits for your Amazon Kendra Intelligent Ranking service\. Please see [Quotas](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html) for more information, or contact [Support](http://aws.amazon.com/contact-us/) to inquire about an increase of limits\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra Intelligent Ranking service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_Ranking_CreateRescoreExecutionPlan_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/CreateRescoreExecutionPlan) 