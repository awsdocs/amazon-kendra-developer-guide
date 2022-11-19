--------

--------

# CreateDataSource<a name="API_CreateDataSource"></a>

Creates a data source connector that you want to use with an Amazon Kendra index\.

You specify a name, data source connector type and description for your data source\. You also specify configuration information for the data source connector\.

 `CreateDataSource` is a synchronous operation\. The operation returns 200 if the data source was successfully created\. Otherwise, an exception is raised\.

Amazon S3 and [custom](https://docs.aws.amazon.com/kendra/latest/dg/data-source-custom.html) data sources are the only supported data sources in the AWS GovCloud \(US\-West\) region\.

For an example of creating an index and data source using the Python SDK, see [Getting started with Python SDK](https://docs.aws.amazon.com/kendra/latest/dg/gs-python.html)\. For an example of creating an index and data source using the Java SDK, see [Getting started with Java SDK](https://docs.aws.amazon.com/kendra/latest/dg/gs-java.html)\.

## Request Syntax<a name="API_CreateDataSource_RequestSyntax"></a>

```
{
   "ClientToken": "string",
   "Configuration": { 
      "AlfrescoConfiguration": { 
         "BlogFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "CrawlComments": boolean,
         "CrawlSystemFolders": boolean,
         "DocumentLibraryFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "EntityFilter": [ "string" ],
         "ExclusionPatterns": [ "string" ],
         "InclusionPatterns": [ "string" ],
         "SecretArn": "string",
         "SiteId": "string",
         "SiteUrl": "string",
         "SslCertificateS3Path": { 
            "Bucket": "string",
            "Key": "string"
         },
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         },
         "WikiFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ]
      },
      "BoxConfiguration": { 
         "CommentFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "CrawlComments": boolean,
         "CrawlTasks": boolean,
         "CrawlWebLinks": boolean,
         "EnterpriseId": "string",
         "ExclusionPatterns": [ "string" ],
         "FileFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionPatterns": [ "string" ],
         "SecretArn": "string",
         "TaskFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "UseChangeLog": boolean,
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         },
         "WebLinkFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ]
      },
      "ConfluenceConfiguration": { 
         "AttachmentConfiguration": { 
            "AttachmentFieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ],
            "CrawlAttachments": boolean
         },
         "AuthenticationType": "string",
         "BlogConfiguration": { 
            "BlogFieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ]
         },
         "ExclusionPatterns": [ "string" ],
         "InclusionPatterns": [ "string" ],
         "PageConfiguration": { 
            "PageFieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ]
         },
         "ProxyConfiguration": { 
            "Credentials": "string",
            "Host": "string",
            "Port": number
         },
         "SecretArn": "string",
         "ServerUrl": "string",
         "SpaceConfiguration": { 
            "CrawlArchivedSpaces": boolean,
            "CrawlPersonalSpaces": boolean,
            "ExcludeSpaces": [ "string" ],
            "IncludeSpaces": [ "string" ],
            "SpaceFieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ]
         },
         "Version": "string",
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "DatabaseConfiguration": { 
         "AclConfiguration": { 
            "AllowedGroupsColumnName": "string"
         },
         "ColumnConfiguration": { 
            "ChangeDetectingColumns": [ "string" ],
            "DocumentDataColumnName": "string",
            "DocumentIdColumnName": "string",
            "DocumentTitleColumnName": "string",
            "FieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ]
         },
         "ConnectionConfiguration": { 
            "DatabaseHost": "string",
            "DatabaseName": "string",
            "DatabasePort": number,
            "SecretArn": "string",
            "TableName": "string"
         },
         "DatabaseEngineType": "string",
         "SqlConfiguration": { 
            "QueryIdentifiersEnclosingOption": "string"
         },
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "FsxConfiguration": { 
         "ExclusionPatterns": [ "string" ],
         "FieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "FileSystemId": "string",
         "FileSystemType": "string",
         "InclusionPatterns": [ "string" ],
         "SecretArn": "string",
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "GitHubConfiguration": { 
         "ExclusionFileNamePatterns": [ "string" ],
         "ExclusionFileTypePatterns": [ "string" ],
         "ExclusionFolderNamePatterns": [ "string" ],
         "GitHubCommitConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubDocumentCrawlProperties": { 
            "CrawlIssue": boolean,
            "CrawlIssueComment": boolean,
            "CrawlIssueCommentAttachment": boolean,
            "CrawlPullRequest": boolean,
            "CrawlPullRequestComment": boolean,
            "CrawlPullRequestCommentAttachment": boolean,
            "CrawlRepositoryDocuments": boolean
         },
         "GitHubIssueAttachmentConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubIssueCommentConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubIssueDocumentConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubPullRequestCommentConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubPullRequestDocumentAttachmentConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubPullRequestDocumentConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "GitHubRepositoryConfigurationFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionFileNamePatterns": [ "string" ],
         "InclusionFileTypePatterns": [ "string" ],
         "InclusionFolderNamePatterns": [ "string" ],
         "OnPremiseConfiguration": { 
            "HostUrl": "string",
            "OrganizationName": "string",
            "SslCertificateS3Path": { 
               "Bucket": "string",
               "Key": "string"
            }
         },
         "RepositoryFilter": [ "string" ],
         "SaaSConfiguration": { 
            "HostUrl": "string",
            "OrganizationName": "string"
         },
         "SecretArn": "string",
         "Type": "string",
         "UseChangeLog": boolean,
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "GoogleDriveConfiguration": { 
         "ExcludeMimeTypes": [ "string" ],
         "ExcludeSharedDrives": [ "string" ],
         "ExcludeUserAccounts": [ "string" ],
         "ExclusionPatterns": [ "string" ],
         "FieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionPatterns": [ "string" ],
         "SecretArn": "string"
      },
      "JiraConfiguration": { 
         "AttachmentFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "CommentFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "ExclusionPatterns": [ "string" ],
         "InclusionPatterns": [ "string" ],
         "IssueFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "IssueSubEntityFilter": [ "string" ],
         "IssueType": [ "string" ],
         "JiraAccountUrl": "string",
         "Project": [ "string" ],
         "ProjectFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "SecretArn": "string",
         "Status": [ "string" ],
         "UseChangeLog": boolean,
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         },
         "WorkLogFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ]
      },
      "OneDriveConfiguration": { 
         "DisableLocalGroups": boolean,
         "ExclusionPatterns": [ "string" ],
         "FieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionPatterns": [ "string" ],
         "OneDriveUsers": { 
            "OneDriveUserList": [ "string" ],
            "OneDriveUserS3Path": { 
               "Bucket": "string",
               "Key": "string"
            }
         },
         "SecretArn": "string",
         "TenantDomain": "string"
      },
      "QuipConfiguration": { 
         "AttachmentFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "CrawlAttachments": boolean,
         "CrawlChatRooms": boolean,
         "CrawlFileComments": boolean,
         "Domain": "string",
         "ExclusionPatterns": [ "string" ],
         "FolderIds": [ "string" ],
         "InclusionPatterns": [ "string" ],
         "MessageFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "SecretArn": "string",
         "ThreadFieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "S3Configuration": { 
         "AccessControlListConfiguration": { 
            "KeyPath": "string"
         },
         "BucketName": "string",
         "DocumentsMetadataConfiguration": { 
            "S3Prefix": "string"
         },
         "ExclusionPatterns": [ "string" ],
         "InclusionPatterns": [ "string" ],
         "InclusionPrefixes": [ "string" ]
      },
      "SalesforceConfiguration": { 
         "ChatterFeedConfiguration": { 
            "DocumentDataFieldName": "string",
            "DocumentTitleFieldName": "string",
            "FieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ],
            "IncludeFilterTypes": [ "string" ]
         },
         "CrawlAttachments": boolean,
         "ExcludeAttachmentFilePatterns": [ "string" ],
         "IncludeAttachmentFilePatterns": [ "string" ],
         "KnowledgeArticleConfiguration": { 
            "CustomKnowledgeArticleTypeConfigurations": [ 
               { 
                  "DocumentDataFieldName": "string",
                  "DocumentTitleFieldName": "string",
                  "FieldMappings": [ 
                     { 
                        "DataSourceFieldName": "string",
                        "DateFieldFormat": "string",
                        "IndexFieldName": "string"
                     }
                  ],
                  "Name": "string"
               }
            ],
            "IncludedStates": [ "string" ],
            "StandardKnowledgeArticleTypeConfiguration": { 
               "DocumentDataFieldName": "string",
               "DocumentTitleFieldName": "string",
               "FieldMappings": [ 
                  { 
                     "DataSourceFieldName": "string",
                     "DateFieldFormat": "string",
                     "IndexFieldName": "string"
                  }
               ]
            }
         },
         "SecretArn": "string",
         "ServerUrl": "string",
         "StandardObjectAttachmentConfiguration": { 
            "DocumentTitleFieldName": "string",
            "FieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ]
         },
         "StandardObjectConfigurations": [ 
            { 
               "DocumentDataFieldName": "string",
               "DocumentTitleFieldName": "string",
               "FieldMappings": [ 
                  { 
                     "DataSourceFieldName": "string",
                     "DateFieldFormat": "string",
                     "IndexFieldName": "string"
                  }
               ],
               "Name": "string"
            }
         ]
      },
      "ServiceNowConfiguration": { 
         "AuthenticationType": "string",
         "HostUrl": "string",
         "KnowledgeArticleConfiguration": { 
            "CrawlAttachments": boolean,
            "DocumentDataFieldName": "string",
            "DocumentTitleFieldName": "string",
            "ExcludeAttachmentFilePatterns": [ "string" ],
            "FieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ],
            "FilterQuery": "string",
            "IncludeAttachmentFilePatterns": [ "string" ]
         },
         "SecretArn": "string",
         "ServiceCatalogConfiguration": { 
            "CrawlAttachments": boolean,
            "DocumentDataFieldName": "string",
            "DocumentTitleFieldName": "string",
            "ExcludeAttachmentFilePatterns": [ "string" ],
            "FieldMappings": [ 
               { 
                  "DataSourceFieldName": "string",
                  "DateFieldFormat": "string",
                  "IndexFieldName": "string"
               }
            ],
            "IncludeAttachmentFilePatterns": [ "string" ]
         },
         "ServiceNowBuildVersion": "string"
      },
      "SharePointConfiguration": { 
         "AuthenticationType": "string",
         "CrawlAttachments": boolean,
         "DisableLocalGroups": boolean,
         "DocumentTitleFieldName": "string",
         "ExclusionPatterns": [ "string" ],
         "FieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionPatterns": [ "string" ],
         "ProxyConfiguration": { 
            "Credentials": "string",
            "Host": "string",
            "Port": number
         },
         "SecretArn": "string",
         "SharePointVersion": "string",
         "SslCertificateS3Path": { 
            "Bucket": "string",
            "Key": "string"
         },
         "Urls": [ "string" ],
         "UseChangeLog": boolean,
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "SlackConfiguration": { 
         "CrawlBotMessage": boolean,
         "ExcludeArchived": boolean,
         "ExclusionPatterns": [ "string" ],
         "FieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionPatterns": [ "string" ],
         "LookBackPeriod": number,
         "PrivateChannelFilter": [ "string" ],
         "PublicChannelFilter": [ "string" ],
         "SecretArn": "string",
         "SinceCrawlDate": "string",
         "SlackEntityList": [ "string" ],
         "TeamId": "string",
         "UseChangeLog": boolean,
         "VpcConfiguration": { 
            "SecurityGroupIds": [ "string" ],
            "SubnetIds": [ "string" ]
         }
      },
      "TemplateConfiguration": { 
         "Template": JSON value
      },
      "WebCrawlerConfiguration": { 
         "AuthenticationConfiguration": { 
            "BasicAuthentication": [ 
               { 
                  "Credentials": "string",
                  "Host": "string",
                  "Port": number
               }
            ]
         },
         "CrawlDepth": number,
         "MaxContentSizePerPageInMegaBytes": number,
         "MaxLinksPerPage": number,
         "MaxUrlsPerMinuteCrawlRate": number,
         "ProxyConfiguration": { 
            "Credentials": "string",
            "Host": "string",
            "Port": number
         },
         "UrlExclusionPatterns": [ "string" ],
         "UrlInclusionPatterns": [ "string" ],
         "Urls": { 
            "SeedUrlConfiguration": { 
               "SeedUrls": [ "string" ],
               "WebCrawlerMode": "string"
            },
            "SiteMapsConfiguration": { 
               "SiteMaps": [ "string" ]
            }
         }
      },
      "WorkDocsConfiguration": { 
         "CrawlComments": boolean,
         "ExclusionPatterns": [ "string" ],
         "FieldMappings": [ 
            { 
               "DataSourceFieldName": "string",
               "DateFieldFormat": "string",
               "IndexFieldName": "string"
            }
         ],
         "InclusionPatterns": [ "string" ],
         "OrganizationId": "string",
         "UseChangeLog": boolean
      }
   },
   "CustomDocumentEnrichmentConfiguration": { 
      "InlineConfigurations": [ 
         { 
            "Condition": { 
               "ConditionDocumentAttributeKey": "string",
               "ConditionOnValue": { 
                  "DateValue": number,
                  "LongValue": number,
                  "StringListValue": [ "string" ],
                  "StringValue": "string"
               },
               "Operator": "string"
            },
            "DocumentContentDeletion": boolean,
            "Target": { 
               "TargetDocumentAttributeKey": "string",
               "TargetDocumentAttributeValue": { 
                  "DateValue": number,
                  "LongValue": number,
                  "StringListValue": [ "string" ],
                  "StringValue": "string"
               },
               "TargetDocumentAttributeValueDeletion": boolean
            }
         }
      ],
      "PostExtractionHookConfiguration": { 
         "InvocationCondition": { 
            "ConditionDocumentAttributeKey": "string",
            "ConditionOnValue": { 
               "DateValue": number,
               "LongValue": number,
               "StringListValue": [ "string" ],
               "StringValue": "string"
            },
            "Operator": "string"
         },
         "LambdaArn": "string",
         "S3Bucket": "string"
      },
      "PreExtractionHookConfiguration": { 
         "InvocationCondition": { 
            "ConditionDocumentAttributeKey": "string",
            "ConditionOnValue": { 
               "DateValue": number,
               "LongValue": number,
               "StringListValue": [ "string" ],
               "StringValue": "string"
            },
            "Operator": "string"
         },
         "LambdaArn": "string",
         "S3Bucket": "string"
      },
      "RoleArn": "string"
   },
   "Description": "string",
   "IndexId": "string",
   "LanguageCode": "string",
   "Name": "string",
   "RoleArn": "string",
   "Schedule": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "Type": "string",
   "VpcConfiguration": { 
      "SecurityGroupIds": [ "string" ],
      "SubnetIds": [ "string" ]
   }
}
```

## Request Parameters<a name="API_CreateDataSource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ClientToken](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-ClientToken"></a>
A token that you provide to identify the request to create a data source connector\. Multiple calls to the `CreateDataSource` API with the same client token will create only one data source connector\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Required: No

 ** [Configuration](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-Configuration"></a>
Configuration information to connect to your data source repository\.  
You can't specify the `Configuration` parameter when the `Type` parameter is set to `CUSTOM`\. If you do, you receive a `ValidationException` exception\.  
The `Configuration` parameter is required for all other data sources\.  
Type: [DataSourceConfiguration](API_DataSourceConfiguration.md) object  
Required: No

 ** [CustomDocumentEnrichmentConfiguration](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-CustomDocumentEnrichmentConfiguration"></a>
Configuration information for altering document metadata and content during the document ingestion process\.  
For more information on how to create, modify and delete document metadata, or make other content alterations when you ingest documents into Amazon Kendra, see [Customizing document metadata during the ingestion process](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\.  
Type: [CustomDocumentEnrichmentConfiguration](API_CustomDocumentEnrichmentConfiguration.md) object  
Required: No

 ** [Description](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-Description"></a>
A description for the data source connector\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1000\.  
Pattern: `^\P{C}*$`   
Required: No

 ** [IndexId](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-IndexId"></a>
The identifier of the index you want to use with the data source connector\.  
Type: String  
Length Constraints: Fixed length of 36\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9-]*`   
Required: Yes

 ** [LanguageCode](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-LanguageCode"></a>
The code for a language\. This allows you to support a language for all documents when creating the data source connector\. English is supported by default\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 10\.  
Pattern: `[a-zA-Z-]*`   
Required: No

 ** [Name](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-Name"></a>
A name for the data source connector\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 ** [RoleArn](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-RoleArn"></a>
The Amazon Resource Name \(ARN\) of a role with permission to access the data source and required resources\. For more information, see [IAM roles for Amazon Kendra](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.  
You can't specify the `RoleArn` parameter when the `Type` parameter is set to `CUSTOM`\. If you do, you receive a `ValidationException` exception\.  
The `RoleArn` parameter is required for all other data sources\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: No

 ** [Schedule](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-Schedule"></a>
Sets the frequency for Amazon Kendra to check the documents in your data source repository and update the index\. If you don't set a schedule Amazon Kendra will not periodically update the index\. You can call the `StartDataSourceSyncJob` API to update the index\.  
You can't specify the `Schedule` parameter when the `Type` parameter is set to `CUSTOM`\. If you do, you receive a `ValidationException` exception\.  
Type: String  
Required: No

 ** [Tags](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-Tags"></a>
A list of key\-value pairs that identify the data source connector\. You can use the tags to identify and organize your resources and to control access to resources\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

 ** [Type](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-Type"></a>
The type of data source repository\. For example, `SHAREPOINT`\.  
Type: String  
Valid Values:` S3 | SHAREPOINT | DATABASE | SALESFORCE | ONEDRIVE | SERVICENOW | CUSTOM | CONFLUENCE | GOOGLEDRIVE | WEBCRAWLER | WORKDOCS | FSX | SLACK | BOX | QUIP | JIRA | GITHUB | ALFRESCO | TEMPLATE`   
Required: Yes

 ** [VpcConfiguration](#API_CreateDataSource_RequestSyntax) **   <a name="Kendra-CreateDataSource-request-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud to connect to your data source\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

## Response Syntax<a name="API_CreateDataSource_ResponseSyntax"></a>

```
{
   "Id": "string"
}
```

## Response Elements<a name="API_CreateDataSource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Id](#API_CreateDataSource_ResponseSyntax) **   <a name="Kendra-CreateDataSource-response-Id"></a>
The identifier of the data source connector\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z0-9][a-zA-Z0-9_-]*` 

## Errors<a name="API_CreateDataSource_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** AccessDeniedException **   
You don't have sufficient access to perform this action\. Please ensure you have the required permission policies and user accounts and try again\.  
HTTP Status Code: 400

 ** ConflictException **   
A conflict occurred with the request\. Please fix any inconsistences with your resources and try again\.  
HTTP Status Code: 400

 ** InternalServerException **   
An issue occurred with the internal server used for your Amazon Kendra service\. Please wait a few minutes and try again, or contact [ Support](http://aws.amazon.com/aws.amazon.com/contact-us) for help\.  
HTTP Status Code: 500

 ** ResourceAlreadyExistException **   
The resource you want to use already exists\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ResourceNotFoundException **   
The resource you want to use doesn’t exist\. Please check you have provided the correct resource and try again\.  
HTTP Status Code: 400

 ** ServiceQuotaExceededException **   
You have exceeded the set limits for your Amazon Kendra service\. Please see Quotas\[hyperlink Kendra Quotas pg\] for more information, or contact [ Support](http://aws.amazon.com/aws.amazon.com/contact-us) to inquire about an increase of limits\.  
HTTP Status Code: 400

 ** ThrottlingException **   
The request was denied due to request throttling\. Please reduce the number of requests and try again\.  
HTTP Status Code: 400

 ** ValidationException **   
The input fails to satisfy the constraints set by the Amazon Kendra service\. Please provide the correct input and try again\.  
HTTP Status Code: 400

## See Also<a name="API_CreateDataSource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/kendra-2019-02-03/CreateDataSource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/CreateDataSource) 