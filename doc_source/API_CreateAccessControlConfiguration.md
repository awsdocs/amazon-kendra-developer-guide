--------

--------

# CreateAccessControlConfiguration<a name="API_CreateAccessControlConfiguration"></a>

Creates an access configuration for your documents\. This includes user and group access information for your documents\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.

You can use this to re\-configure your existing document level access control without indexing all of your documents again\. For example, your index contains top\-secret company documents that only certain employees or users should access\. One of these users leaves the company or switches to a team that should be blocked from accessing top\-secret documents\. The user still has access to top\-secret documents because the user had access when your documents were previously indexed\. You can create a specific access control configuration for the user with deny access\. You can later update the access control configuration to allow access if the user returns to the company and re\-joins the 'top\-secret' team\. You can re\-configure access control for your documents as circumstances change\.

To apply your access control configuration to certain documents, you call the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API with the `AccessControlConfigurationId` included in the [Document](https://docs.aws.amazon.com/kendra/latest/dg/API_Document.html) object\. If you use an S3 bucket as a data source, you update the `.metadata.json` with the `AccessControlConfigurationId` and synchronize your data source\. Amazon Kendra currently only supports access control configuration for S3 data sources and documents indexed using the `BatchPutDocument` API\.

## Request Syntax<a name="API_CreateAccessControlConfiguration_RequestSyntax"></a>

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
   "ClientToken": "string",
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
   "IndexId": "string",
   "Name": "string"
}
```

## Request Parameters<a name="API_CreateAccessControlConfiguration_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [AccessControlList](#API_CreateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-request-AccessControlList"></a>
Information on principals \(users and/or groups\) and which documents they should have access to\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.  
Type: Array of [Principal](API_Principal.md) objects  
Required: No

 ** [ClientToken](#API_CreateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-request-ClientToken"></a>
A token that you provide to identify the request to create an access control configuration\. Multiple calls to the `CreateAccessControlConfiguration` API with the same client token will create only one access control configuration\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

 ** [Description](#API_CreateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-request-Description"></a>
A description for the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [HierarchicalAccessControlList](#API_CreateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-request-HierarchicalAccessControlList"></a>
The list of [principal](https://docs.aws.amazon.com/kendra/latest/dg/API_Principal.html) lists that define the hierarchy for which documents users should have access to\.  
Type: Array of [HierarchicalPrincipal](API_HierarchicalPrincipal.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 30 items\.  
Required: No

 ** [IndexId](#API_CreateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-request-IndexId"></a>
The identifier of the index to create an access control configuration for your documents\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [Name](#API_CreateAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-request-Name"></a>
A name for the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[\S\s]*`   
Required: Yes

## Response Syntax<a name="API_CreateAccessControlConfiguration_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateAccessControlConfiguration_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Id](#API_CreateAccessControlConfiguration_ResponseSyntax) **   <a name="Kendra-CreateAccessControlConfiguration-response-Id"></a>
The identifier of the access control configuration for your documents in an index\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9-]+` 

## Errors<a name="API_CreateAccessControlConfiguration_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistences with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [Support](http://aws.amazon.com/contact-us/) for help\.  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
The resource you want to use doesn’t exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ServiceQuotaExceededException **   
You have exceeded the set limits for your Amazon Kendra service\. Please see [Quotas](https://docs.aws.amazon.com/kendra/latest/dg/quotas.html) for more information, or contact [Support](http://aws.amazon.com/contact-us/) to inquire about an increase of limits\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_CreateAccessControlConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateAccessControlConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateAccessControlConfiguration) 