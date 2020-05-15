--------

--------

# UpdateDataSource<a name="API_UpdateDataSource"></a>

Updates an existing Amazon Kendra data source\.

## Request Syntax<a name="API_UpdateDataSource_RequestSyntax"></a>

```
{
   "[Configuration](#Kendra-UpdateDataSource-request-Configuration)": { 
      "[DatabaseConfiguration](API_DataSourceConfiguration.md#Kendra-Type-DataSourceConfiguration-DatabaseConfiguration)": { 
         "[AclConfiguration](API_DatabaseConfiguration.md#Kendra-Type-DatabaseConfiguration-AclConfiguration)": { 
            "[AllowedGroupsColumnName](API_AclConfiguration.md#Kendra-Type-AclConfiguration-AllowedGroupsColumnName)": "string"
         },
         "[ColumnConfiguration](API_DatabaseConfiguration.md#Kendra-Type-DatabaseConfiguration-ColumnConfiguration)": { 
            "[ChangeDetectingColumns](API_ColumnConfiguration.md#Kendra-Type-ColumnConfiguration-ChangeDetectingColumns)": [ "string" ],
            "[DocumentDataColumnName](API_ColumnConfiguration.md#Kendra-Type-ColumnConfiguration-DocumentDataColumnName)": "string",
            "[DocumentIdColumnName](API_ColumnConfiguration.md#Kendra-Type-ColumnConfiguration-DocumentIdColumnName)": "string",
            "[DocumentTitleColumnName](API_ColumnConfiguration.md#Kendra-Type-ColumnConfiguration-DocumentTitleColumnName)": "string",
            "[FieldMappings](API_ColumnConfiguration.md#Kendra-Type-ColumnConfiguration-FieldMappings)": [ 
               { 
                  "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                  "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                  "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
               }
            ]
         },
         "[ConnectionConfiguration](API_DatabaseConfiguration.md#Kendra-Type-DatabaseConfiguration-ConnectionConfiguration)": { 
            "[DatabaseHost](API_ConnectionConfiguration.md#Kendra-Type-ConnectionConfiguration-DatabaseHost)": "string",
            "[DatabaseName](API_ConnectionConfiguration.md#Kendra-Type-ConnectionConfiguration-DatabaseName)": "string",
            "[DatabasePort](API_ConnectionConfiguration.md#Kendra-Type-ConnectionConfiguration-DatabasePort)": number,
            "[SecretArn](API_ConnectionConfiguration.md#Kendra-Type-ConnectionConfiguration-SecretArn)": "string",
            "[TableName](API_ConnectionConfiguration.md#Kendra-Type-ConnectionConfiguration-TableName)": "string"
         },
         "[DatabaseEngineType](API_DatabaseConfiguration.md#Kendra-Type-DatabaseConfiguration-DatabaseEngineType)": "string",
         "[VpcConfiguration](API_DatabaseConfiguration.md#Kendra-Type-DatabaseConfiguration-VpcConfiguration)": { 
            "[SecurityGroupIds](API_DataSourceVpcConfiguration.md#Kendra-Type-DataSourceVpcConfiguration-SecurityGroupIds)": [ "string" ],
            "[SubnetIds](API_DataSourceVpcConfiguration.md#Kendra-Type-DataSourceVpcConfiguration-SubnetIds)": [ "string" ]
         }
      },
      "[OneDriveConfiguration](API_DataSourceConfiguration.md#Kendra-Type-DataSourceConfiguration-OneDriveConfiguration)": { 
         "[ExclusionPatterns](API_OneDriveConfiguration.md#Kendra-Type-OneDriveConfiguration-ExclusionPatterns)": [ "string" ],
         "[FieldMappings](API_OneDriveConfiguration.md#Kendra-Type-OneDriveConfiguration-FieldMappings)": [ 
            { 
               "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
               "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
               "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
            }
         ],
         "[InclusionPatterns](API_OneDriveConfiguration.md#Kendra-Type-OneDriveConfiguration-InclusionPatterns)": [ "string" ],
         "[OneDriveUsers](API_OneDriveConfiguration.md#Kendra-Type-OneDriveConfiguration-OneDriveUsers)": { 
            "[OneDriveUserList](API_OneDriveUsers.md#Kendra-Type-OneDriveUsers-OneDriveUserList)": [ "string" ],
            "[OneDriveUserS3Path](API_OneDriveUsers.md#Kendra-Type-OneDriveUsers-OneDriveUserS3Path)": { 
               "[Bucket](API_S3Path.md#Kendra-Type-S3Path-Bucket)": "string",
               "[Key](API_S3Path.md#Kendra-Type-S3Path-Key)": "string"
            }
         },
         "[SecretArn](API_OneDriveConfiguration.md#Kendra-Type-OneDriveConfiguration-SecretArn)": "string",
         "[TenantDomain](API_OneDriveConfiguration.md#Kendra-Type-OneDriveConfiguration-TenantDomain)": "string"
      },
      "[S3Configuration](API_DataSourceConfiguration.md#Kendra-Type-DataSourceConfiguration-S3Configuration)": { 
         "[AccessControlListConfiguration](API_S3DataSourceConfiguration.md#Kendra-Type-S3DataSourceConfiguration-AccessControlListConfiguration)": { 
            "[KeyPath](API_AccessControlListConfiguration.md#Kendra-Type-AccessControlListConfiguration-KeyPath)": "string"
         },
         "[BucketName](API_S3DataSourceConfiguration.md#Kendra-Type-S3DataSourceConfiguration-BucketName)": "string",
         "[DocumentsMetadataConfiguration](API_S3DataSourceConfiguration.md#Kendra-Type-S3DataSourceConfiguration-DocumentsMetadataConfiguration)": { 
            "[S3Prefix](API_DocumentsMetadataConfiguration.md#Kendra-Type-DocumentsMetadataConfiguration-S3Prefix)": "string"
         },
         "[ExclusionPatterns](API_S3DataSourceConfiguration.md#Kendra-Type-S3DataSourceConfiguration-ExclusionPatterns)": [ "string" ],
         "[InclusionPrefixes](API_S3DataSourceConfiguration.md#Kendra-Type-S3DataSourceConfiguration-InclusionPrefixes)": [ "string" ]
      },
      "[SalesforceConfiguration](API_DataSourceConfiguration.md#Kendra-Type-DataSourceConfiguration-SalesforceConfiguration)": { 
         "[ChatterFeedConfiguration](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-ChatterFeedConfiguration)": { 
            "[DocumentDataFieldName](API_SalesforceChatterFeedConfiguration.md#Kendra-Type-SalesforceChatterFeedConfiguration-DocumentDataFieldName)": "string",
            "[DocumentTitleFieldName](API_SalesforceChatterFeedConfiguration.md#Kendra-Type-SalesforceChatterFeedConfiguration-DocumentTitleFieldName)": "string",
            "[FieldMappings](API_SalesforceChatterFeedConfiguration.md#Kendra-Type-SalesforceChatterFeedConfiguration-FieldMappings)": [ 
               { 
                  "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                  "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                  "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
               }
            ],
            "[IncludeFilterTypes](API_SalesforceChatterFeedConfiguration.md#Kendra-Type-SalesforceChatterFeedConfiguration-IncludeFilterTypes)": [ "string" ]
         },
         "[CrawlAttachments](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-CrawlAttachments)": boolean,
         "[ExcludeAttachmentFilePatterns](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-ExcludeAttachmentFilePatterns)": [ "string" ],
         "[IncludeAttachmentFilePatterns](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-IncludeAttachmentFilePatterns)": [ "string" ],
         "[KnowledgeArticleConfiguration](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-KnowledgeArticleConfiguration)": { 
            "[CustomKnowledgeArticleTypeConfigurations](API_SalesforceKnowledgeArticleConfiguration.md#Kendra-Type-SalesforceKnowledgeArticleConfiguration-CustomKnowledgeArticleTypeConfigurations)": [ 
               { 
                  "[DocumentDataFieldName](API_SalesforceCustomKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceCustomKnowledgeArticleTypeConfiguration-DocumentDataFieldName)": "string",
                  "[DocumentTitleFieldName](API_SalesforceCustomKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceCustomKnowledgeArticleTypeConfiguration-DocumentTitleFieldName)": "string",
                  "[FieldMappings](API_SalesforceCustomKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceCustomKnowledgeArticleTypeConfiguration-FieldMappings)": [ 
                     { 
                        "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                        "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                        "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
                     }
                  ],
                  "[Name](API_SalesforceCustomKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceCustomKnowledgeArticleTypeConfiguration-Name)": "string"
               }
            ],
            "[IncludedStates](API_SalesforceKnowledgeArticleConfiguration.md#Kendra-Type-SalesforceKnowledgeArticleConfiguration-IncludedStates)": [ "string" ],
            "[StandardKnowledgeArticleTypeConfiguration](API_SalesforceKnowledgeArticleConfiguration.md#Kendra-Type-SalesforceKnowledgeArticleConfiguration-StandardKnowledgeArticleTypeConfiguration)": { 
               "[DocumentDataFieldName](API_SalesforceStandardKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceStandardKnowledgeArticleTypeConfiguration-DocumentDataFieldName)": "string",
               "[DocumentTitleFieldName](API_SalesforceStandardKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceStandardKnowledgeArticleTypeConfiguration-DocumentTitleFieldName)": "string",
               "[FieldMappings](API_SalesforceStandardKnowledgeArticleTypeConfiguration.md#Kendra-Type-SalesforceStandardKnowledgeArticleTypeConfiguration-FieldMappings)": [ 
                  { 
                     "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                     "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                     "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
                  }
               ]
            }
         },
         "[SecretArn](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-SecretArn)": "string",
         "[ServerUrl](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-ServerUrl)": "string",
         "[StandardObjectAttachmentConfiguration](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-StandardObjectAttachmentConfiguration)": { 
            "[DocumentTitleFieldName](API_SalesforceStandardObjectAttachmentConfiguration.md#Kendra-Type-SalesforceStandardObjectAttachmentConfiguration-DocumentTitleFieldName)": "string",
            "[FieldMappings](API_SalesforceStandardObjectAttachmentConfiguration.md#Kendra-Type-SalesforceStandardObjectAttachmentConfiguration-FieldMappings)": [ 
               { 
                  "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                  "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                  "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
               }
            ]
         },
         "[StandardObjectConfigurations](API_SalesforceConfiguration.md#Kendra-Type-SalesforceConfiguration-StandardObjectConfigurations)": [ 
            { 
               "[DocumentDataFieldName](API_SalesforceStandardObjectConfiguration.md#Kendra-Type-SalesforceStandardObjectConfiguration-DocumentDataFieldName)": "string",
               "[DocumentTitleFieldName](API_SalesforceStandardObjectConfiguration.md#Kendra-Type-SalesforceStandardObjectConfiguration-DocumentTitleFieldName)": "string",
               "[FieldMappings](API_SalesforceStandardObjectConfiguration.md#Kendra-Type-SalesforceStandardObjectConfiguration-FieldMappings)": [ 
                  { 
                     "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                     "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                     "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
                  }
               ],
               "[Name](API_SalesforceStandardObjectConfiguration.md#Kendra-Type-SalesforceStandardObjectConfiguration-Name)": "string"
            }
         ]
      },
      "[ServiceNowConfiguration](API_DataSourceConfiguration.md#Kendra-Type-DataSourceConfiguration-ServiceNowConfiguration)": { 
         "[HostUrl](API_ServiceNowConfiguration.md#Kendra-Type-ServiceNowConfiguration-HostUrl)": "string",
         "[KnowledgeArticleConfiguration](API_ServiceNowConfiguration.md#Kendra-Type-ServiceNowConfiguration-KnowledgeArticleConfiguration)": { 
            "[CrawlAttachments](API_ServiceNowKnowledgeArticleConfiguration.md#Kendra-Type-ServiceNowKnowledgeArticleConfiguration-CrawlAttachments)": boolean,
            "[DocumentDataFieldName](API_ServiceNowKnowledgeArticleConfiguration.md#Kendra-Type-ServiceNowKnowledgeArticleConfiguration-DocumentDataFieldName)": "string",
            "[DocumentTitleFieldName](API_ServiceNowKnowledgeArticleConfiguration.md#Kendra-Type-ServiceNowKnowledgeArticleConfiguration-DocumentTitleFieldName)": "string",
            "[ExcludeAttachmentFilePatterns](API_ServiceNowKnowledgeArticleConfiguration.md#Kendra-Type-ServiceNowKnowledgeArticleConfiguration-ExcludeAttachmentFilePatterns)": [ "string" ],
            "[FieldMappings](API_ServiceNowKnowledgeArticleConfiguration.md#Kendra-Type-ServiceNowKnowledgeArticleConfiguration-FieldMappings)": [ 
               { 
                  "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                  "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                  "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
               }
            ],
            "[IncludeAttachmentFilePatterns](API_ServiceNowKnowledgeArticleConfiguration.md#Kendra-Type-ServiceNowKnowledgeArticleConfiguration-IncludeAttachmentFilePatterns)": [ "string" ]
         },
         "[SecretArn](API_ServiceNowConfiguration.md#Kendra-Type-ServiceNowConfiguration-SecretArn)": "string",
         "[ServiceCatalogConfiguration](API_ServiceNowConfiguration.md#Kendra-Type-ServiceNowConfiguration-ServiceCatalogConfiguration)": { 
            "[CrawlAttachments](API_ServiceNowServiceCatalogConfiguration.md#Kendra-Type-ServiceNowServiceCatalogConfiguration-CrawlAttachments)": boolean,
            "[DocumentDataFieldName](API_ServiceNowServiceCatalogConfiguration.md#Kendra-Type-ServiceNowServiceCatalogConfiguration-DocumentDataFieldName)": "string",
            "[DocumentTitleFieldName](API_ServiceNowServiceCatalogConfiguration.md#Kendra-Type-ServiceNowServiceCatalogConfiguration-DocumentTitleFieldName)": "string",
            "[ExcludeAttachmentFilePatterns](API_ServiceNowServiceCatalogConfiguration.md#Kendra-Type-ServiceNowServiceCatalogConfiguration-ExcludeAttachmentFilePatterns)": [ "string" ],
            "[FieldMappings](API_ServiceNowServiceCatalogConfiguration.md#Kendra-Type-ServiceNowServiceCatalogConfiguration-FieldMappings)": [ 
               { 
                  "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
                  "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
                  "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
               }
            ],
            "[IncludeAttachmentFilePatterns](API_ServiceNowServiceCatalogConfiguration.md#Kendra-Type-ServiceNowServiceCatalogConfiguration-IncludeAttachmentFilePatterns)": [ "string" ]
         },
         "[ServiceNowBuildVersion](API_ServiceNowConfiguration.md#Kendra-Type-ServiceNowConfiguration-ServiceNowBuildVersion)": "string"
      },
      "[SharePointConfiguration](API_DataSourceConfiguration.md#Kendra-Type-DataSourceConfiguration-SharePointConfiguration)": { 
         "[CrawlAttachments](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-CrawlAttachments)": boolean,
         "[DocumentTitleFieldName](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-DocumentTitleFieldName)": "string",
         "[ExclusionPatterns](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-ExclusionPatterns)": [ "string" ],
         "[FieldMappings](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-FieldMappings)": [ 
            { 
               "[DataSourceFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DataSourceFieldName)": "string",
               "[DateFieldFormat](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-DateFieldFormat)": "string",
               "[IndexFieldName](API_DataSourceToIndexFieldMapping.md#Kendra-Type-DataSourceToIndexFieldMapping-IndexFieldName)": "string"
            }
         ],
         "[InclusionPatterns](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-InclusionPatterns)": [ "string" ],
         "[SecretArn](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-SecretArn)": "string",
         "[SharePointVersion](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-SharePointVersion)": "string",
         "[Urls](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-Urls)": [ "string" ],
         "[UseChangeLog](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-UseChangeLog)": boolean,
         "[VpcConfiguration](API_SharePointConfiguration.md#Kendra-Type-SharePointConfiguration-VpcConfiguration)": { 
            "[SecurityGroupIds](API_DataSourceVpcConfiguration.md#Kendra-Type-DataSourceVpcConfiguration-SecurityGroupIds)": [ "string" ],
            "[SubnetIds](API_DataSourceVpcConfiguration.md#Kendra-Type-DataSourceVpcConfiguration-SubnetIds)": [ "string" ]
         }
      }
   },
   "[Description](#Kendra-UpdateDataSource-request-Description)": "string",
   "[Id](#Kendra-UpdateDataSource-request-Id)": "string",
   "[IndexId](#Kendra-UpdateDataSource-request-IndexId)": "string",
   "[Name](#Kendra-UpdateDataSource-request-Name)": "string",
   "[RoleArn](#Kendra-UpdateDataSource-request-RoleArn)": "string",
   "[Schedule](#Kendra-UpdateDataSource-request-Schedule)": "string"
}
```

## Request Parameters<a name="API_UpdateDataSource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [Configuration](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-Configuration"></a>
Configuration information for a Amazon Kendra data source\.  
Type: [DataSourceConfiguration](API_DataSourceConfiguration.md) object  
Required: No

 ** [Description](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-Description"></a>
The new description for the data source\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [Id](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-Id"></a>
The unique identifier of the data source to update\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [IndexId](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-IndexId"></a>
The identifier of the index that contains the data source to update\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [Name](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-Name"></a>
The name of the data source to update\. The name of the data source can't be updated\. To rename a data source you must delete the data source and re\-create it\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: No

 ** [RoleArn](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-RoleArn"></a>
The Amazon Resource Name \(ARN\) of the new role to use when the data source is accessing resources on your behalf\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** [Schedule](#API_UpdateDataSource_RequestSyntax) **   <a name="Kendra-UpdateDataSource-request-Schedule"></a>
The new update schedule for the data source\.  
Type: String  
Required: No

## Response Elements<a name="API_UpdateDataSource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UpdateDataSource_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **AccessDeniedException**   
HTTP Status Code: 400

 **ConflictException**   
HTTP Status Code: 400

 **InternalServerException**   
HTTP Status Code: 500

 **ResourceNotFoundException**   
HTTP Status Code: 400

 **ThrottlingException**   
HTTP Status Code: 400

 **ValidationException**   
HTTP Status Code: 400

## See Also<a name="API_UpdateDataSource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/UpdateDataSource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/UpdateDataSource) 