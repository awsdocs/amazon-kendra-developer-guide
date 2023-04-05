--------

--------

# ListRescoreExecutionPlans<a name="API_Ranking_ListRescoreExecutionPlans"></a>

Lists your rescore execution plans\. A rescore execution plan is an Amazon Kendra Intelligent Ranking resource used for provisioning the `Rescore` API\.

## Request Syntax<a name="API_Ranking_ListRescoreExecutionPlans_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NextToken": "string"
}
```

## Request Parameters<a name="API_Ranking_ListRescoreExecutionPlans_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_Ranking_ListRescoreExecutionPlans_RequestSyntax) **   <a name="Kendra-Ranking_ListRescoreExecutionPlans-request-MaxResults"></a>
The maximum number of rescore execution plans to return\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 50\.  
Required: No

 ** [NextToken](#API_Ranking_ListRescoreExecutionPlans_RequestSyntax) **   <a name="Kendra-Ranking_ListRescoreExecutionPlans-request-NextToken"></a>
If the response is truncated, Amazon Kendra Intelligent Ranking returns a pagination token in the response\. You can use this pagination token to retrieve the next set of rescore execution plans\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Pattern: `^\P{C}*$`   
Required: No

## Response Syntax<a name="API_Ranking_ListRescoreExecutionPlans_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "SummaryItems": [ 
      { 
         "CreatedAt": number,
         "Id": "string",
         "Name": "string",
         "Status": "string",
         "UpdatedAt": number
      }
   ]
}
```

## Response Elements<a name="API_Ranking_ListRescoreExecutionPlans_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_Ranking_ListRescoreExecutionPlans_ResponseSyntax) **   <a name="Kendra-Ranking_ListRescoreExecutionPlans-response-NextToken"></a>
If the response is truncated, Amazon Kendra Intelligent Ranking returns a pagination token in the response\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 800\.  
Pattern: `^\P{C}*$` 

 ** [SummaryItems](#API_Ranking_ListRescoreExecutionPlans_ResponseSyntax) **   <a name="Kendra-Ranking_ListRescoreExecutionPlans-response-SummaryItems"></a>
An array of summary information for one or more rescore execution plans\.  
Type: Array of [RescoreExecutionPlanSummary](API_Ranking_RescoreExecutionPlanSummary.md) objects

## Errors<a name="API_Ranking_ListRescoreExecutionPlans_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don’t have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra Intelligent Ranking service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra Intelligent Ranking service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_Ranking_ListRescoreExecutionPlans_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-ranking-2022-10-19/ListRescoreExecutionPlans) 