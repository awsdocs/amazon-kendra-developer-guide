--------

--------

# PutPrincipalMapping<a name="API_PutPrincipalMapping"></a>

Maps users to their groups so that you only need to provide the user ID when you issue the query\.

You can also map sub groups to groups\. For example, the group "Company Intellectual Property Teams" includes sub groups "Research" and "Engineering"\. These sub groups include their own list of users or people who work in these teams\. Only users who work in research and engineering, and therefore belong in the intellectual property group, can see top\-secret company documents in their search results\.

This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [Filtering on user context](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.

If more than five `PUT` actions for a group are currently processing, a validation exception is thrown\.

 `PutPrincipalMapping` is currently not supported in the AWS GovCloud \(US\-West\) region\.

## Request Syntax<a name="API_PutPrincipalMapping_RequestSyntax"></a>

```
{
   "DataSourceId": "string",
   "GroupId": "string",
   "GroupMembers": { 
      "MemberGroups": [ 
         { 
            "DataSourceId": "string",
            "GroupId": "string"
         }
      ],
      "MemberUsers": [ 
         { 
            "UserId": "string"
         }
      ],
      "S3PathforGroupMembers": { 
         "Bucket": "string",
         "Key": "string"
      }
   },
   "IndexId": "string",
   "OrderingId": number,
   "RoleArn": "string"
}
```

## Request Parameters<a name="API_PutPrincipalMapping_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [DataSourceId](#API_PutPrincipalMapping_RequestSyntax) **   <a name="Kendra-PutPrincipalMapping-request-DataSourceId"></a>
The identifier of the data source you want to map users to their groups\.  
This is useful if a group is tied to multiple data sources, but you only want the group to access documents of a certain data source\. For example, the groups "Research", "Engineering", and "Sales and Marketing" are all tied to the company's documents stored in the data sources Confluence and Salesforce\. However, "Sales and Marketing" team only needs access to customer\-related documents stored in Salesforce\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** [GroupId](#API_PutPrincipalMapping_RequestSyntax) **   <a name="Kendra-PutPrincipalMapping-request-GroupId"></a>
The identifier of the group you want to map its users to\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^\P{C}*$`   
Required: Yes

 ** [GroupMembers](#API_PutPrincipalMapping_RequestSyntax) **   <a name="Kendra-PutPrincipalMapping-request-GroupMembers"></a>
The list that contains your users or sub groups that belong the same group\.  
For example, the group "Company" includes the user "CEO" and the sub groups "Research", "Engineering", and "Sales and Marketing"\.  
If you have more than 1000 users and/or sub groups for a single group, you need to provide the path to the S3 file that lists your users and sub groups for a group\. Your sub groups can contain more than 1000 users, but the list of sub groups that belong to a group \(and/or users\) must be no more than 1000\.  
Type: [GroupMembers](API_GroupMembers.md) object  
Required: Yes

 ** [IndexId](#API_PutPrincipalMapping_RequestSyntax) **   <a name="Kendra-PutPrincipalMapping-request-IndexId"></a>
The identifier of the index you want to map users to their groups\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [OrderingId](#API_PutPrincipalMapping_RequestSyntax) **   <a name="Kendra-PutPrincipalMapping-request-OrderingId"></a>
The timestamp identifier you specify to ensure Amazon Kendra does not override the latest `PUT` action with previous actions\. The highest number ID, which is the ordering ID, is the latest action you want to process and apply on top of other actions with lower number IDs\. This prevents previous actions with lower number IDs from possibly overriding the latest action\.  
The ordering ID can be the UNIX time of the last update you made to a group members list\. You would then provide this list when calling `PutPrincipalMapping`\. This ensures your `PUT` action for that updated group with the latest members list doesn't get overwritten by earlier `PUT` actions for the same group which are yet to be processed\.  
The default ordering ID is the current UNIX time in milliseconds that the action was received by Amazon Kendra\.  
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 32535158400000\.  
Required: No

 ** [RoleArn](#API_PutPrincipalMapping_RequestSyntax) **   <a name="Kendra-PutPrincipalMapping-request-RoleArn"></a>
The Amazon Resource Name \(ARN\) of a role that has access to the S3 file that contains your list of users or sub groups that belong to a group\.  
For more information, see [IAM roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

## Response Elements<a name="API_PutPrincipalMapping_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_PutPrincipalMapping_Errors"></a>

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

## See Also<a name="API_PutPrincipalMapping_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/PutPrincipalMapping) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/PutPrincipalMapping) 