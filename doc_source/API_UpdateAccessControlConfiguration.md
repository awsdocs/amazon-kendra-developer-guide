--------

--------

# UpdateAccessControlConfiguration<a name="API_UpdateAccessControlConfiguration"></a>

Updates an access control configuration for your documents in an index\. This includes user and group access information for your documents\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.

You can update an access control configuration you created without indexing all of your documents again\. For example, your index contains top\-secret company documents that only certain employees or users should access\. You created an 'allow' access control configuration for one user who recently joined the 'top\-secret' team, switching from a team with 'deny' access to top\-secret documents\. However, the user suddenly returns to their previous team and should no longer have access to top secret documents\. You can update the access control configuration to re\-configure access control for your documents as circumstances change\.

You call the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API to apply the updated access control configuration, with the `AccessControlConfigurationId` included in the [Document](https://docs.aws.amazon.com/kendra/latest/dg/API_Document.html) object\. If you use an S3 bucket as a data source, you synchronize your data source to apply the `AccessControlConfigurationId` in the `.metadata.json` file\. Amazon Kendra currently only supports access control configuration for S3 data sources and documents indexed using the `BatchPutDocument` API\.

## Request Syntax<a name="API_UpdateAccessControlConfiguration_RequestSyntax"></a>

```
{
   "AccessControlList": [ 
      { 
         "Access": "string",
         "DataSourceId": "string",
         "Name": "string",
         "Type": "string"
      }
   ],
   "Description": "string",
   "HierarchicalAccessControlList": [ 
      { 
         "PrincipalList": [ 
            { 
               "Access": "string",
               "DataSourceId": "string",
               "Name": "string",
               "Type": "string"
            }
         ]
      }
   ],
   "Id": "string",
   "IndexId": "string",
   "Name": "string"
}
```

## Request Parameters<a name="API_UpdateAccessControlConfiguration_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AccessControlList](#API_UpdateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-UpdateAccessControlConfiguration-request-AccessControlList"></a>
Information you want to update on principals \(users and/or groups\) and which documents they should have access to\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.  
Type: Array of [Principal](API_Principal.md) objects  
Required: No

 ** [Description](#API_UpdateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-UpdateAccessControlConfiguration-request-Description"></a>
A new description for the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [HierarchicalAccessControlList](#API_UpdateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-UpdateAccessControlConfiguration-request-HierarchicalAccessControlList"></a>
The updated list of [principal](https://docs.aws.amazon.com/kendra/latest/dg/API_Principal.html) lists that define the hierarchy for which documents users should have access to\.  
Type: Array of [HierarchicalPrincipal](API_HierarchicalPrincipal.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 30 items\.  
Required: No

 ** [Id](#API_UpdateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-UpdateAccessControlConfiguration-request-Id"></a>
The identifier of the access control configuration you want to update\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9-]+`   
Required: Yes

 ** [IndexId](#API_UpdateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-UpdateAccessControlConfiguration-request-IndexId"></a>
The identifier of the index for an access control configuration\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [Name](#API_UpdateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-UpdateAccessControlConfiguration-request-Name"></a>
A new name for the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[\S\s]*`   
Required: No

## Response Elements<a name="API_UpdateAccessControlConfiguration_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateAccessControlConfiguration_Errors"></a>

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

## See Also<a name="API_UpdateAccessControlConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateAccessControlConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateAccessControlConfiguration) 