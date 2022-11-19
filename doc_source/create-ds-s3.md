--------

--------

# Creating an Amazon S3 data source<a name="create-ds-s3"></a>

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