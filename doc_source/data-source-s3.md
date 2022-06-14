--------

--------

# Using an S3 data source<a name="data-source-s3"></a>

**Warning**  
Amazon Kendra doesn't use a bucket policy that grants permissions to an Amazon Kendra principal to interact with an S3 bucket\. Instead, it uses IAM roles\. Make sure that Amazon Kendra isn't included as a trusted member in your bucket policy to avoid any data security issues in accidentally granting permissions to arbitrary principals\. However, you can add a bucket policy to use an Amazon S3 bucket across different accounts\. For more information, see [Policies to use Amazon S3 across accounts](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3-cross-accounts)\. For information about IAM roles for S3 data sources, see [IAM roles](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds-s3)\.

You can use your S3 bucket repository of documents as a data source for Amazon Kendra\. For a walk\-through of how to use Amazon S3 in the console, see [Getting started with an Amazon S3 data source \(console\)](https://docs.aws.amazon.com/kendra/latest/dg/gs-console.html)\.

When you connect to Amazon S3 to index your documents, you specify the name of the S3 bucket that contains your documents\. You can specify glob patterns to include or exclude specific documents in your name of provider\.

You must create an index before you create the Amazon S3 data source\. For more information, see [CreateDataSource](API_CreateDataSource.md)\. You provide the ID of the index when you create the data source\.

To connect to Amazon S3, you specify the connection and other information in the console or by using the [S3DataSourceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_S3DataSourceConfiguration.html) object\. You provide the name of the Amazon S3 bucket you want to index\.

Before you can index your documents from your Amazon S3 bucket, your bucket must be in the same Region as the index and Amazon Kendra must have permission to access the bucket that contains your documents\. You can configure your Access Control List for your Amazon S3 bucket\. This contains information on user and group access to documents\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Amazon S3 bucket\. You provide the ARN of an IAM role using [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. For more information on permissions, see [IAM roles for Amazon S3 data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You also can add the following optional information:
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any document with a file name or file type that does't match the pattern is not indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.

The following examples demonstrate creating an Amazon S3 data source\. The examples assume that you have already created an index and an IAM role with permission to read the data from the index\. For more information about the IAM role, see [IAM roles for Amazon S3 data sources](iam-roles.md#iam-roles-ds-s3)\. For more information about creating an index, see [Creating an index](create-index.md)\.

------
#### [ CLI ]

```
aws kendra create-data-source \
 --index-id index ID \
 --name example-data-source \
 --type S3 \
 --configuration '{"S3Configuration":{"BucketName":"bucket name"}}' 
 --role-arn 'arn:aws:iam::account id:role:/role name
```

------
#### [ Python ]

The following snippet of Python code creates an Amazon S3 data source\. For the complete example, see [Getting started \(AWS SDK for Python \(Boto3\)\)](gs-python.md)\.

```
print("Create an Amazon S3 data source.")
    
    # Provide a name for the data source
    name = "getting-started-data-source"
    # Provide an optional description for the data source
    description = "Getting started data source."
    # Provide the IAM role ARN required for data sources
    role_arn = "arn:aws:iam::${accountID}:role/${roleName}"
    # Provide the data soource connection information
    s3_bucket_name = "S3-bucket-name"
    type = "S3"
    # Configure the data source
    configuration = {"S3DataSourceConfiguration":
        {
            "BucketName": s3_bucket_name
        }
    }

    data_source_response = kendra.create_data_source(
        Configuration = configuration,
        Name = name,
        Description = description,
        RoleArn = role_arn,
        Type = type,
        IndexId = index_id
    )
```

------

It can take some time to create your data source\. You can monitor the progress by using the [DescribeDataSource](API_DescribeDataSource.md) API\. When the data source status is `ACTIVE` the data source is ready to use\. 

The following examples demonstrate getting the status of a data source\.

------
#### [ CLI ]

```
aws kendra describe-data-source \
 --index-id index ID \
 --id data source ID
```

------
#### [ Python ]

The following snippet of Python code gets information about an S3 data source\. For the complete example, see [Getting started \(AWS SDK for Python \(Boto3\)\)](gs-python.md)\.

```
print("Wait for Amazon Kendra to create the data source.")

    while True:
        data_source_description = kendra.describe_data_source(
            Id = "data-source-id",
            IndexId = "index-id"
        )
        status = data_source_description["Status"]
        print(" Creating data source. Status: "+status)
        time.sleep(60)
        if status != "CREATING":
            break
```

------

This data source doesn't have a schedule, so it doesn't run automatically\. To index the data source, you call [StartDataSourceSyncJob](API_StartDataSourceSyncJob.md) to synchronize the index with the data source\.

The following examples demonstrate synchronizing a data source\.

------
#### [ CLI ]

```
aws kendra start-data-source-sync-job \
 --index-id index ID \
 --id data source ID
```

------
#### [ Python ]

The following snippet of Python code synchronizes an Amazon S3 data source\. For the complete example, see [Getting started \(AWS SDK for Python \(Boto3\)\)](gs-python.md)\.

```
print("Synchronize the data source.")

    sync_response = kendra.start_data_source_sync_job(
        Id = "data-source-id",
        IndexId = "index-id"
    )
```

------