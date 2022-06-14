--------

--------

# UpdateIndex<a name="API_UpdateIndex"></a>

Updates an existing Amazon Kendra index\.

## Request Syntax<a name="API_UpdateIndex_RequestSyntax"></a>

```
{
   "CapacityUnits": { 
      "QueryCapacityUnits": number,
      "StorageCapacityUnits": number
   },
   "Description": "string",
   "DocumentMetadataConfigurationUpdates": [ 
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
   "Id": "string",
   "Name": "string",
   "RoleArn": "string",
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

## Request Parameters<a name="API_UpdateIndex_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CapacityUnits](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-CapacityUnits"></a>
Sets the number of additional document storage and query capacity units that should be used by the index\. You can change the capacity of the index up to 5 times per day, or make 5 API calls\.  
If you are using extra storage units, you can't reduce the storage capacity below what is required to meet the storage needs for your index\.  
Type: [CapacityUnitsConfiguration](API_CapacityUnitsConfiguration.md) object  
Required: No

 ** [Description](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-Description"></a>
A new description for the index\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [DocumentMetadataConfigurationUpdates](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-DocumentMetadataConfigurationUpdates"></a>
The document metadata you want to update\.  
Type: Array of [DocumentMetadataConfiguration](API_DocumentMetadataConfiguration.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 500 items\.  
Required: No

 ** [Id](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-Id"></a>
The identifier of the index to update\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [Name](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-Name"></a>
The name of the index to update\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** [RoleArn](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-RoleArn"></a>
A new IAM role that gives Amazon Kendra permission to access your Amazon CloudWatch logs\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** [UserContextPolicy](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-UserContextPolicy"></a>
The user context policy\.  
Type: String  
Valid Values:` ATTRIBUTE_FILTER | USER_TOKEN`   
Required: No

 ** [UserGroupResolutionConfiguration](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-UserGroupResolutionConfiguration"></a>
Enables fetching access levels of groups and users from an AWS Single Sign\-On identity source\. To configure this, see [UserGroupResolutionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html)\.  
Type: [UserGroupResolutionConfiguration](API_UserGroupResolutionConfiguration.md) object  
Required: No

 ** [UserTokenConfigurations](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-UserTokenConfigurations"></a>
The user token configuration\.  
Type: Array of [UserTokenConfiguration](API_UserTokenConfiguration.md) objects  
Array Members: Maximum number of 1 item\.  
Required: No

## Response Elements<a name="API_UpdateIndex_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateIndex_Errors"></a>

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

## See Also<a name="API_UpdateIndex_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateIndex) 