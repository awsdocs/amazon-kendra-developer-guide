--------

--------

# DescribeRescoreExecutionPlan<a name="API_Ranking_DescribeRescoreExecutionPlan"></a>

Gets information about a rescore execution plan\. A rescore execution plan is an Amazon Kendra Intelligent Ranking resource used for provisioning the `Rescore` API\.

## Request Syntax<a name="API_Ranking_DescribeRescoreExecutionPlan_RequestSyntax"></a>

```
{
   "Id": "string"
}
```

## Request Parameters<a name="API_Ranking_DescribeRescoreExecutionPlan_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_Ranking_DescribeRescoreExecutionPlan_RequestSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-request-Id"></a>
The identifier of the rescore execution plan that you want to get information on\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax"></a>

```
{
   "Arn": "string",
   "CapacityUnits": { 
      "RescoreCapacityUnits": number
   },
   "CreatedAt": number,
   "Description": "string",
   "ErrorMessage": "string",
   "Id": "string",
   "Name": "string",
   "Status": "string",
   "UpdatedAt": number
}
```

## Response Elements<a name="API_Ranking_DescribeRescoreExecutionPlan_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Arn](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-Arn"></a>
The Amazon Resource Name \(ARN\) of the rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

 ** [CapacityUnits](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-CapacityUnits"></a>
The capacity units set for the rescore execution plan\. A capacity of zero indicates that the rescore execution plan is using the default capacity\. For more information on the default capacity and additional capacity units, see [Adjusting capacity](https://docs.aws.amazon.com/kendra/latest/dg/adjusting-capacity.html)\.  
Type: [CapacityUnitsConfiguration](API_Ranking_CapacityUnitsConfiguration.md) object

 ** [CreatedAt](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-CreatedAt"></a>
The Unix timestamp of when the rescore execution plan was created\.  
Type: Timestamp

 ** [Description](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-Description"></a>
The description for the rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [ErrorMessage](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-ErrorMessage"></a>
When the `Status` field value is `FAILED`, the `ErrorMessage` field contains a message that explains why\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

 ** [Id](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-Id"></a>
The identifier of the rescore execution plan\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

 ** [Name](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-Name"></a>
The name for the rescore execution plan\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [Status](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-Status"></a>
The current status of the rescore execution plan\. When the value is `ACTIVE`, the rescore execution plan is ready for use\. If the `Status` field value is `FAILED`, the `ErrorMessage` field contains a message that explains why\.  
Type: String  
Valid Values:` CREATING | UPDATING | ACTIVE | DELETING | FAILED` 

 ** [UpdatedAt](#API_Ranking_DescribeRescoreExecutionPlan_ResponseSyntax) **   <a name="Kendra-Ranking_DescribeRescoreExecutionPlan-response-UpdatedAt"></a>
The Unix timestamp of when the rescore execution plan was last updated\.  
Type: Timestamp

## Errors<a name="API_Ranking_DescribeRescoreExecutionPlan_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don’t have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra Intelligent Ranking service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
The resource you want to use doesn't exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra Intelligent Ranking service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_Ranking_DescribeRescoreExecutionPlan_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/DescribeRescoreExecutionPlan) 