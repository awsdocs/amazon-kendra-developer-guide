--------

--------

# UpdateIndex<a name="API_UpdateIndex"></a>

Updates an existing Amazon Kendra index\.

## Request Syntax<a name="API_UpdateIndex_RequestSyntax"></a>

```
{
   "[CapacityUnits](#Kendra-UpdateIndex-request-CapacityUnits)": { 
      "[QueryCapacityUnits](API_CapacityUnitsConfiguration.md#Kendra-Type-CapacityUnitsConfiguration-QueryCapacityUnits)": number,
      "[StorageCapacityUnits](API_CapacityUnitsConfiguration.md#Kendra-Type-CapacityUnitsConfiguration-StorageCapacityUnits)": number
   },
   "[Description](#Kendra-UpdateIndex-request-Description)": "string",
   "[DocumentMetadataConfigurationUpdates](#Kendra-UpdateIndex-request-DocumentMetadataConfigurationUpdates)": [ 
      { 
         "[Name](API_DocumentMetadataConfiguration.md#Kendra-Type-DocumentMetadataConfiguration-Name)": "string",
         "[Relevance](API_DocumentMetadataConfiguration.md#Kendra-Type-DocumentMetadataConfiguration-Relevance)": { 
            "[Duration](API_Relevance.md#Kendra-Type-Relevance-Duration)": "string",
            "[Freshness](API_Relevance.md#Kendra-Type-Relevance-Freshness)": boolean,
            "[Importance](API_Relevance.md#Kendra-Type-Relevance-Importance)": number,
            "[RankOrder](API_Relevance.md#Kendra-Type-Relevance-RankOrder)": "string",
            "[ValueImportanceMap](API_Relevance.md#Kendra-Type-Relevance-ValueImportanceMap)": { 
               "string" : number 
            }
         },
         "[Search](API_DocumentMetadataConfiguration.md#Kendra-Type-DocumentMetadataConfiguration-Search)": { 
            "[Displayable](API_Search.md#Kendra-Type-Search-Displayable)": boolean,
            "[Facetable](API_Search.md#Kendra-Type-Search-Facetable)": boolean,
            "[Searchable](API_Search.md#Kendra-Type-Search-Searchable)": boolean
         },
         "[Type](API_DocumentMetadataConfiguration.md#Kendra-Type-DocumentMetadataConfiguration-Type)": "string"
      }
   ],
   "[Id](#Kendra-UpdateIndex-request-Id)": "string",
   "[Name](#Kendra-UpdateIndex-request-Name)": "string",
   "[RoleArn](#Kendra-UpdateIndex-request-RoleArn)": "string"
}
```

## Request Parameters<a name="API_UpdateIndex_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CapacityUnits](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-CapacityUnits"></a>
Sets the number of addtional storage and query capacity units that should be used by the index\. You can change the capacity of the index up to 5 times per day\.  
If you are using extra storage units, you can't reduce the storage capacity below that required to meet the storage needs for your index\.  
Type: [CapacityUnitsConfiguration](API_CapacityUnitsConfiguration.md) object  
Required: No

 ** [Description](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-Description"></a>
A new description for the index\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [DocumentMetadataConfigurationUpdates](#API_UpdateIndex_RequestSyntax) **   <a name="Kendra-UpdateIndex-request-DocumentMetadataConfigurationUpdates"></a>
The document metadata to update\.   
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
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

## Response Elements<a name="API_UpdateIndex_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateIndex_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **AccessDeniedException**   
HTTP Status Code: 400

 **ConflictException**   
HTTP Status Code: 400

 **InternalServerException**   
HTTP Status Code: 500

 **ResourceNotFoundException**   
HTTP Status Code: 400

 **ServiceQuotaExceededException**   
HTTP Status Code: 400

 **ThrottlingException**   
HTTP Status Code: 400

 **ValidationException**   
HTTP Status Code: 400

## See Also<a name="API_UpdateIndex_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateIndex) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateIndex) 