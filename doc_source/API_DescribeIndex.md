--------

--------

# DescribeIndex<a name="API_DescribeIndex"></a>

Gets information about an existing Amazon Kendra index\.

## Request Syntax<a name="API_DescribeIndex_RequestSyntax"></a>

```
{
   "Id": "string"
}
```

## Request Parameters<a name="API_DescribeIndex_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Id](#API_DescribeIndex_RequestSyntax) **   <a name="Kendra-DescribeIndex-request-Id"></a>
The identifier of the index you want to get information on\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

## Response Syntax<a name="API_DescribeIndex_ResponseSyntax"></a>

```
{
   "CapacityUnits": { 
      "QueryCapacityUnits": number,
      "StorageCapacityUnits": number
   },
   "CreatedAt": number,
   "Description": "string",
   "DocumentMetadataConfigurations": [ 
      { 
         "Name": "string",
         "Relevance": { 
            "Duration": "string",
            "Freshness": boolean,
            "Importance": number,
            "RankOrder": "string",
            "ValueImportanceMap": { 
               "string" : number 
            }
         },
         "Search": { 
            "Displayable": boolean,
            "Facetable": boolean,
            "Searchable": boolean,
            "Sortable": boolean
         },
         "Type": "string"
      }
   ],
   "Edition": "string",
   "ErrorMessage": "string",
   "Id": "string",
   "IndexStatistics": { 
      "FaqStatistics": { 
         "IndexedQuestionAnswersCount": number
      },
      "TextDocumentStatistics": { 
         "IndexedTextBytes": number,
         "IndexedTextDocumentsCount": number
      }
   },
   "Name": "string",
   "RoleArn": "string",
   "ServerSideEncryptionConfiguration": { 
      "KmsKeyId": "string"
   },
   "Status": "string",
   "UpdatedAt": number,
   "UserContextPolicy": "string",
   "UserGroupResolutionConfiguration": { 
      "UserGroupResolutionMode": "string"
   },
   "UserTokenConfigurations": [ 
      { 
         "JsonTokenTypeConfiguration": { 
            "GroupAttributeField": "string",
            "UserNameAttributeField": "string"
         },
         "JwtTokenTypeConfiguration": { 
            "ClaimRegex": "string",
            "GroupAttributeField": "string",
            "Issuer": "string",
            "KeyLocation": "string",
            "SecretManagerArn": "string",
            "URL": "string",
            "UserNameAttributeField": "string"
         }
      }
   ]
}
```

## Response Elements<a name="API_DescribeIndex_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CapacityUnits](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-CapacityUnits"></a>
For Enterprise Edition indexes, you can choose to use additional capacity to meet the needs of your application\. This contains the capacity units used for the index\. A query or document storage capacity of zero indicates that the index is using the default capacity\. For more information on the default capacity for an index and adjusting this, see [Adjusting capacity](https://docs.aws.amazon.com/kendra/latest/dg/adjusting-capacity.html)\.  
Type: [CapacityUnitsConfiguration](API_CapacityUnitsConfiguration.md) object

 ** [CreatedAt](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-CreatedAt"></a>
The Unix datetime that the index was created\.  
Type: Timestamp

 ** [Description](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-Description"></a>
The description for the index\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$` 

 ** [DocumentMetadataConfigurations](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-DocumentMetadataConfigurations"></a>
Configuration information for document metadata or fields\. Document metadata are fields or attributes associated with your documents\. For example, the company department name associated with each document\.  
Type: Array of [DocumentMetadataConfiguration](API_DocumentMetadataConfiguration.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 500 items\.

 ** [Edition](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-Edition"></a>
The Amazon Kendra edition used for the index\. You decide the edition when you create the index\.  
Type: String  
Valid Values:` DEVELOPER_EDITION | ENTERPRISE_EDITION` 

 ** [ErrorMessage](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-ErrorMessage"></a>
When the `Status` field value is `FAILED`, the `ErrorMessage` field contains a message that explains why\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^\P{C}*$` 

 ** [Id](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-Id"></a>
The identifier of the index\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*` 

 ** [IndexStatistics](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-IndexStatistics"></a>
Provides information about the number of FAQ questions and answers and the number of text documents indexed\.  
Type: [IndexStatistics](API_IndexStatistics.md) object

 ** [Name](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-Name"></a>
The name of the index\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

 ** [RoleArn](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-RoleArn"></a>
The Amazon Resource Name \(ARN\) of the IAM role that gives Amazon Kendra permission to write to your Amazon Cloudwatch logs\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}` 

 ** [ServerSideEncryptionConfiguration](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-ServerSideEncryptionConfiguration"></a>
The identifier of the AWS KMScustomer master key \(CMK\) that is used to encrypt your data\. Amazon Kendra doesn't support asymmetric CMKs\.  
Type: [ServerSideEncryptionConfiguration](API_ServerSideEncryptionConfiguration.md) object

 ** [Status](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-Status"></a>
The current status of the index\. When the value is `ACTIVE`, the index is ready for use\. If the `Status` field value is `FAILED`, the `ErrorMessage` field contains a message that explains why\.  
Type: String  
Valid Values:` CREATING | ACTIVE | DELETING | FAILED | UPDATING | SYSTEM_UPDATING` 

 ** [UpdatedAt](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-UpdatedAt"></a>
The Unix datetime that the index was last updated\.  
Type: Timestamp

 ** [UserContextPolicy](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-UserContextPolicy"></a>
The user context policy for the Amazon Kendra index\.  
Type: String  
Valid Values:` ATTRIBUTE_FILTER | USER_TOKEN` 

 ** [UserGroupResolutionConfiguration](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-UserGroupResolutionConfiguration"></a>
Whether you have enabled the configuration for fetching access levels of groups and users from an AWS IAM Identity Center \(successor to AWS Single Sign\-On\) identity source\.  
Type: [UserGroupResolutionConfiguration](API_UserGroupResolutionConfiguration.md) object

 ** [UserTokenConfigurations](#API_DescribeIndex_ResponseSyntax) **   <a name="Kendra-DescribeIndex-response-UserTokenConfigurations"></a>
The user token configuration for the Amazon Kendra index\.  
Type: Array of [UserTokenConfiguration](API_UserTokenConfiguration.md) objects  
Array Members: Maximum number of 1 item\.

## Errors<a name="API_DescribeIndex_Errors"></a>

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

## See Also<a name="API_DescribeIndex_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/DescribeIndex) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/DescribeIndex) 