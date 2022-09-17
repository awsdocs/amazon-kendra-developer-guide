--------

--------

# DeletePrincipalMapping<a name="API_DeletePrincipalMapping"></a>

Deletes a group so that all users and sub groups that belong to the group can no longer access documents only available to that group\.

For example, after deleting the group "Summer Interns", all interns who belonged to that group no longer see intern\-only documents in their search results\.

If you want to delete or replace users or sub groups of a group, you need to use the `PutPrincipalMapping` operation\. For example, if a user in the group "Engineering" leaves the engineering team and another user takes their place, you provide an updated list of users or sub groups that belong to the "Engineering" group when calling `PutPrincipalMapping`\. You can update your internal list of users or sub groups and input this list when calling `PutPrincipalMapping`\.

 `DeletePrincipalMapping` is currently not supported in the AWS GovCloud \(US\-West\) region\.

## Request Syntax<a name="API_DeletePrincipalMapping_RequestSyntax"></a>

```
{
   "DataSourceId": "string",
   "GroupId": "string",
   "IndexId": "string",
   "OrderingId": number
}
```

## Request Parameters<a name="API_DeletePrincipalMapping_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [DataSourceId](#API_DeletePrincipalMapping_RequestSyntax) **   <a name="Kendra-DeletePrincipalMapping-request-DataSourceId"></a>
The identifier of the data source you want to delete a group from\.  
A group can be tied to multiple data sources\. You can delete a group from accessing documents in a certain data source\. For example, the groups "Research", "Engineering", and "Sales and Marketing" are all tied to the company's documents stored in the data sources Confluence and Salesforce\. You want to delete "Research" and "Engineering" groups from Salesforce, so that these groups cannot access customer\-related documents stored in Salesforce\. Only "Sales and Marketing" should access documents in the Salesforce data source\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** [GroupId](#API_DeletePrincipalMapping_RequestSyntax) **   <a name="Kendra-DeletePrincipalMapping-request-GroupId"></a>
The identifier of the group you want to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `^\P{C}*$`   
Required: Yes

 ** [IndexId](#API_DeletePrincipalMapping_RequestSyntax) **   <a name="Kendra-DeletePrincipalMapping-request-IndexId"></a>
The identifier of the index you want to delete a group from\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [OrderingId](#API_DeletePrincipalMapping_RequestSyntax) **   <a name="Kendra-DeletePrincipalMapping-request-OrderingId"></a>
The timestamp identifier you specify to ensure Amazon Kendra does not override the latest `DELETE` action with previous actions\. The highest number ID, which is the ordering ID, is the latest action you want to process and apply on top of other actions with lower number IDs\. This prevents previous actions with lower number IDs from possibly overriding the latest action\.  
The ordering ID can be the UNIX time of the last update you made to a group members list\. You would then provide this list when calling `PutPrincipalMapping`\. This ensures your `DELETE` action for that updated group with the latest members list doesn't get overwritten by earlier `DELETE` actions for the same group which are yet to be processed\.  
The default ordering ID is the current UNIX time in milliseconds that the action was received by Amazon Kendra\.   
Type: Long  
Valid Range: Minimum value of 0\. Maximum value of 32535158400000\.  
Required: No

## Response Elements<a name="API_DeletePrincipalMapping_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeletePrincipalMapping_Errors"></a>

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

## See Also<a name="API_DeletePrincipalMapping_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DeletePrincipalMapping) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DeletePrincipalMapping) 