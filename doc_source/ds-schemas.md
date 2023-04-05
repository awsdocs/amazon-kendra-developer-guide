--------

--------

# Data source template schemas<a name="ds-schemas"></a>

The following are template schemas for data sources where templates are supported\.

**Topics**
+ [Amazon S3 template schema](#ds-s3-schema)
+ [Confluence template schema](#ds-confluence-schema)
+ [Dropbox template schema](#ds-dropbox-schema)
+ [Google Drive template schema](#ds-googledrive-schema)
+ [Microsoft Exchange template schema](#ds-msexchange-schema)
+ [Microsoft OneDrive v2\.0 template schema](#ds-onedrive-schema)
+ [Microsoft SharePoint template schema](#ds-schema-sharepoint)
+ [Microsoft Teams template schema](#ds-msteams-schema)
+ [Microsoft Yammer template schema](#ds-schema-yammer)
+ [Salesforce template schema](#ds-salesforce-schema)
+ [ServiceNow template schema](#ds-servicenow-schema)
+ [Zendesk template schema](#ds-schema-zendesk)

## Amazon S3 template schema<a name="ds-s3-schema"></a>

You include a JSON that contains the data source schema as part of the template configuration\. You provide the name of the S3 bucket as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `S3`, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [S3 JSON schema](#s3-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. | 
| BucketName | The name of your Amazon S3 bucket\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
| additionalProperties | Additional configuration options for your content in your data source | 
| [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) | A list of regular expression patterns to include or exclude specific files in your Amazon S3 data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
| aclConfigurationFilePath | The file path that controls access to documents in an Amazon Kendra index\. | 
| metadataFilesPrefix | The location within your bucket for metadata files\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| type | The type of data source\. Specify S3 as your data source type\. | 
| version | The version of the template that is supported\. | 

### S3 JSON schema<a name="s3-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "BucketName": {
              "type": "string"
            }
          },
          "required": [
            "BucketName"
          ]
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "document": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      },
      "required": [
        "document"
      ]
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "inclusionPatterns": {
          "type": "array"
        },
        "exclusionPatterns": {
          "type": "array"
        },
        "inclusionPrefixes": {
          "type": "array"
        },
        "exclusionPrefixes": {
          "type": "array"
        },
        "aclConfigurationFilePath": {
          "type": "string"
        },
        "metadataFilesPrefix": {
          "type": "string"
        }
      }
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FULL_CRAWL",
        "FORCED_FULL_CRAWL"
      ]
    },
    "type": {
      "type": "string",
      "pattern": "S3"
    },
    "version": {
      "type": "string",
      "anyOf": [
        {
          "pattern": "1.0.0"
        }
      ]
    }
  },
  "required": [
    "connectionConfiguration",
    "type",
    "syncMode",
    "repositoryConfigurations"
  ]
}
```

## Confluence template schema<a name="ds-confluence-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the Confluence host URL, the hosting method, and the authentication type as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `CONFLUENCEV2`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Confluence JSON schema](#confluence-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. | 
| hostUrl | The URL for your Confluence instance\. For example, https://example\.confluence\.com\. | 
| type | The hosting method for your Confluence instance, whether SAAS and ON\_PREM\. | 
| authType | The authentication method for your Confluence instance, whether Basic, OAuth2, or Personal\-token\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of objects that map the attributes or field names of your Confluence spaces, pages, blogs, comments, and attachments to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Confluence data source field names must exist in your Confluence custom metadata\. | 
| additionalProperties | Additional configuration options for your content in your data source\. | 
| [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) | A list of regular expression patterns to include and/or exclude certain files in your Confluence data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index files in your Confluence personal spaces, pages, blogs, page comments, page attachments, blog comments, and blog attachments\. | 
| type | The type of data source\. Specify CONFLUENCEV2 as your data source type\. | 
| enableIdentityCrawler | true to activate identity crawler\. Identity crawler is activated by default\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| secretARN | The Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the key\-value pairs required to connect to your Confluence instance\.If you use basic authentication, the secret must contain a JSON structure with the following keys: <pre>{<br />"username": "Confluence account user name",<br />"password": "Confluence API token"<br />}</pre>If you use OAuth 2\.0 authentication, the secret must contain a JSON structure with the following keys: <pre>{<br />"confluenceAppKey": "app key for your Confluence account",<br />"confluenceAppSecret": "app secret from your Confluence token",<br />"confluenceAccessToken": "access token created in Confluence",<br />"confluenceRefreshToken": "refresh token created in Confluence"<br />}</pre>If you use Personal Access Token authentication, the secret must contain a JSON structure with the following keys: <pre>{<br />"patToken": "Confluence token"<br />}</pre>  | 
| version | The version of this template that is currently supported\. | 

### Confluence JSON schema<a name="confluence-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "hostUrl": {
              "type": "string",
              "pattern": "https:.*"
            },
            "type": {
              "type": "string",
              "enum": [
                "SAAS",
                "ON_PREM"
              ]
            },
            "authType": {
              "type": "string",
              "enum": [
                "Basic",
                "OAuth2",
                "Personal-token"
              ]
            }
          },
          "required": [
            "hostUrl",
            "type",
            "authType"
          ]
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "space": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "page": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "blog": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "comment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "attachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      }
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "inclusionSpaceKeyFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionSpaceKeyFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "pageTitleRegEX": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "blogTitleRegEX": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "commentTitleRegEX": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "attachmentTitleRegEX": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "isCrawlPersonalSpace": {
          "type": "boolean"
        },
        "isCrawlArchivedSpace": {
          "type": "boolean"
        },
        "isCrawlArchivedPage": {
          "type": "boolean"
        },
        "isCrawlPage": {
          "type": "boolean"
        },
        "isCrawlBlog": {
          "type": "boolean"
        },
        "isCrawlPageComment": {
          "type": "boolean"
        },
        "isCrawlPageAttachment": {
          "type": "boolean"
        },
        "isCrawlBlogComment": {
          "type": "boolean"
        },
        "isCrawlBlogAttachment": {
          "type": "boolean"
        },
        "inclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionUrlPatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionUrlPatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "proxyUrl": {
          "type": "string"
        },
        "proxyPort": {
          "type": "string"
        }
      },
      "required": []
    },
    "type": {
      "type": "string",
      "pattern": "CONFLUENCEV2"
    },
    "enableIdentityCrawler": {
      "type": "boolean"
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FULL_CRAWL",
        "FORCED_FULL_CRAWL"
      ]
    },
    "secretArn": {
      "type": "string",
      "minLength": 20,
      "maxLength": 2048
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "syncMode",
    "additionalProperties",
    "secretArn",
    "type"
  ]
}
```

## Dropbox template schema<a name="ds-dropbox-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the Dropbox app key, app secret, and access token as part of your secret that stores your authentication credentials\. Also specify the type of data source as `DROPBOX`, the type of access token you want to use \(temporary or permanent\), and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Dropbox JSON schema](#dropbox-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. This data source does not specify an endpoint in repositoryEndpointMetadata\. Rather, the connection information is included in an AWS Secrets Manager secret that you provide the secretArn\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of objects that map the attributes or field names of your Dropbox files, Dropbox Paper, and shortcuts to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Dropbox data source field names must exist in your Dropbox custom metadata\. | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Dropbox\. The secret must contain a JSON structure with the following keys: <pre>{<br />    "appKey": "Dropbox app key",<br />    "appSecret": "Dropbox app secret",<br />    "accesstoken": "temporary access token or refresh access token",<br />}</pre> | 
| additionalProperties | Additional configuration options for your content in your data source\. | 
| inclusionPatterns | A list of regular expression patterns to include certain files in your Dropbox data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
| exclusionPatterns | A list of regular expression patterns to exclude certain files in your Dropbox data source\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index files in your Dropbox, Dropbox Paper documents, Dropbox Paper templates, and webpage shortcuts stored in your Dropbox\. | 
| type | The type of data source\. Specify DROPBOX as your data source type\. | 
| useChangeLog | true to use the Dropbox change log to determine which documents require adding updating, or deleting in the index\. Depending on the change log's size, it may take longer for Amazon Kendra to use the change log than to scan all of your documents in your Dropbox\. | 
| tokenType | Specify your access token type: permanent or temporary access token\. It's recommended that you create a refresh access token that never expires in Dropbox rather that relying on a one\-time access token that expires after 4 hours\. You create an app and a refresh access token in the Dropbox developer console and provide the access token in your secret\. | 
| version | The version of this template that is currently supported\. | 

### Dropbox JSON schema<a name="dropbox-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
          }
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "file": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": [
                          "STRING",
                          "STRING_LIST",
                          "LONG",
                          "DATE"
                        ]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "paper": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": [
                          "STRING",
                          "STRING_LIST",
                          "LONG",
                          "DATE"
                        ]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "papert": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": [
                          "STRING",
                          "STRING_LIST",
                          "LONG",
                          "DATE"
                        ]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "shortcut": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": [
                          "STRING",
                          "STRING_LIST",
                          "LONG",
                          "DATE"
                        ]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      }
    },
    "secretArn": {
      "type": "string"
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "inclusionPatterns": {
          "type": "array"
        },
        "exclusionPatterns": {
          "type": "array"
        },
        "crawlFile": {
          "type": "boolean"
        },
        "crawlPaper": {
          "type": "boolean"
        },
        "crawlPapert": {
          "type": "boolean"
        },
        "crawlShortcut": {
          "type": "boolean"
        }
      }
    },
    "type": {
      "type": "string",
      "pattern": "DROPBOX"
    },
    "useChangeLog": {
      "type": "string",
      "enum": [
        "true",
        "false"
      ]
    },
    "tokenType": {
      "type": "string",
      "enum": [
        "PERMANENT",
        "TEMPORARY"
      ]
    },
    "version": {
      "type": "string",
      "anyOf": [
        {
          "pattern": "1.0.0"
        }
      ]
    }
  },
  "additionalProperties": false,
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "additionalProperties",
    "useChangeLog",
    "secretArn",
    "type",
    "tokenType"
  ]
}
```

## Google Drive template schema<a name="ds-googledrive-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. Specify the type of data source as `GOOGLEDRIVE2`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Google Drive JSON schema](#googledrive-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. This data source does not specify an endpoint\. You choose your authentication type: serviceAccount and OAuth2\. The connection information is included in an AWS Secrets Manager secret that you provide the secretArn\. | 
| authType | Choose between serviceAccount and OAuth2 based on your use case\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  |  A list of objects that map the attributes or field names of your Google Drive to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Google Drive data source field names must exist in your Google Drive custom metadata\. | 
| additionalProperties | Additional configuration options for your content in your data source | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index comments in your Google Drive data source\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of regular expression patterns to exclude certain files in your Google Drive data source\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence, and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of regular expression patterns to include certain files in your Google Drive data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence, and the file isn't included in the index\. | 
| type | The type of data source\. Specify GOOOGLEDRIVEV2 as your data source type\. | 
| enableIdentityCrawler | true to use the GoogleDrive identity crawler to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Google Drive\. The secret must contain a JSON structure with the following keys: ****If using Google Service Account authentication:<pre>{<br />    "clientEmail": "service account email",<br />    "adminAccountEmail": "user account email",<br />    "privateKey": "private key"<br />}</pre> ****If using OAuth 2\.0 authentication: <pre>{<br />    "clientID": "OAuth client ID",<br />    "clientSecret": "client secret",<br />    "refreshToken": "refresh token"<br />}</pre> | 
| version | The version of this template that is currently supported\. | 

### Google Drive JSON schema<a name="googledrive-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "authType": {
              "type": "string",
              "enum": [
                "serviceAccount",
                "OAuth2"
              ]
            }
          },
          "required": [
            "authType"
          ]
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "file": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "STRING_LIST",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "comment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "STRING_LIST"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      }
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "isCrawlComment": {
          "type": "boolean"
        },
        "excludeUserAccounts": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "excludeSharedDrives": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "excludeMimeTypes": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "includeUserAccounts": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "includeSharedDrives": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "includeMimeTypes": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionFileNamePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileNamePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionFilePathFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFilePathFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      }
    },
    "type": {
      "type": "string",
      "pattern": "GOOGLEDRIVEV2"
    },
    "enableIdentityCrawler": {
      "type": "boolean"
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FORCED_FULL_CRAWL",
        "FULL_CRAWL",
        "CHANGE_LOG"
      ]
    },
    "secretArn": {
      "type": "string",
      "minLength": 20,
      "maxLength": 2048
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "syncMode",
    "additionalProperties",
    "secretArn",
    "type"
  ]
}
```

## Microsoft Exchange template schema<a name="ds-msexchange-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the tenant ID as as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `MSEXCHANGE`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Microsoft Exchange JSON schema](#msexchange-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. | 
| tenantId | The Microsoft 365 tenant ID\. You can find your tenant ID in the Properties of your Azure Active Directory Portal\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  |  A list of objects that map the attributes or field names of your Exchange data source\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Exchange data source field names must exist in your Exchange custom metadata\. | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Exchange\. This includes your client ID and your client secret\. | 
| additionalProperties | Additional configuration options for content in your data source | 
| inclusionPatterns | A list of regular expression patterns to include certain files in your Exchange data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
| exclusionPatterns | A list of regular expression patterns to exclude certain files in your Exchange data source\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index this content in your Microsoft Exchange data source\. | 
| syncMode | Specifies how Amazon Kendra will crawl your Microsoft Exchange data source\. | 
| type | The type of data source\. Specify MSEXCHANGE as your data source type\. | 
| enableIdentityCrawler | true to use the Exchange identity crawler to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. | 
| version | The version of this template that is currently supported\. | 

### Microsoft Exchange JSON schema<a name="msexchange-json"></a>

```
{
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "tenantId": {
              "type": "string",
              "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
              "minLength": 36,
              "maxLength": 36
            }
          },
          "required": ["tenantId"]
        }
      }
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "email": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": ["STRING", "STRING_LIST", "DATE"]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "attachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": ["STRING", "DATE","LONG"]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "calendar": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": ["STRING", "STRING_LIST", "DATE"]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "contacts": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": ["STRING", "STRING_LIST", "DATE"]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "notes": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": ["STRING", "DATE"]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      },
      "required": ["email"
      ]
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "inclusionPatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionPatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionUsersList": {
          "type": "array",
          "items": {
            "type": "string",
            "format": "email"
          }
        },
        "exclusionUsersList": {
          "type": "array",
          "items": {
            "type": "string",
            "format": "email"
          }
        },
        "s3bucketName": {
          "type": "string"
        },
        "inclusionUsersFileName": {
          "type": "string"
        },
        "exclusionUsersFileName": {
          "type": "string"
        },
        "inclusionDomainUsers": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionDomainUsers": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "crawlCalendar": {
          "type": "boolean"
        },
        "crawlNotes": {
          "type": "boolean"
        },
        "crawlContacts": {
          "type": "boolean"
        },
        "startCalendarDateTime": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z$"
            },
            {
              "type": "string",
              "pattern": ""
            }
          ]
        },
        "endCalendarDateTime": {
          "anyOf": [
            {
            "type": "string",
            "pattern": "^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z$"
            },
            {
              "type": "string",
              "pattern": ""
            }
          ]
        },
        "subject": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "emailFrom": {
          "type": "array",
          "items": {
            "type": "string",
            "format": "email"
          }
        },
        "emailTo": {
          "type": "array",
          "items": {
            "type": "string",
            "format": "email"
          }
        }
      },
      "required": []
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FORCED_FULL_CRAWL",
        "FULL_CRAWL",
        "CHANGE_LOG"
      ]
    },
    "type" : {
      "type" : "string",
      "pattern": "MSEXCHANGE"
    },
    "secretArn": {
      "type": "string"
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "syncMode",
    "additionalProperties",
    "secretArn",
    "type"
  ]
}
}
```

## Microsoft OneDrive v2\.0 template schema<a name="ds-onedrive-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the Microsoft OneDrive username, password, clientId, and clientSecret, as part of your secret that stores your authentication credentials\. Also specify the type of data source as `ONEDRIVEV2`, and a secret for your authentication credentials as part of the repository configuration details\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Microsoft OneDrive v2\.0 JSON schema](#onedrive-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. This includes the tenant ID in the form of the OneDrive site URL\.  | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. Specify the type of data source and the secret ARN\. | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Salesforce\. The secret must contain a JSON structure with the following keys: <pre>{<br />    "username": "user name",<br />    "password": "password",<br />    "clientId": "client ID",<br />    "clientSecret": "client secret",<br />}</pre> | 
| additionalProperties | Additional configuration options for your content in your data source | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A collection of strings that specifies which entities to filter\. | 
| type | The type of data source\. Specify ONEDRIVEV2 as your data source type\. | 
| enableIdentityCrawler | true to use the identity crawler to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| version | The version of this template that is currently supported\. | 

### Microsoft OneDrive v2\.0 JSON schema<a name="onedrive-json"></a>

```
{
	"$schema": "http://json-schema.org/draft-04/schema#",
	"type": "object",
	"properties": {
		"connectionConfiguration": {
			"type": "object",
			"properties": {
				"repositoryEndpointMetadata": {
					"type": "object",
					"properties": {
						"tenantId": {
							"type": "string",
							"pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
							"minLength": 36,
							"maxLength": 36
						}
					},
					"required": [
						"tenantId"
					]
				}
			},
			"required": [
				"repositoryEndpointMetadata"
			]
		},
		"repositoryConfigurations": {
			"type": "object",
			"properties": {
				"file": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"STRING_LIST",
												"DATE",
												"LONG"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				}
			}
		},
		"additionalProperties": {
			"type": "object",
			"properties": {
				"userNameFilter": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"userFilterPath": {
					"type": "string"
				},
				"inclusionFileTypePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionFileTypePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionFileNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionFileNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionFilePathPatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionFilePathPatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionOneNoteSectionNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionOneNoteSectionNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionOneNotePageNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionOneNotePageNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				}
			},
			"required": []
		},
		"enableIdentityCrawler": {
			"type": "boolean"
		},
		"type": {
			"type": "string",
			"pattern": "ONEDRIVEV2"
		},
		"syncMode": {
			"type": "string",
			"enum": [
				"FULL_CRAWL",
				"FORCED_FULL_CRAWL",
				"CHANGE_LOG"
			]
		},
		"secretArn": {
			"type": "string",
			"minLength": 20,
			"maxLength": 2048
		}
	},
	"version": {
		"type": "string",
		"anyOf": [
			{
				"pattern": "1.0.0"
			}
		]
	},
	"required": [
		"connectionConfiguration",
		"repositoryConfigurations",
		"syncMode",
		"additionalProperties",
		"secretArn",
		"type"
	]
}
```

## Microsoft SharePoint template schema<a name="ds-schema-sharepoint"></a>

You include a JSON that contains the data source schema as part of [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the SharePoint host URL, domain, and also a tenant ID if required as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `SHAREPOINTV2`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the **Type** when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [SharePoint JSON schema](#sharepoint-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source | 
| repositoryEndpointMetadata | The endpoint information for the data source | 
| tenantId | The tenant id of your SharePoint account\. | 
| domain | The domain of your SharePoint account\. | 
| siteUrls | The host URLs of your SharePoint account\. | 
| repositoryAdditionalProperties | Additional properties for your data source content\. | 
| s3bucketName | The name of the Amazon S3 bucket that stores your SSL certificate\. | 
| s3certificateName | The name of the SSL certificate stored in your Amazon S3 bucket\. | 
| authType | The type of authentication you are using, whether OAuth2, OAuth2Certificate Basic NTLM, or Kerberos\. | 
| version | The SharePoint version you are using, whether Server or Online\. | 
| onPremVersion | The SharePoint Server version you are using, whether 2013, 2016 2019, or SubscriptionEdition\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
| additionalProperties | Additional configuration options for your content in your data source\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) | A list of regular expression patterns to include/exclude certain files in your Sharepoint data source\. Files that match the patterns are included in the index\. File that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence, and the file isn't included in the index\. | 
| [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html) | Input TRUE to index\. | 
| type | Specify SHAREPOINTV2 as your data source type | 
| enableIdentityCrawler | true to activate identity crawler\. Identity crawler is activated by default\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| secretARN | The Amazon Resource Name \(ARN\) of a AWS Secrets Manager secret that contains the key\-value pairs required to connect to your SharePoint\. If you use basic, NTLM, or Kerberos authentication, provide the user name and password\. If you use OAuth 2\.0 authentication, provide the user name, password, client ID, and client secret\. | 
| version | The version of this template that is currently supported\. | 

## SharePoint JSON schema<a name="sharepoint-json"></a>

```
{
	"$schema": "http://json-schema.org/draft-04/schema#",
	"type": "object",
	"properties": {
		"connectionConfiguration": {
			"type": "object",
			"properties": {
				"repositoryEndpointMetadata": {
					"type": "object",
					"properties": {
						"tenantId": {
							"type": "string",
							"pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
							"minLength": 36,
							"maxLength": 36
						},
						"domain": {
							"type": "string"
						},
						"siteUrls": {
							"type": "array",
							"items": {
								"type": "string",
								"pattern": "https://.*"
							}
						},
						"repositoryAdditionalProperties": {
							"type": "object",
							"properties": {
								"s3bucketName": {
									"type": "string"
								},
								"s3certificateName": {
									"type": "string"
								},
								"authType": {
									"type": "string",
									"enum": [
										"OAuth2",
										"OAuth2Certificate",
										"Basic",
										"NTLM",
										"Kerberos"
									]
								},
								"version": {
									"type": "string",
									"enum": [
										"Server",
										"Online"
									]
								},
								"onPremVersion": {
									"type": "string",
									"enum": [
										"",
										"2013",
										"2016",
										"2019",
										"SubscriptionEdition"
									]
								}
							},
							"required": [
								"authType",
								"version"
							]
						}
					},
					"required": [
						"siteUrls",
						"domain",
						"repositoryAdditionalProperties"
					]
				}
			},
			"required": [
				"repositoryEndpointMetadata"
			]
		},
		"repositoryConfigurations": {
			"type": "object",
			"properties": {
				"event": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"STRING_LIST",
												"DATE"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				},
				"page": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"DATE",
												"LONG"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				},
				"file": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"DATE",
												"LONG"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				},
				"link": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"STRING_LIST",
												"DATE"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				},
				"attachment": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"STRING_LIST",
												"DATE"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				},
				"comment": {
					"type": "object",
					"properties": {
						"fieldMappings": {
							"type": "array",
							"items": [
								{
									"type": "object",
									"properties": {
										"indexFieldName": {
											"type": "string"
										},
										"indexFieldType": {
											"type": "string",
											"enum": [
												"STRING",
												"STRING_LIST",
												"DATE"
											]
										},
										"dataSourceFieldName": {
											"type": "string"
										},
										"dateFieldFormat": {
											"type": "string",
											"pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
										}
									},
									"required": [
										"indexFieldName",
										"indexFieldType",
										"dataSourceFieldName"
									]
								}
							]
						}
					},
					"required": [
						"fieldMappings"
					]
				}
			}
		},
		"additionalProperties": {
			"type": "object",
			"properties": {
				"eventTitleFilterRegEx": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"pageTitleFilterRegEx": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"linkTitleFilterRegEx": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionFilePath": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionFilePath": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionFileTypePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionFileTypePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionFileNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionFileNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionOneNoteSectionNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionOneNoteSectionNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"inclusionOneNotePageNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"exclusionOneNotePageNamePatterns": {
					"type": "array",
					"items": {
						"type": "string"
					}
				},
				"crawlFiles": {
					"type": "boolean"
				},
				"crawlPages": {
					"type": "boolean"
				},
				"crawlEvents": {
					"type": "boolean"
				},
				"crawlComments": {
					"type": "boolean"
				},
				"crawlLinks": {
					"type": "boolean"
				},
				"crawlAttachments": {
					"type": "boolean"
				},
				"crawlListData": {
					"type": "boolean"
				},
				"aclConfiguration": {
					"type": "string",
					"enum": [
						"ACLWithLDAPEmailFmt",
						"ACLWithManualEmailFmt",
						"ACLWithUsernameFmt"
					]
				},
				"emailDomain": {
					"type": "string"
				},
				"isCrawlLocalGroupMapping": {
					"type": "boolean"
				},
				"isCrawlAdGroupMapping": {
					"type": "boolean"
				},
				"proxyHost": {
					"type": "string"
				},
				"proxyPort": {
					"type": "string"
				}
			},
			"required": [
			]
		},
		"type": {
			"type": "string",
			"pattern": "SHAREPOINTV2"
		},
		"enableIdentityCrawler": {
			"type": "boolean"
		},
		"syncMode": {
			"type": "string",
			"enum": [
				"FULL_CRAWL",
				"FORCED_FULL_CRAWL",
				"CHANGE_LOG"
			]
		},
		"secretArn": {
			"type": "string",
			"minLength": 20,
			"maxLength": 2048
		}
	},
	"version": {
		"type": "string",
		"anyOf": [
			{
				"pattern": "1.0.0"
			}
		]
	},
	"required": [
		"connectionConfiguration",
		"repositoryConfigurations",
		"enableIdentityCrawler",
		"syncMode",
		"additionalProperties",
		"secretArn",
		"type"
	]
}
```

## Microsoft Teams template schema<a name="ds-msteams-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the tenant ID as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `MSTEAMS`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Microsoft Teams JSON schema](#msteams-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. | 
| tenantId | The Microsoft 365 tenant ID\. You can find your tenant ID in the Properties of your Azure Active Directory Portal\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
| additionalProperties | Additional configuration options for your content in your data source\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index this content in your Microsoft Teams data source\. | 
| paymentModel | Specifies what type of payment model to use with your Teams data source\. Model A payment models are restricted to licensing and payment models that require security compliance\. Model B payment models are suitable for licensing and payment models that do not require security compliance\. | 
| syncMode | Specifies how Amazon Kendra will crawl your Microsoft Teams data source\. | 
| secretArn | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Microsoft Teams\. This includes your client ID and client secret\.  | 
| type | The type of data source\. Specify MSTEAMS as your data source type\. | 
| enableIdentityCrawler | true to use the Teams identity crawler to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. | 
| version | The version of this template that is currently supported\. | 

### Microsoft Teams JSON schema<a name="msteams-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "tenantId": {
              "type": "string",
              "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
              "minLength": 36,
              "maxLength": 36
            }
          },
          "required": [
            "tenantId"
          ]
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "chatMessage": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "chatAttachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "channelPost": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "channelWiki": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "channelAttachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "meetingChat": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "meetingFile": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "meetingNote": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "calendarMeeting": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      }
    },


    "additionalProperties": {
      "type": "object",
      "properties": {
        "paymentModel": {
          "type": "string",
          "enum": [
            "A",
            "B",
            "Evaluation Mode"
          ]
        },
        "inclusionTeamNameFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionTeamNameFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionChannelNameFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionChannelNameFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionFileNamePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileNamePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionUserEmailFilter": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "isCrawlChatMessage": {
          "type": "boolean"
        },
        "isCrawlChatAttachment": {
          "type": "boolean"
        },
        "isCrawlChannelPost": {
          "type": "boolean"
        },
        "isCrawlChannelAttachment": {
          "type": "boolean"
        },
        "isCrawlChannelWiki": {
          "type": "boolean"
        },
        "isCrawlCalendarMeeting": {
          "type": "boolean"
        },
        "isCrawlMeetingChat": {
          "type": "boolean"
        },
        "isCrawlMeetingFile": {
          "type": "boolean"
        },
        "isCrawlMeetingNote": {
          "type": "boolean"
        },
        "startCalendarDateTime": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z$"
            },
            {
              "type": "string",
              "pattern": ""
            }
          ]
        },
        "endCalendarDateTime": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z$"
            },
            {
              "type": "string",
              "pattern": ""
            }
          ]
        }
      },
      "required": []
    },
    "type": {
      "type": "string",
      "pattern": "MSTEAMS"
    },
    "enableIdentityCrawler": {
      "type": "boolean"
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FORCED_FULL_CRAWL",
        "FULL_CRAWL",
        "CHANGE_LOG"
      ]
    },
    "secretArn": {
      "type": "string",
      "minLength": 20,
      "maxLength": 2048
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "syncMode",
    "additionalProperties",
    "secretArn",
    "type"
  ]

}
```

## Microsoft Yammer template schema<a name="ds-schema-yammer"></a>

You include a JSON that contains the data source schema as part of [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. Specify the type of data source as `YAMMER`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the **Type** when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. This data source does not specify an endpoint in repositoryEndpointMetadata\. Rather, the connection information is included in an AWS Secrets Manager secret that you provide the secretArn\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of objects that map attributes or field names of Microsoft Yammer objects to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Microsoft Yammer data source field names must exist in your Microsoft Yammer custom metadata\. | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Microsoft Yammer\. This includes your client ID and client secret\. | 
| additionalProperties | Additional configuration options for your content in your data source | 
| organizationFilter | If desired, you can choose to index tickets that exist within a specific Organization | 
| repositoryEndpointMetadata | The endpoint information for the data source\. This data source does not specify an endpoint in repositoryEndpointMetadata\. Rather, the connection information is included in an AWS Secrets Manager secret that you provide the secretArn\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. Specify the type of data source and the secret ARN\. | 
| additionalProperties | Additional configuration options for content in your data source | 
| inclusionPatterns | A list of regular expression patterns to include certain files in your Yammer data source\. Files that match the patterns are included in the index\. File that don't match the patterns are excluded from the index\. If a file files in your data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
| exclusionPatterns | A list of regular expression patterns to exclude certain files in your Yammer data source\. Files that match the patterns are excluded from the files in your data source\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | Input TRUE to index | 
| type | Specify YAMMER as your data source type | 

### Microsoft Yammer JSON schema<a name="yammer-json"></a>

```
{
  {
  "connectionConfiguration": {
    "repositoryEndpointMetadata": {
    }
  },
  "repositoryConfigurations": {
    "community": {
      "fieldMappings": [
        {
          "indexFieldName": "ymr_community_id",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "id"
        },
        {
          "indexFieldName": "ymr_community_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "name"
        },
        {
          "indexFieldName": "ymr_community_email",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "email"
        },
        {
          "indexFieldName": "ymr_community_full_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "full_name"
        },
        {
          "indexFieldName": "ymr_community_description",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "description"
        },
        {
          "indexFieldName": "ymr_community_privacy",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "privacy"
        },
        {
          "indexFieldName": "ymr_community_url",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "url"
        },
        {
          "indexFieldName": "_created_at",
          "indexFieldType": "DATE",
          "dateFieldFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
          "dataSourceFieldName": "created_at"
        },
        {
          "indexFieldName": "ymr_community_state",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "state"
        },
        {
          "indexFieldName": "_source_uri",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "web_url"
        }
      ]
    },
    "user": {
      "fieldMappings": [
        {
          "indexFieldName": "ymr_user_id",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "id"
        },
        {
          "indexFieldName": "ymr_user_type",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "user_type"
        },
        {
          "indexFieldName": "_created_at",
          "indexFieldType": "DATE",
          "dateFieldFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
          "dataSourceFieldName": "activated_at"
        },
        {
          "indexFieldName": "ymr_user_full_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "full_name"
        },
        {
          "indexFieldName": "ymr_user_first_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "first_name"
        },
        {
          "indexFieldName": "ymr_user_last_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "last_name"
        },
        {
          "indexFieldName": "ymr_user_network_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "network_name"
        },
        {
          "indexFieldName": "ymr_user_url",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "url"
        },
        {
          "indexFieldName": "ymr_user_network_domains",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "network_domains"
        },
        {
          "indexFieldName": "ymr_user_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "name"
        },
        {
          "indexFieldName": "ymr_user_birthdate",
          "indexFieldType": "DATE",
          "dateFieldFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
          "dataSourceFieldName": "birth_date"
        },
        {
          "indexFieldName": "ymr_user_admin",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "admin"
        },
        {
          "indexFieldName": "ymr_user_verified_admin",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "verified_admin"
        },
        {
          "indexFieldName": "ymr_user_contact",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "contact"
        },
        {
          "indexFieldName": "ymr_user_email",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "email"
        },
        {
          "indexFieldName": "ymr_user_state",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "state"
        },
        {
          "indexFieldName": "_source_uri",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "web_url"
        }
      ]
    },
    "message": {
      "fieldMappings": [
        {
          "indexFieldName": "ymr_id",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "id"
        },
        {
          "indexFieldName": "ymr_api_url",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "api_url"
        },
        {
          "indexFieldName": "_created_at",
          "indexFieldType": "DATE",
          "dateFieldFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
          "dataSourceFieldName": "created_at"
        },
        {
          "indexFieldName": "ymr_group_id",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "group_id"
        },
        {
          "indexFieldName": "ymr_group_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "group_name"
        },
        {
          "indexFieldName": "ymr_in_private_conversation",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "in_private_conversation"
        },
        {
          "indexFieldName": "ymr_in_private_group",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "in_private_group"
        },
        {
          "indexFieldName": "ymr_message_type",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "message_type"
        },
        {
          "indexFieldName": "ymr_sender_email",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "sender_email"
        },
        {
          "indexFieldName": "ymr_sender_id",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "sender_id"
        },
        {
          "indexFieldName": "ymr_sender_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "sender_name"
        },
        {
          "indexFieldName": "_source_uri",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "web_url"
        }
      ]
    },
    "attachment": {
      "fieldMappings": [
        {
          "indexFieldName": "ymr_attachment_id",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "id"
        },
        {
          "indexFieldName": "ymr_attachment_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "name"
        },
        {
          "indexFieldName": "ymr_attachment_size",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "size"
        },
        {
          "indexFieldName": "ymr_attachment_url",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "url"
        },
        {
          "indexFieldName": "ymr_attachment_type",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "file_type"
        },
        {
          "indexFieldName": "_created_at",
          "indexFieldType": "DATE",
          "dateFieldFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
          "dataSourceFieldName": "created_at"
        },
        {
          "indexFieldName": "ymr_attachment_privacy",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "privacy"
        },
        {
          "indexFieldName": "ymr_attachment_group_name",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "group_name"
        },
        {
          "indexFieldName": "ymr_attachment_sender_email",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "sender_email"
        },
        {
          "indexFieldName": "_source_uri",
          "indexFieldType": "STRING",
          "dataSourceFieldName": "web_url"
        }
      ]
    }
  },
  "additionalProperties": {
    "inclusionPatterns": [
      ".*\\.txt",
      ".*\\.doc",
      ".*\\.ppt"
    ],
    "exclusionPatterns": [
      ".*\\.pdf",
      "exclusionffff.txt"
    ],
    "sinceDate": "2020-02-09T00:00:02+00:00",
    "communityNameFilter": [
      "Ritesh's Community"
    ],
    "isCrawlMessage": true,
    "isCrawlAttachment": true,
    "isCrawlPrivateMessage": true
  },
  "type" : "YAMMER",
  "secretArn": "arn:aws:secretsmanager:us-west-2:123:secret:AmazonKendra-Yammer-bILNGJ",
  "syncMode": "FULL_CRAWL",
  "version": "1.0.0"
 }  
}
```

## Salesforce template schema<a name="ds-salesforce-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the Salesforce host URL as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `SALESFORCEV2`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Salesforce JSON schema](#salesforce-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. | 
| hostUrl | The URL of the Salesforce instance to be indexed\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  |  A list of objects that map the attributes or field names of your Salesforce entities to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Salesforce data source field names must exist in your Salesforce custom metadata\. | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Salesforce\. The secret must contain a JSON structure with the following keys: <pre>{<br />    "username": "user name",<br />    "password": "password",<br />    "clientId": "cient ID",<br />    "clientSecret": "client secret",<br />}</pre> | 
| additionalProperties | Additional configuration options for your content in your data source | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A collection of strings that specifies which entities to filter\. | 
| inclusionPatterns [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of regular expression patterns to include certain files in your Salesforce data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
| exclusionPatterns [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of regular expression patterns to exclude certain files in your Salesforce data source\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index corresponding files in your Salesforce account\. | 
| type | The type of data source\. Specify SALESFORCEV2 as your data source type\. | 
| enableIdentityCrawler | true to use the Salesforce identity crawler to activate Amazon Kendra identity crawler to sync identity information\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| version | The version of this template that is currently supported\. | 

### Salesforce JSON schema<a name="salesforce-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties":
  {
    "connectionConfiguration": {
      "type": "object",
      "properties":
      {
        "repositoryEndpointMetadata":
        {
          "type": "object",
          "properties":
          {
            "hostUrl":
            {
              "type": "string",
              "pattern": "https:.*"
            }
          },
          "required":
          [
            "hostUrl"
          ]
        }
      },
      "required":
      [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties":
      {
        "account":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "contact":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "campaign":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "case":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "product":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "lead":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "contract":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "partner":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "profile":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "idea":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "pricebook":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "task":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "solution":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "attachment":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "user":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "document":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "knowledgeArticles":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "group":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "opportunity":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE",
                        "LONG"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "chatter":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        },
        "customEntity":
        {
          "type": "object",
          "properties":
          {
            "fieldMappings":
            {
              "type": "array",
              "items":
              [
                {
                  "type": "object",
                  "properties":
                  {
                    "indexFieldName":
                    {
                      "type": "string"
                    },
                    "indexFieldType":
                    {
                      "type": "string",
                      "enum":
                      [
                        "STRING",
                        "STRING_LIST",
                        "DATE"
                      ]
                    },
                    "dataSourceFieldName":
                    {
                      "type": "string"
                    },
                    "dateFieldFormat":
                    {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required":
                  [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required":
          [
            "fieldMappings"
          ]
        }
      }
    },
    "additionalProperties": {
      "type": "object",
      "properties":
      {
        "accountFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "contactFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "caseFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "campaignFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "contractFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "groupFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "leadFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "productFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "opportunityFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "partnerFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "pricebookFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "ideaFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "profileFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "taskFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "solutionFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "userFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "chatterFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "documentFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "knowledgeArticleFilter":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "customEntities":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "isCrawlAccount": {
          "type": "boolean"
        },
        "isCrawlContact": {
          "type": "boolean"
        },
        "isCrawlCase": {
          "type": "boolean"
        },
        "isCrawlCampaign": {
          "type": "boolean"
        },
        "isCrawlProduct": {
          "type": "boolean"
        },
        "isCrawlLead": {
          "type": "boolean"
        },
        "isCrawlContract": {
          "type": "boolean"
        },
        "isCrawlPartner": {
          "type": "boolean"
        },
        "isCrawlProfile": {
          "type": "boolean"
        },
        "isCrawlIdea": {
          "type": "boolean"
        },
        "isCrawlPricebook": {
          "type": "boolean"
        },
        "isCrawlDocument": {
          "type": "boolean"
        },
        "crawlSharedDocument": {
          "type": "boolean"
        },
        "isCrawlGroup": {
          "type": "boolean"
        },
        "isCrawlOpportunity": {
          "type": "boolean"
        },
        "isCrawlChatter": {
          "type": "boolean"
        },
        "isCrawlUser": {
          "type": "boolean"
        },
        "isCrawlSolution":{
          "type": "boolean"
        },
        "isCrawlTask":{
          "type": "boolean"
        },

        "isCrawlAccountAttachments": {
          "type": "boolean"
        },
        "isCrawlContactAttachments": {
          "type": "boolean"
        },
        "isCrawlCaseAttachments": {
          "type": "boolean"
        },
        "isCrawlCampaignAttachments": {
          "type": "boolean"
        },
        "isCrawlLeadAttachments": {
          "type": "boolean"
        },
        "isCrawlContractAttachments": {
          "type": "boolean"
        },
        "isCrawlGroupAttachments": {
          "type": "boolean"
        },
        "isCrawlOpportunityAttachments": {
          "type": "boolean"
        },
        "isCrawlChatterAttachments": {
          "type": "boolean"
        },
        "isCrawlSolutionAttachments":{
          "type": "boolean"
        },
        "isCrawlTaskAttachments":{
          "type": "boolean"
        },
        "isCrawlCustomEntityAttachments":{
          "type": "boolean"
        },
        "isCrawlKnowledgeArticles": {
          "type": "object",
          "properties":
          {
            "isCrawlDraft": {
              "type": "boolean"
            },
            "isCrawlPublish": {
              "type": "boolean"
            },
            "isCrawlArchived": {
              "type": "boolean"
            }
          }
        },
        "inclusionDocumentFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionDocumentFileTypePatterns": {
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionDocumentFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionDocumentFileNamePatterns": {
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionAccountFileTypePatterns": {
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionAccountFileTypePatterns": {
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionAccountFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionAccountFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionCampaignFileTypePatterns": {
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionCampaignFileTypePatterns": {
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionCampaignFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionCampaignFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionCaseFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionCaseFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionCaseFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionCaseFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionContactFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionContactFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionContactFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionContactFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionContractFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionContractFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionContractFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionContractFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionLeadFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionLeadFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionLeadFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionLeadFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionOpportunityFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionOpportunityFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionOpportunityFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionOpportunityFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionSolutionFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionSolutionFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionSolutionFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionSolutionFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionTaskFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionTaskFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionTaskFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionTaskFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionGroupFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionGroupFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionGroupFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionGroupFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionChatterFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionChatterFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionChatterFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionChatterFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionCustomEntityFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionCustomEntityFileTypePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "inclusionCustomEntityFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        },
        "exclusionCustomEntityFileNamePatterns":{
          "type": "array",
          "items":
          {
            "type": "string"
          }
        }
      },
      "required":
      []
    },
    "enableIdentityCrawler": {
      "type": "boolean"
    },
    "type": {
      "type": "string",
      "pattern": "SALESFORCEV2"
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FULL_CRAWL",
        "FORCED_FULL_CRAWL",
        "CHANGE_LOG"
      ]
    },
    "secretArn": {
      "type": "string",
      "minLength": 20,
      "maxLength": 2048
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "syncMode",
    "additionalProperties",
    "secretArn",
    "type"
  ]
}
```

## ServiceNow template schema<a name="ds-servicenow-schema"></a>

You include a JSON that contains the data source schema as part of the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the ServiceNow host URL, authentication type, and instance version as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `SERVICENOWV2`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the `Type` when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [ServiceNow JSON schema](#servicenow-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source\. | 
| repositoryEndpointMetadata | The endpoint information for the data source\. | 
| hostUrl | The ServiceNow host URL\. For example, your\-domain\.service\-now\.com\. | 
| authType | The type of authentication you are using, whether basicAuth or OAuth2\. | 
| servicenowInstanceVersion | The ServiceNow version you are using\. You can choose between Tokyo, Sandiego, Rome, and Others\. | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of objects that map the attributes or field names of your ServiceNow knowledge articles, attachments, service catalog, and incidents to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The ServiceNow data source field names must exist in your ServiceNow custom metadata\. | 
| additional properties | Additional configuration options for your content in your data source\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | A list of regular expression patterns to include and/or exclude certain files in your ServiceNow data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | true to index ServiceNow knowledge articles, service catalogs, incidents, and attachments\. | 
| type | The type of data source\. Specify SERVICENOWV2 as your data source type\. | 
| enableIdentityCrawler | true to activate identity crawler\. Identity crawler is activated by default\. If you choose to turn identity crawler off, you must upload the principal information using the [PutPrincipalMapping ](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html)API\. | 
| syncMode | Specify whether Amazon Kendra should update your index by syncing all documents or only new, modified, and deleted documents\. You can choose between: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your ServiceNow\. The secret must contain a JSON structure with the following keys: <pre>{<br />    "username": "user name",<br />    "password": "password",<br />}</pre> If you use OAuth2 authentication, your secret must contain a JSON structure with the following keys: <pre>{<br />    "username": "user name",<br />    "password": "password",<br />    "clientId": "client id",<br />    "clientSecret": "client secret"          <br />}</pre>  | 
| version | The version of the template that is currently supported\. | 

### ServiceNow JSON schema<a name="servicenow-json"></a>

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "hostUrl": {
              "type": "string",
              "pattern": "^(?!(^(https?|ftp|file):\/\/))[a-z0-9-]+.service-now.com$",
              "minLength": 1,
              "maxLength": 2048
            },
            "authType": {
              "type": "string",
              "enum": [
                "basicAuth",
                "OAuth2"
              ]
            },
            "servicenowInstanceVersion": {
              "type": "string",
              "enum": [
                "Tokyo",
                "Sandiego",
                "Rome",
                "Others"
                ]
            }
          },
          "required": [
            "hostUrl",
            "authType",
            "servicenowInstanceVersion"
          ]
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "knowledgeArticle": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "STRING_LIST"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "attachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "LONG",
                        "DATE",
                        "STRING_LIST"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "serviceCatalog": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "STRING_LIST"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "incident": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "indexFieldName": {
                      "type": "string"
                    },
                    "indexFieldType": {
                      "type": "string",
                      "enum": [
                        "STRING",
                        "DATE",
                        "STRING_LIST"
                      ]
                    },
                    "dataSourceFieldName": {
                      "type": "string"
                    },
                    "dateFieldFormat": {
                      "type": "string",
                      "pattern": "yyyy-MM-dd'T'HH:mm:ss'Z'"
                    }
                  },
                  "required": [
                    "indexFieldName",
                    "indexFieldType",
                    "dataSourceFieldName"
                  ]
                }
              ]
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      }
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "isCrawlKnowledgeArticle": {
          "type": "boolean"
        },
        "isCrawlKnowledgeArticleAttachment": {
          "type": "boolean"
        },
        "includePublicArticlesOnly": {
          "type": "boolean"
        },
        "knowledgeArticleFilter": {
          "type": "string"
        },
        "incidentQueryFilter": {
          "type": "string"
        },
        "serviceCatalogQueryFilter": {
          "type": "string"
        },
        "isCrawlServiceCatalog": {
          "type": "boolean"
        },
        "isCrawlServiceCatalogAttachment": {
          "type": "boolean"
        },
        "isCrawlActiveServiceCatalog": {
          "type": "boolean"
        },
        "isCrawlInactiveServiceCatalog": {
          "type": "boolean"
        },
        "isCrawlIncident": {
          "type": "boolean"
        },
        "isCrawlIncidentAttachment": {
          "type": "boolean"
        },
        "isCrawlActiveIncident": {
          "type": "boolean"
        },
        "isCrawlInactiveIncident": {
          "type": "boolean"
        },
        "applyACLForKnowledgeArticle": {
          "type": "boolean"
        },
        "applyACLForServiceCatalog": {
          "type": "boolean"
        },
        "applyACLForIncident": {
          "type": "boolean"
        },
        "incidentStateType": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "Open",
              "Open - Unassigned",
              "Resolved",
              "All"
            ]
          }
        },
        "knowledgeArticleTitleRegExp": {
          "type": "string"
        },
        "serviceCatalogTitleRegExp": {
          "type": "string"
        },
        "incidentTitleRegExp": {
          "type": "string"
        },
        "inclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileTypePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "inclusionFileNamePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "exclusionFileNamePatterns": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      },
      "required": []
    },
    "type": {
      "type": "string",
      "pattern": "SERVICENOWV2"
    },
    "enableIdentityCrawler": {
      "type": "boolean"
    },
    "syncMode": {
      "type": "string",
      "enum": [
        "FORCED_FULL_CRAWL",
        "FULL_CRAWL"
      ]
    },
    "secretArn": {
      "type": "string",
      "minLength": 20,
      "maxLength": 2048
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "syncMode",
    "additionalProperties",
    "secretArn",
    "type"
  ]
}
```

## Zendesk template schema<a name="ds-schema-zendesk"></a>

You include a JSON that contains the data source schema as part of [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) object\. You provide the host URL as a part of the connection configuration or repository endpoint details\. Also specify the type of data source as `ZENDESK`, a secret for your authentication credentials, and other necessary configurations\. You then specify `TEMPLATE` as the **Type** when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\.

You can use the template provided in this developer guide\. See [Zendesk JSON schema](#zendesk-json)\.

The following provides information on important JSON keys to configure\.


| Configuration | Description | 
| --- | --- | 
| connectionConfiguration | Configuration information for the endpoint for the data source | 
| repositoryEndpointMetadata | The endpoint information for the data source | 
| hostURL | The Zendesk host URL\. For example, https://yoursubdomain\.zendesk\.com | 
| repositoryConfigurations | Configuration information for the content of the data source\. For example, configuring specific types of content and field mappings\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  |  A list of objects that map attributes or field names of Zendesk tickets to Amazon Kendra index field names\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Zendesk data source field names must exist in your Zendesk custom metadata\. | 
| secretARN | The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Zendesk\. The secret must contain a JSON structure with the following keys: host URL, client ID, client secret, user name, and password\. | 
| additionalProperties | Additional configuration options for your content in your data source | 
| organizationFilter | If desired, you can choose to index tickets that exist within a specific Organization | 
| sinceDate |  If desired, you can configure a sinceDate parameter so the Zendesk connector will crawl based on the sinceDate\. | 
| inclusionPatterns | A list of regular expression patterns to include certain files in your Zendesk data source\. Files that match the patterns are included in the index\. File that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
| exclusionPatterns | A list of regular expression patterns to exclude certain files in your Zendesk data source\. Files that match the patterns are excluded from the index\. X that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\. | 
|  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/kendra/latest/dg/ds-schemas.html)  | Input TRUE to index | 
| type | Specify ZENDESK as your data source type\. | 
| useChangeLog | Input TRUEto use the Zendesk change log to determine which documents require updating in the index\. Depending on the change log's size, it might be faster to scan the documents in Zendesk\. If you are syncing your Zendesk data source with your index for the first time, all documents are scanned\. | 

### Zendesk JSON schema<a name="zendesk-json"></a>

```
{

  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "connectionConfiguration": {
      "type": "object",
      "properties": {
        "repositoryEndpointMetadata": {
          "type": "object",
          "properties": {
            "hostUrl": {
              "type": "string",
              "pattern": "https:.*"
            }
          },
          "required": [
            "hostUrl"
          ]
        }
      },
      "required": [
        "repositoryEndpointMetadata"
      ]
    },
    "repositoryConfigurations": {
      "type": "object",
      "properties": {
        "ticket": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"

                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "ticketComment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"

                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "ticketCommentAttachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "article": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "communityPostComment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "articleComment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "articleAttachment": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        },
        "communityTopic": {
          "type": "object",
          "properties": {
            "fieldMappings": {
              "type": "array",
              "items": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "indexFieldName": {
                        "type": "string"
                      },
                      "indexFieldType": {
                        "type": "string",
                        "enum": ["STRING", "STRING_LIST", "LONG", "DATE"]
                      },
                      "dataSourceFieldName": {
                        "type": "string"
                      },
                      "dateFieldFormat": {
                        "type": "string",
                        "pattern": "dd-MM-yyyy HH:mm:ss"
                      }
                    },
                    "required": [
                      "indexFieldName",
                      "indexFieldType",
                      "dataSourceFieldName"
                    ]
                  }
                ]
              }
            }
          },
          "required": [
            "fieldMappings"
          ]
        }
      }
    },
    "secretArn": {
      "type": "string",
      "minLength": 20,
      "maxLength": 2048
    },
    "additionalProperties": {
      "type": "object",
      "properties": {
        "organizationNameFilter": {
          "type": "array"
        },
        "sinceDate": {
          "type": "string",
          "pattern": "^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}$"
        },
        "inclusionPatterns": {
          "type": "array"
        },
        "exclusionPatterns": {
          "type": "array"
        },
        "isCrawTicket": {
          "type": "string"
        },
        "isCrawTicketComment": {
          "type": "string"
        },
        "isCrawTicketCommentAttachment": {
          "type": "string"
        },
        "isCrawlArticle": {
          "type": "string"
        },
        "isCrawlArticleAttachment": {
          "type": "string"
        },
        "isCrawlArticleComment": {
          "type": "string"
        },
        "isCrawlCommunityTopic": {
          "type": "string"
        },
        "isCrawlCommunityPost": {
          "type": "string"
        },
        "isCrawlCommunityPostComment": {
          "type": "string"
        }
      }
    },
    "type": {
      "type": "string",
      "pattern": "ZENDESK"
    },
    "useChangeLog": {
      "type": "string",
      "enum": ["true", "false"]
    }
  },
  "version": {
    "type": "string",
    "anyOf": [
      {
        "pattern": "1.0.0"
      }
    ]
  },
  "additionalProperties": false,
  "required": [
    "connectionConfiguration",
    "repositoryConfigurations",
    "additionalProperties",
    "useChangeLog",
    "secretArn",
    "type"
  ]
}
```