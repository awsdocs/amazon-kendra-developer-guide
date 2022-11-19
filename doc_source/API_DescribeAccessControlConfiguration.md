--------

--------

# DescribeAccessControlConfiguration<a name="API_DescribeAccessControlConfiguration"></a>

Gets information about an access control configuration that you created for your documents in an index\. This includes user and group access information for your documents\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.

## Request Syntax<a name="API_DescribeAccessControlConfiguration_RequestSyntax"></a>

```
{
   "Id": "string",
   "IndexId": "string"
}
```

## Request Parameters<a name="API_DescribeAccessControlConfiguration_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_DescribeAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-request-Id"></a>
The identifier of the access control configuration you want to get information on\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 36\.  
Pattern: `[a-zA-Z0-9-]+`   
Required: Yes

 ** [IndexId](#API_DescribeAccessControlConfiguration_RequestSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-request-IndexId"></a>
The identifier of the index for an access control configuration\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeAccessControlConfiguration_ResponseSyntax"></a>

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
   "ErrorMessage": "string",
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
   "Name": "string"
}
```

## Response Elements<a name="API_DescribeAccessControlConfiguration_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [AccessControlList](#API_DescribeAccessControlConfiguration_ResponseSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-response-AccessControlList"></a>
Information on principals \(users and/or groups\) and which documents they should have access to\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\.  
Type: Array of [Principal](API_Principal.md) objects

 ** [Description](#API_DescribeAccessControlConfiguration_ResponseSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-response-Description"></a>
The description for the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [ErrorMessage](#API_DescribeAccessControlConfiguration_ResponseSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-response-ErrorMessage"></a>
The error message containing details if there are issues processing the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

 ** [HierarchicalAccessControlList](#API_DescribeAccessControlConfiguration_ResponseSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-response-HierarchicalAccessControlList"></a>
The list of [principal](https://docs.aws.amazon.com/kendra/latest/dg/API_Principal.html) lists that define the hierarchy for which documents users should have access to\.  
Type: Array of [HierarchicalPrincipal](API_HierarchicalPrincipal.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 30 items\.

 ** [Name](#API_DescribeAccessControlConfiguration_ResponseSyntax) **   <a name="Kendra-DescribeAccessControlConfiguration-response-Name"></a>
The name for the access control configuration\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `[\S\s]*` 

## Errors<a name="API_DescribeAccessControlConfiguration_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [ Support](http://aws.amazon.com/aws.amazon.com/contact-us) for help\.  
HTTP Status Code: 500

 ** ResourceNotFoundException **   
The resource you want to use doesn’t exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_DescribeAccessControlConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeAccessControlConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeAccessControlConfiguration) 