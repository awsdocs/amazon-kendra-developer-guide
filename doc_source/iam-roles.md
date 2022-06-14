--------

--------

# IAM access roles for Amazon Kendra<a name="iam-roles"></a>

When you create an index, data source, or an FAQ, Amazon Kendra needs access to the AWS resources required to create the Amazon Kendra resource\. You must create a AWS Identity and Access Management \(IAM\) policy before you create the Amazon Kendra resource\. When you call the operation, you provide the Amazon Resource Name \(ARN\) of the role with the policy attached\. For example, if you are calling the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API to add documents from an Amazon S3 bucket, you provide Amazon Kendra with a role with a policy that has access to the bucket\.

You can create a new IAM role in the Amazon Kendra console or choose an IAM existing role to use\. The console displays roles that have the string "kendra" or "Kendra" in the role name\. 

The following topics provide details for the required policies\. If you create IAM roles using the Amazon Kendra console these policies are created for you\.

**Topics**
+ [IAM roles for indexes](#iam-roles-index)
+ [IAM roles for the BatchPutDocument API](#iam-roles-batch)
+ [IAM roles for data sources](#iam-roles-ds)
+ [IAM roles for frequently asked questions](#iam-roles-ds-faq)
+ [IAM roles for query suggestions](#iam-roles-query-suggestions)
+ [IAM roles for principal mapping of users and groups](#iam-roles-principal-mapping)
+ [IAM roles for AWS Single Sign\-On](#iam-roles-aws-sso)
+ [IAM roles for Amazon Kendra experiences](#iam-roles-amazon-kendra-experiences)
+ [IAM roles for Custom Document Enrichment](#iam-roles-custom-document-enrichment)

## IAM roles for indexes<a name="iam-roles-index"></a>

When you create an index, you must provide an IAM role with permission to write to an Amazon CloudWatch\. You must also provide a trust policy that allows Amazon Kendra to assume the role\. The following are the policies that must be provided\.

A role policy to allow Amazon Kendra to access a CloudWatch log\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "cloudwatch:PutMetricData",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "cloudwatch:namespace": "Kendra"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": "logs:DescribeLogGroups",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "logs:CreateLogGroup",
            "Resource": "arn:aws:logs:region:account ID:log-group:/aws/kendra/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:DescribeLogStreams",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "arn:aws:logs:region:account ID:log-group:/aws/kendra/*:log-stream:*"
        }
    ]
}
```

A role policy to allow Amazon Kendra to access AWS Secrets Manager\. If you are using user context with Secrets Manager as a key location, you can use the following policy\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":"cloudwatch:PutMetricData",
         "Resource":"*",
         "Condition":{
            "StringEquals":{
               "cloudwatch:namespace":"Kendra"
            }
         }
      },
      {
         "Effect":"Allow",
         "Action":"logs:DescribeLogGroups",
         "Resource":"*"
      },
      {
         "Effect":"Allow",
         "Action":"logs:CreateLogGroup",
         "Resource":"arn:aws:logs:region:account ID:log-group:/aws/kendra/*"
      },
      {
         "Effect":"Allow",
         "Action":[
            "logs:DescribeLogStreams",
            "logs:CreateLogStream",
            "logs:PutLogEvents"
         ],
         "Resource":"arn:aws:logs:region:account ID:log-group:/aws/kendra/*:log-stream:*"
      },
      {
         "Effect":"Allow",
         "Action":[
            "secretsmanager:GetSecretValue"
         ],
         "Resource":[
            "arn:aws:secretsmanager:region:account ID:secret:secret_id"
         ]
      },
      {
         "Effect":"Allow",
         "Action":[
            "kms:Decrypt"
         ],
         "Resource":[
            "arn:aws:kms:region:account ID:key/key_id"
         ],
         "Condition":{
            "StringLike":{
               "kms:ViaService":[
                  "secretsmanager.*.amazonaws.com"
               ]
            }
         }
      }
   ]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

## IAM roles for the BatchPutDocument API<a name="iam-roles-batch"></a>

**Warning**  
Amazon Kendra doesn't use a bucket policy that grants permissions to an Amazon Kendra principal to interact with an S3 bucket\. Instead, it uses IAM roles\. Make sure that Amazon Kendra isn't included as a trusted member in your bucket policy to avoid any data security issues in accidentally granting permissions to arbitrary principals\. However, you can add a bucket policy to use an Amazon S3 bucket across different accounts\. For more information, see [Policies to use Amazon S3 across accounts](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3-cross-accounts)\. For information about IAM roles for S3 data sources, see [IAM roles](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3)\.

When you use the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) API to index documents in an Amazon S3 bucket, you must provide Amazon Kendra with an IAM role with access to the bucket\. You must also provide a trust policy that allows Amazon Kendra to assume the role\. If the documents in the bucket are encrypted, you must provide permission to use the AWS KMS customer master key \(CMK\) to decrypt the documents\.

A required role policy to allow Amazon Kendra to access an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ]
        }
    ]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

It is recommended that you include `aws:sourceAccount` and `aws:sourceArn` in the trust policy\. This limits permissions and securely checks if `aws:sourceAccount` and `aws:sourceArn` are the same as provided in the IAM role policy for the `sts:AssumeRole` action\. This prevents unauthorized entities from accessing your IAM roles and their permissions\. For more information, see the AWS Identity and Access Management guide on the [confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "kendra.amazonaws.com"
                ]
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account ID"
                },
                "StringLike": {
                    "aws:SourceArn": "arn:aws:kendra:region:accountId:index/*"
                }
            }
        }
    ]
}
```

An optional role policy to allow Amazon Kendra to use an AWS KMS customer master key \(CMK\) to decrypt documents in an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        }
    ]
}
```

## IAM roles for data sources<a name="iam-roles-ds"></a>

When you use the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API, you must give Amazon Kendra an IAM role that has permission to access the database resources\. The specific permissions required depend on the data source\.

**Topics**
+ [IAM roles for Amazon S3 data sources](#iam-roles-ds-s3)
+ [IAM roles for Confluence server data sources](#iam-roles-ds-cnf)
+ [IAM roles for database data sources](#iam-roles-ds-jdbc)
+ [IAM roles for Google Workspace Drive data sources](#iam-roles-ds-gd)
+ [IAM roles for Microsoft OneDrive data sources](#iam-roles-ds-on)
+ [IAM roles for Salesforce data sources](#iam-roles-ds-sf)
+ [IAM roles for ServiceNow data sources](#iam-roles-ds-sn)
+ [IAM roles for Microsoft SharePoint data sources](#iam-roles-ds-spo)
+ [Virtual private cloud \(VPC\) IAM role](#iam-roles-vpc)
+ [IAM roles for web crawler data sources](#iam-roles-ds-webcrawler)
+ [IAM roles for Amazon WorkDocs data sources](#iam-roles-workdocs)
+ [IAM roles for Amazon FSx data sources](#iam-roles-ds-fsx)
+ [IAM roles for Slack data sources](#iam-roles-ds-slack)
+ [IAM roles for Box data sources](#iam-roles-ds-box)
+ [IAM roles for Quip data sources](#iam-roles-ds-quip)
+ [IAM roles for Jira data sources](#iam-roles-ds-jira)
+ [IAM roles for GitHub data sources](#iam-roles-ds-github)

### IAM roles for Amazon S3 data sources<a name="iam-roles-ds-s3"></a>

**Warning**  
Amazon Kendra doesn't use a bucket policy that grants permissions to an Amazon Kendra principal to interact with an S3 bucket\. Instead, it uses IAM roles\. Make sure that Amazon Kendra isn't included as a trusted member in your bucket policy to avoid any data security issues in accidentally granting permissions to arbitrary principals\. However, you can add a bucket policy to use an Amazon S3 bucket across different accounts\. For more information, see [Policies to use Amazon S3 across accounts](#iam-roles-ds-s3-cross-accounts)\.

When you use an Amazon S3 bucket as a data source, you supply a role that has permission to access the bucket, and to use the `BatchPutDocument` and `BatchDeleteDocument` operations\. If the documents in the Amazon S3 bucket are encrypted, you must provide permission to use the AWS KMS customer master key \(CMK\) to decrypt the documents\.

A required role policy to allow Amazon Kendra to use an Amazon S3 bucket as a data source\.

```
{
    "Version": "2012-10-17",
    "Statement": [
         {
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name"
            ],
            "Effect": "Allow"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kendra:BatchPutDocument",
                "kendra:BatchDeleteDocument"
            ],
            "Resource": [
                "arn:aws:kendra:region:account ID:index/index ID"
            ]
        }
    ]
}
```

An optional role policy to allow Amazon Kendra to use an AWS KMS customer master key \(CMK\) to decrypt documents in an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        }
    ]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

#### Policies to use Amazon S3 across accounts<a name="iam-roles-ds-s3-cross-accounts"></a>

If your Amazon S3 bucket is in a different account to the account you use for your Amazon Kendra index, you can create policies to use it across accounts\.

A role policy to use your Amazon S3 bucket as your data source when the bucket is in a different account to your Amazon Kendra index\.

```
{
    "Version": "2012-10-17",
    "Statement": [
         {
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::$BUCKET_IN_OTHER_ACCOUNT/*"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::$BUCKET_IN_OTHER_ACCOUNT/*"
            ],
            "Effect": "Allow"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kendra:BatchPutDocument",
                "kendra:BatchDeleteDocument"
            ],
            "Resource": [
                "arn:aws:kendra:$KENDRA_REGION:$KENDRA_ACCOUNT_ID:index/$KENDRA_INDEX_ID"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::$BUCKET_IN_OTHER_ACCOUNT/*"
        }
    ]
}
```

A bucket policy to allow the Amazon S3 data source role to access the Amazon S3 bucket across accounts\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "$KENDRA_S3_CONNECTOR_ROLE_ARN"
            },
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:PutObjectAcl"
            ],
            "Resource": [
                "arn:aws:s3:::$BUCKET_IN_OTHER_ACCOUNT/*"
            ]
        },
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "$KENDRA_S3_CONNECTOR_ROLE_ARN"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::$BUCKET_IN_OTHER_ACCOUNT"
        }
    ]
}
```

##### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Confluence server data sources<a name="iam-roles-ds-cnf"></a>

When you use a Confluence server as a data source, you provide a role with the following policies:
+ Permission to access the AWS Secrets Manager secret that contains the credentials necessary to connect to the Confluence server\. For more information about the contents of the secret, see [Using an Atlassian Confluence data source](data-source-confluence.md)\.
+ Permission to use the AWS KMS customer master key \(CMK\) to decrypt the user name and password secret stored by Secrets Manager\.
+ Permission to use the `BatchPutDocument` and `BatchDeleteDocument` operations to update the index\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

If you are using a VPC, provide a policy that gives Amazon Kendra access to the required resources\. See [Virtual private cloud \(VPC\) IAM role](#iam-roles-vpc) for the required policy\.

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for database data sources<a name="iam-roles-ds-jdbc"></a>

When you use a database as a data source, you provide Amazon Kendra with a role that has the permissions necessary for connecting to the database\. These include:
+ Permission to access the AWS Secrets Manager secret that contains the user name and password for the database site\. For more information about the contents of the secret, see [Using a database data source](data-source-database.md)\.
+ Permission to use the AWS KMS customer master key \(CMK\) to decrypt the user name and password secret stored by Secrets Manager\.
+ Permission to use the `BatchPutDocument` and `BatchDeleteDocument` operations to update the index\.
+ Permission to access the Amazon S3 bucket that contains the SSL certificate used to communicate with the database site\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "secretsmanager:GetSecretValue"
            ],
            "Resource": [
                "arn:aws:secretsmanager:region:account ID:secret:secret ID"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "kendra:BatchPutDocument",
                "kendra:BatchDeleteDocument"
            ],
            "Resource": [
                "arn:aws:kendra:region:account ID:index/index ID"
            "Condition": {
                "StringLike": {
                    "kms:ViaService": [
                        "kendra.amazonaws.com"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ]
        }
    ]
}
```

There are two optional policies that you might use with a database data source\.

If you have encrypted the Amazon S3 bucket that contains the SSL certificate used to communicate with the database, provide a policy to give Amazon Kendra access to the key\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        }
    ]
}
```

If you are using a VPC, provide a policy that gives Amazon Kendra access to the required resources\. See [Virtual private cloud \(VPC\) IAM role](#iam-roles-vpc) for the required policy\.

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Google Workspace Drive data sources<a name="iam-roles-ds-gd"></a>

When you use a Google Workspace Drive data source, you provide Amazon Kendra with a role that has the permissions necessary for connecting to the site\. These include: 
+ Permission to get and decrypt the AWS Secrets Manager secret that contains the client account email, admin account email, and private key necessary to connect to the Google Drive site\. For more information about the contents of the secret, see [Using a Google Workspace Drive data source](data-source-google-drive.md)\.
+ Permission to use the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) and [BatchDeleteDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchDeleteDocument.html) APIs\.

The following IAM policy provides the necessary permissions:

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Microsoft OneDrive data sources<a name="iam-roles-ds-on"></a>

When you use a Microsoft OneDrive data source, you provide Amazon Kendra with a role that has the permissions necessary for connecting to the site\. These include: 
+ Permission to get and decrypt the AWS Secrets Manager secret that contains the application ID and secret key necessary to connect to the OneDrive site\. For more information about the contents of the secret, see [Using a Microsoft OneDrive data source](data-source-onedrive.md)\.
+ Permission to use the [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) and [BatchDeleteDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchDeleteDocument.html) APIs\.

The following IAM policy provides the necessary permissions:

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

If you are storing the list of users to index in an Amazon S3 bucket, you must also provide permission to use the S3 `GetObject` operation\. The following IAM policy provides the necessary permissions:

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Action": [
      "s3:GetObject"
    ],
    "Resource": [
      "arn:aws:s3:::input_bucket_name/*"
    ],
    "Effect": "Allow"
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/[[key IDs]]"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com",
          "s3.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Salesforce data sources<a name="iam-roles-ds-sf"></a>

When you use a Salesforce as a data source, you provide a role with the following policies:
+ Permission to access the AWS Secrets Manager secret that contains the user name and password for the Salesforce site\. For more information about the contents of the secret, see [Using a Salesforce data source](data-source-salesforce.md)\.
+ Permission to use the AWS KMS customer master key \(CMK\) to decrypt the user name and password secret stored by Secrets Manager\.
+ Permission to use the `BatchPutDocument` and `BatchDeleteDocument` operations to update the index\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for ServiceNow data sources<a name="iam-roles-ds-sn"></a>

When you use a ServiceNow as a data source, you provide a role with the following policies:
+ Permission to access the Secrets Manager secret that contains the user name and password for the ServiceNow site\. For more information about the contents of the secret, see [Using a ServiceNow data source](data-source-servicenow.md)\.
+ Permission to use the AWS KMS customer master key \(CMK\) to decrypt the user name and password secret stored by Secrets Manager\.
+ Permission to use the `BatchPutDocument` and `BatchDeleteDocument` operations to update the index\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Microsoft SharePoint data sources<a name="iam-roles-ds-spo"></a>

For a Microsoft SharePoint data source, you provide a role with the following policies\.
+ Permission to access the AWS Secrets Manager secret that contains the user name and password for the SharePoint site\. For more information about the contents of the secret, see [Using a Microsoft SharePoint data source](data-source-sharepoint.md)\.
+ Permission to use the AWS KMS customer master key \(CMK\) to decrypt the user name and password secret stored by AWS Secrets Manager\.
+ Permission to use the `BatchPutDocument` and `BatchDeleteDocument` operations to update the index\.
+ Permission to access the Amazon S3 bucket that contains the SSL certificate used to communicate with the SharePoint site\.

You must also attach a trust policy that allows Amazon Kendra to assume the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "secretsmanager:GetSecretValue"
            ],
            "Resource": [
                "arn:aws:secretsmanager:region:account ID:secret:secret ID"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "kendra:BatchPutDocument",
                "kendra:BatchDeleteDocument"
            ],
            "Resource": [
                "arn:aws:kendra:region:account ID:index/index ID"
            ],
            "Condition": {
                "StringLike": {
                    "kms:ViaService": [
                        "kendra.amazonaws.com"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ]
        }
    ]
}
```

If you have encrypted the Amazon S3 bucket that contains the SSL certificate used to communicate with the SharePoint site, provide a policy to give Amazon Kendra access to the key\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        }
    ]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### Virtual private cloud \(VPC\) IAM role<a name="iam-roles-vpc"></a>

If you use a virtual private cloud \(VPC\) to connect to your data source, you must provide the following permissions\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:CreateNetworkInterface",
        "ec2:DescribeNetworkInterfaces",
        "ec2:DeleteNetworkInterface"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:CreateNetworkInterfacePermission"
      ],
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "ec2:AuthorizedService": "kendra.amazonaws.com"
        },
        "ArnEquals": {
          "ec2:Subnet": [
            "arn:aws:ec2:region:account ID:subnet/subnet IDs"
          ]
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeSubnets"
      ],
      "Resource": "*"
    },
    {
      "Sid": "iamPassRole",
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": [
            "kendra.amazonaws.com"
          ]
        }
      }
    }
  ]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for web crawler data sources<a name="iam-roles-ds-webcrawler"></a>

When you use Amazon Kendra Web Crawler, you provide a role with the following policies:
+ Permission to access the AWS Secrets Manager secret that contains the user name and password to connect to websites or a web proxy server backed by basic authentication\. For more information about the contents of the secret, see [Using a web crawler data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-web-crawler.html)\.
+ Permission to use the AWS KMS customer master key \(CMK\) to decrypt the user name and password secret stored by Secrets Manager\.
+ Permission to use the `BatchPutDocument` and `BatchDeleteDocument` operations to update the index\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:region:account ID:secret:secret ID"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:region:account ID:key/key ID"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:region:account ID:index/index ID"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Amazon WorkDocs data sources<a name="iam-roles-workdocs"></a>

When you use Amazon WorkDocs, you provide a role with the following policies
+ Permission to verify the directory ID \(organization ID\) that corresponds with your Amazon WorkDocs site repository\.
+ Permission to get the domain name of your Active Directory that contains your Amazon WorkDocs site directory\.
+ Permission to call the required public APIs for the Amazon WorkDocs connector\.
+ Permission to call the `BatchPutDocument` and `BatchDeleteDocument` APIs to update the index\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowsKendraToGetDomainNameOfActiveDirectory",
      "Effect": "Allow",
      "Action": "ds:DescribeDirectories",
      "Resource": "*"
    },
    {
      "Sid": "AllowsKendraToCallRequiredWorkDocsAPIs",
      "Effect": "Allow",
      "Action": [
        "workdocs:GetDocumentPath",
        "workdocs:GetGroup",
        "workdocs:GetDocument",
        "workdocs:DownloadDocumentVersions",
        "workdocs:DescribeUsers",
        "workdocs:DescribeFolderContents",
        "workdocs:DescribeActivities",
        "workdocs:DescribeComments",
        "workdocs:GetFolder",
        "workdocs:DescribeResourcePermissions",
        "workdocs:GetFolderPath",
        "workdocs:DescribeInstances"
      ],
      "Resource": "*"
    },
    {
      "Sid": "iamPassRole",
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": [
            "kendra.amazonaws.com"
          ]
        }
      }
    },
    {
      "Sid": "AllowsKendraToCallBatchPutDeleteAPIs",
      "Effect": "Allow",
      "Action": [
        "kendra:BatchPutDocument",
        "kendra:BatchDeleteDocument"
      ],
      "Resource": [
        "arn:aws:kendra:{{region}}:{{account_id}}:index/${IndexId}"
      ]
    }
  ]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Amazon FSx data sources<a name="iam-roles-ds-fsx"></a>

When you use Amazon FSx, you provide a role with the following policies\.
+ Permission to access your AWS Secrets Manager secret to authenticate your Amazon FSx\.
+ Permission to access Amazon Virtual Private Cloud \(VPC\) where your Amazon FSx resides\.
+ Permission to get the domain name of your Active Directory for your Amazon FSx Windows file system\.
+ Permission to call the required public APIs for the Amazon FSx connector\.
+ Permission to call the `BatchPutDocument` and `BatchDeleteDocument` APIs to update the index\.

```
{
    "Version": "2012-10-17",
        "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "secretsmanager:GetSecretValue"
          ],
          "Resource": [
            "arn:aws:secretsmanager:{{region}}:{{account_id}}:secret:{{secret_id}}"
          ]
        },
        {
          "Effect": "Allow",
          "Action": [
            "kms:Decrypt"
          ],
          "Resource": [
            "arn:aws:kms:{{region}}:{{account_id}}:key/{{key_id}}"
          ],
          "Condition": {
            "StringLike": {
              "kms:ViaService": [
                "secretsmanager.{{region}}.amazonaws.com"
              ]
            }
          }
        },
        {
          "Effect": "Allow",
          "Action":[
            "ec2:CreateNetworkInterface",
            "ec2:DeleteNetworkInterface"
          ],
          "Resource": [
                "arn:aws:ec2:{{region}}:{{account_id}}:network-interface/*",
                "arn:aws:ec2:{{region}}:{{account_id}}:subnet/[[subnet_ids]]"
          ]   
        },
        {
          "Effect": "Allow",
          "Action": [
            "ec2:DescribeSubnets",
            "ec2:DescribeNetworkInterfaces"
          ],
          "Resource": "*"
        },
        {
          "Effect": "Allow",
          "Action": [
            "ec2:CreateNetworkInterfacePermission"
          ],
          "Resource": "arn:aws:ec2:{{region}}:{{account_id}}:network-interface/*",
          "Condition": {
            "StringEquals": {
              "ec2:AuthorizedService": "kendra.amazonaws.com"
            },
            "ArnEquals": {
              "ec2:Subnet": [
                "arn:aws:ec2:{{region}}:{{account_id}}:subnet/[[subnet_ids]]"
              ]
            }
          }
        },
        {
          "Sid": "AllowsKendraToGetDomainNameOfActiveDirectory",
          "Effect": "Allow",
          "Action": "ds:DescribeDirectories",
          "Resource": "*"
        },
        {
          "Sid": "AllowsKendraToCallRequiredFsxAPIs",
          "Effect": "Allow",
          "Action": [
              "fsx:DescribeFileSystems"
          ],
          "Resource": "*"
        },
        {
          "Sid": "iamPassRole",
          "Effect": "Allow",
          "Action": "iam:PassRole",
          "Resource": "*",
          "Condition": {
            "StringEquals": {
              "iam:PassedToService": [
                "kendra.amazonaws.com"
              ]
            }
          }
        },
        {
          "Effect": "Allow",
          "Action": [
            "kendra:BatchPutDocument",
            "kendra:BatchDeleteDocument"
          ],
          "Resource": "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}"
        }
        ]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Slack data sources<a name="iam-roles-ds-slack"></a>

When you use Slack, you provide a role with the following policies\.
+ Permission to access your AWS Secrets Manager secret to authenticate your Slack\.
+ Permission to call the required public APIs for the Slack connector\.
+ Permission to call the `BatchPutDocument`, `BatchDeleteDocument`, `PutPrincipalMapping`, `DeletePrincipalMapping`, `DescribePrincipalMapping`, and `ListGroupsOlderThanOrderingId` APIs\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:{{region}}:{{account_id}}:secret:[[secret_id]]"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:{{region}}:{{account_id}}:key/[[key_id]]"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
        "kendra:PutPrincipalMapping",
        "kendra:DeletePrincipalMapping",
        "kendra:ListGroupsOlderThanOrderingId",
        "kendra:DescribePrincipalMapping"
    ],
    "Resource": ["arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}", "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}/data-source/*"]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Box data sources<a name="iam-roles-ds-box"></a>

When you use Box, you provide a role with the following policies\.
+ Permission to access your AWS Secrets Manager secret to authenticate your Slack\.
+ Permission to call the required public APIs for the Box connector\.
+ Permission to call the `BatchPutDocument`, `BatchDeleteDocument`, `PutPrincipalMapping`, `DeletePrincipalMapping`, `DescribePrincipalMapping`, and `ListGroupsOlderThanOrderingId` APIs\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:{{region}}:{{account_id}}:secret:[[secret_id]]"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:{{region}}:{{account_id}}:key/[[key_id]]"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
        "kendra:PutPrincipalMapping",
        "kendra:DeletePrincipalMapping",
        "kendra:ListGroupsOlderThanOrderingId",
        "kendra:DescribePrincipalMapping"
    ],
    "Resource": ["arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}", "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}/data-source/*"]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Quip data sources<a name="iam-roles-ds-quip"></a>

When you use Quip, you provide a role with the following policies\.
+ Permission to access your AWS Secrets Manager secret to authenticate your Quip\.
+ Permission to call the required public APIs for the Quip connector\.
+ Permission to call the `BatchPutDocument`, `BatchDeleteDocument`, `PutPrincipalMapping`, `DeletePrincipalMapping`, `DescribePrincipalMapping`, and `ListGroupsOlderThanOrderingId` APIs\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:{{region}}:{{account_id}}:secret:[[secret_id]]"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:{{region}}:{{account_id}}:key/[[key_id]]"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
        "kendra:PutPrincipalMapping",
        "kendra:DeletePrincipalMapping",
        "kendra:ListGroupsOlderThanOrderingId",
        "kendra:DescribePrincipalMapping"
    ],
    "Resource": ["arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}", "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}/data-source/*"]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for Jira data sources<a name="iam-roles-ds-jira"></a>

When you use Jira, you provide a role with the following policies\.
+ Permission to access your AWS Secrets Manager secret to authenticate your Jira\.
+ Permission to call the required public APIs for the Jira connector\.
+ Permission to call the `BatchPutDocument`, `BatchDeleteDocument`, `PutPrincipalMapping`, `DeletePrincipalMapping`, `DescribePrincipalMapping`, and `ListGroupsOlderThanOrderingId` APIs\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:{{region}}:{{account_id}}:secret:[[secret_id]]"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:{{region}}:{{account_id}}:key/[[key_id]]"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
        "kendra:PutPrincipalMapping",
        "kendra:DeletePrincipalMapping",
        "kendra:ListGroupsOlderThanOrderingId",
        "kendra:DescribePrincipalMapping"
    ],
    "Resource": ["arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}", "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}/data-source/*"]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

### IAM roles for GitHub data sources<a name="iam-roles-ds-github"></a>

When you use GitHub, you provide a role with the following policies\.
+ Permission to access your AWS Secrets Manager secret to authenticate your GitHub\.
+ Permission to call the required public APIs for the GitHub connector\.
+ Permission to call the `BatchPutDocument`, `BatchDeleteDocument`, `PutPrincipalMapping`, `DeletePrincipalMapping`, `DescribePrincipalMapping`, and `ListGroupsOlderThanOrderingId` APIs\.

```
{
  "Version": "2012-10-17",
  "Statement": [
  {
    "Effect": "Allow",
    "Action": [
      "secretsmanager:GetSecretValue"
    ],
    "Resource": [
      "arn:aws:secretsmanager:{{region}}:{{account_id}}:secret:[[secret_id]]"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt"
    ],
    "Resource": [
      "arn:aws:kms:{{region}}:{{account_id}}:key/[[key_id]]"
    ],
    "Condition": {
      "StringLike": {
        "kms:ViaService": [
          "secretsmanager.*.amazonaws.com"
        ]
      }
    }
  },
  {
    "Effect": "Allow",
    "Action": [
        "kendra:PutPrincipalMapping",
        "kendra:DeletePrincipalMapping",
        "kendra:ListGroupsOlderThanOrderingId",
        "kendra:DescribePrincipalMapping"
    ],
    "Resource": ["arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}", "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}/data-source/*"]
  },
  {
    "Effect": "Allow",
    "Action": [
      "kendra:BatchPutDocument",
      "kendra:BatchDeleteDocument"
    ],
    "Resource": "arn:aws:kendra:{{region}}:{{account_id}}:index/{{index_id}}"
  }]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

## IAM roles for frequently asked questions<a name="iam-roles-ds-faq"></a>

When you use the [CreateFaq](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateFaq.html) API to load questions and answers into an index, you must provide Amazon Kendra with an IAM role with access to the Amazon S3 bucket that contains the source files\. If the source files are encrypted, you must provide permission to use the AWS KMS customer master key \(CMK\) to decrypt the files\.

A required role policy to allow Amazon Kendra to access an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ]
        }
    ]
}
```

An optional role policy to allow Amazon Kendra to use an AWS KMS customer master key \(CMK\) to decrypt files in an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ],
            "Condition": {
                "StringLike": {
                    "kms:ViaService": [
                        "kendra.amazonaws.com"
                    ]
                }
            }
        }
    ]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

## IAM roles for query suggestions<a name="iam-roles-query-suggestions"></a>

When you use an Amazon S3 file as a query suggestions block list, you supply a role that has permission to access the Amazon S3 file and the Amazon S3 bucket\. If the block list text file \(the Amazon S3 file\) in the Amazon S3 bucket is encrypted, you must provide permission to use the AWS KMS customer master key \(CMK\) to decrypt the documents\.

A required role policy to allow Amazon Kendra to use the Amazon S3 file as your query suggestions block list\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {"Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ]
        }
    ]
}
```

An optional role policy to allow Amazon Kendra to use an AWS KMS customer master key \(CMK\) to decrypt documents in an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {"Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        }
    ]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

## IAM roles for principal mapping of users and groups<a name="iam-roles-principal-mapping"></a>

When you use the [PutPrincipalMapping](https://docs.aws.amazon.com/kendra/latest/dg/API_PutPrincipalMapping.html) API to map users to their groups for filtering search results by user context, you need to provide a list of users or sub groups that belong to a group\. If your list is more than 1000 users or sub groups for a group, you need to supply a role that has permission to access the Amazon S3 file of your list and the Amazon S3 bucket\. If the text file \(the Amazon S3 file\) of the list in the Amazon S3 bucket is encrypted, you must provide permission to use the AWS KMS customer master key \(CMK\) to decrypt the documents\.

A required role policy to allow Amazon Kendra to use the Amazon S3 file as your list of users and sub groups that belong to a group\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {"Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket name/*"
            ]
        }
    ]
}
```

An optional role policy to allow Amazon Kendra to use an AWS KMS customer master key \(CMK\) to decrypt documents in an Amazon S3 bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {"Effect": "Allow",
            "Action": [
                "kms:Decrypt"
            ],
            "Resource": [
                "arn:aws:kms:region:account ID:key/key ID"
            ]
        }
    ]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

It is recommended that you include `aws:sourceAccount` and `aws:sourceArn` in the trust policy\. This limits permissions and securely checks if `aws:sourceAccount` and `aws:sourceArn` are the same as provided in the IAM role policy for the `sts:AssumeRole` action\. This prevents unauthorized entities from accessing your IAM roles and their permissions\. For more information, see the AWS Identity and Access Management guide on the [confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "kendra.amazonaws.com"
                ]
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account ID"
                },
                "StringLike": {
                    "aws:SourceArn": "arn:aws:kendra:region:accountId:index/*"
                }
            }
        }
    ]
}
```

## IAM roles for AWS Single Sign\-On<a name="iam-roles-aws-sso"></a>

When you use the [UserGroupResolutionConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_UserGroupResolutionConfiguration.html) object to fetch access levels of groups and users from an AWS Single Sign\-On identity source, you need to supply a role that has permission to access AWS SSO\.

A required role policy to allow Amazon Kendra to access AWS SSO\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sso-directory:SearchUsers",
                "sso-directory:ListGroupsForUser",
                "sso-directory:DescribeGroups",
                "sso:ListDirectoryAssociations"
            ],
            "Resource": [
                 "*"
            ]
        },
        {
          "Sid": "iamPassRole",
          "Effect": "Allow",
          "Action": "iam:PassRole",
          "Resource": "*",
          "Condition": {
            "StringEquals": {
              "iam:PassedToService": [
                "kendra.amazonaws.com"
              ]
            }
          }
        }
     ]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

## IAM roles for Amazon Kendra experiences<a name="iam-roles-amazon-kendra-experiences"></a>

### IAM roles for Amazon Kendra search experience<a name="iam-roles-search-app-experience"></a>

When you use the [CreateExperience](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateExperience.html) or [UpdateExperience](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateExperience.html) APIs to create or update a search application, you must supply a role that has permission to access the necessary operations and AWS Single Sign\-On\.

A required role policy to allow Amazon Kendra to access `Query` operations, `QuerySuggestions` operations, `SubmitFeedback` operations, and AWS SSO that stores your user and group information\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowsKendraSearchAppToCallKendraApi",
      "Effect": "Allow",
      "Action": [
        "kendra:GetQuerySuggestions",
        "kendra:Query",
        "kendra:DescribeIndex",
        "kendra:ListFaqs",
        "kendra:DescribeDataSource",
        "kendra:ListDataSources",
        "kendra:DescribeFaq"
      ],
      "Resource": [
        "arn:aws:kendra:{{region}}:{{account_id}}:index/{{IndexId}}"
      ]
    },
    {
      "Sid": "AllowKendraSearchAppToDescribeDataSourcesAndFaq",
      "Effect": "Allow",
      "Action": [
        "kendra:DescribeDataSource",
        "kendra:DescribeFaq"
      ],
      "Resource": [
        "arn:aws:kendra:{{region}}:{{account_id}}:index/{{IndexId}}/data-source/{{DataSourceId}}",
        "arn:aws:kendra:{{region}}:{{account_id}}:index/{{IndexId}}/faq/{{FaqId}}"
      ]
    },
    {
      "Sid": "AllowKendraSearchAppToCallSSODescribeUsersAndGroups",
      "Effect": "Allow",
      "Action": [
        "sso-directory:ListGroupsForUser",
        "sso-directory:SearchGroups",
        "sso-directory:SearchUsers",
        "sso-directory:DescribeUser",
        "sso-directory:DescribeGroup",
        "sso-directory:DescribeGroups",
        "sso-directory:DescribeUsers"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringLike": {
          "kms:ViaService": [
            "kendra.amazonaws.com"
          ]
        }
      }
    }
  ]
}
```

#### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

It is recommended that you include `aws:sourceAccount` and `aws:sourceArn` in the trust policy\. This limits permissions and securely checks if `aws:sourceAccount` and `aws:sourceArn` are the same as provided in the IAM role policy for the `sts:AssumeRole` action\. This prevents unauthorized entities from accessing your IAM roles and their permissions\. For more information, see the AWS Identity and Access Management guide on the [confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "kendra.amazonaws.com"
                ]
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account ID"
                },
                "StringLike": {
                    "aws:SourceArn": "arn:aws:kendra:region:accountId:index/*"
                }
            }
        }
    ]
}
```

## IAM roles for Custom Document Enrichment<a name="iam-roles-custom-document-enrichment"></a>

When you use the [CustomDocumentEnrichmentConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CustomDocumentEnrichmentConfiguration.html) object to apply advanced alterations of your document metadata and content, you must supply a role that has the required permissions to run `PreExtractionHookConfiguration` and/or `PostExtractionHookConfiguration`\. You configure a Lambda function for `PreExtractionHookConfiguration` and/or `PostExtractionHookConfiguration` to apply advanced alterations of your document metadata and content during the ingestion process\. If you choose to enable Server Side Encryption for your Amazon S3 bucket, you must provide permission to use the AWS KMS customer master key \(CMK\) to encrypt and decrypt the objects stored in your Amazon S3 bucket\.

A required role policy to allow Amazon Kendra to run `PreExtractionHookConfiguration` and `PostExtractionHookConfiguration` with encryption for your Amazon S3 bucket\.

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Action": [
      "s3:GetObject",
      "s3:PutObject"
    ],
    "Resource": [
      "arn:aws:s3:::{{input_bucket_name}}/*"
    ],
    "Effect": "Allow"
  },
  {
    "Action": [
      "s3:ListBucket"
    ],
    "Resource": [
      "arn:aws:s3:::{{input_bucket_name}}"
    ],
    "Effect": "Allow"
  },
  {
    "Effect": "Allow",
    "Action": [
      "kms:Decrypt",
      "kms:GenerateDataKey"
    ],
    "Resource": [
      "arn:aws:kms:{{region}}:{{account_id}}:key/{{key_id}}"
    ]
  },
  {
    "Effect": "Allow",
    "Action": [
      "lambda:InvokeFunction"
    ],
    "Resource": "arn:aws:lambda:{{region}}:{{account_id}}:function:{{lambda_function}}"
  }]
}
```

An optional role policy to allow Amazon Kendra to run `PreExtractionHookConfiguration` and `PostExtractionHookConfiguration` without encryption for your Amazon S3 bucket\.

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Action": [
      "s3:GetObject",
      "s3:PutObject"
    ],
    "Resource": [
      "arn:aws:s3:::{{input_bucket_name}}/*"
    ],
    "Effect": "Allow"
  },
  {
    "Action": [
      "s3:ListBucket"
    ],
    "Resource": [
      "arn:aws:s3:::{{input_bucket_name}}"
    ],
    "Effect": "Allow"
  },
  {
    "Effect": "Allow",
    "Action": [
      "lambda:InvokeFunction"
    ],
    "Resource": "arn:aws:lambda:{{region}}:{{account_id}}:function:{{lambda_function}}"
  }]
}
```

### <a name="iam-trust-policy-assume-role"></a>

A trust policy to allow Amazon Kendra to assume a role\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":{
            "Service":"kendra.amazonaws.com"
         },
         "Action":"sts:AssumeRole"
      }
   ]
}
```

It is recommended that you include `aws:sourceAccount` and `aws:sourceArn` in the trust policy\. This limits permissions and securely checks if `aws:sourceAccount` and `aws:sourceArn` are the same as provided in the IAM role policy for the `sts:AssumeRole` action\. This prevents unauthorized entities from accessing your IAM roles and their permissions\. For more information, see the AWS Identity and Access Management guide on the [confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html)\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "kendra.amazonaws.com"
                ]
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "account ID"
                },
                "StringLike": {
                    "aws:SourceArn": "arn:aws:kendra:region:accountId:index/*"
                }
            }
        }
    ]
}
```