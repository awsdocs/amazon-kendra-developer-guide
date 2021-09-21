--------

--------

# Using a custom data source<a name="data-source-custom"></a>

Use a custom data source when you have a repository that Amazon Kendra doesn’t yet provide a data source connector for\. It enables you to see the same run history metrics that Amazon Kendra data sources provide even when you can't use Amazon Kendra's data sources to sync your repositories\. Use this to create a consistent sync monitoring experience between Amazon Kendra data sources and custom ones\. Specifically, use a custom data source to see sync metrics for a data source connector that you created using the [ BatchPutDocument ](API_BatchPutDocument.md) and [ BatchDeleteDocument ](API_BatchDeleteDocument.md) operations\.

When you create a custom data source, you have complete control over how the documents to index are selected\. Amazon Kendra only provides metric information that you can use to monitor your data source sync jobs\. You must create and run the crawler that determines the documents your data source indexes\.

You create an identifier for your custom data source using the console or by using the [ CreateDataSource ](API_CreateDataSource.md) operation\. To use the console, give your data source a name, and optionally a description and resource tags\. After the data source is created, a data source ID is shown\. Copy this ID to use when you synchronize the data source with the index\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/kendra/latest/dg/images/CustomDataSource.png)

You can also create a custom data source using the `CreateDataSource` operation\. The operation returns an ID to use when you synchronize the data source\. When you use the `CreateDataSource` operation to create a custom data source, you can't set the `Configuration`, `RoleArn` or `Schedule` parameters\. If you set these parameters, Amazon Kendra returns a `ValidationException` exception\.

To use a custom data source, create an application that is responsible for updating the Amazon Kendra index\. The application depends on a crawler that you create\. The crawler reads the documents in your repository and determines which should be sent to Amazon Kendra\. Your application should perform the following steps: 

1. Crawl your repository and make a list of the documents in your repository that have been added, updated, or deleted\.

1. Call the [ StartDataSourceSyncJob ](API_StartDataSourceSyncJob.md) operation to signal that a sync job is starting\. You provide a data source ID to identify the data source that is synchronizing\. Amazon Kendra returns a execution ID to identify a particular sync job\.

1. Call the [ BatchPutDocument ](API_BatchPutDocument.md) and [ BatchDeleteDocument ](API_BatchDeleteDocument.md) operations to add, update, and remove documents from the index\. You provide the data source ID and execution ID to identify the data source that is synchronizing and the job that this update is associated with\.

1. Call the [ StopDataSourceSyncJob ](API_StopDataSourceSyncJob.md) operation to signal the end of the sync job\. Once you call the `StopDataSourceSyncJob` operation, the associated execution ID is no longer valid\.

1. Call the [ ListDataSourceSyncJobs ](API_ListDataSourceSyncJobs.md) operation with the index and data source identifiers to list the sync jobs for the data source and to see metrics for the sync jobs\.

After you end a sync job, you can start a new synchronization job\. There can be a period of time before all of the submitted documents are added to the index\. Use the `ListDataSourceSyncJobs` operation to see the status of the sync job\. If the `Status` returned for the sync job is `SYNCING_INDEXING`, some documents are still being indexed\. You can start a new sync job when the status of the previous job is `FAILED`, `SUCCEEDED`, or `SYNCING_INDEX`\.

After you call the `StopDataSourceSyncJob` operation, you can't use a sync job identifier in a call to the `BatchPutDocument` or `BatchDeleteDocument` operations\. If you do, all of the documents submitted are returned in the `FailedDocuments` response message from the operation\.

## Required attributes<a name="custom-required-attributes"></a>

When you submit a document to Amazon Kendra using the `BatchPutDocument` operation, each document requires two attributes to identify the data source and synchronization run that it belongs to\. You must provide the following two attributes:
+ `_data_source_id` – The identifier of the data source\. This is returned when you create the data source with the console or the `CreateDataSource` operation\.
+ `_data_source_sync_job_execution_id` – The identifier of the sync run\. This is returned when you start the index synchronization with the `StartDataSourceSyncJob` operation\.

The following is the JSON required to index a document using a custom data source\.

```
{
    "Documents": [
        {
            "Attributes": [
                {
                    "Key": "_data_source_id",
                    "Value": {
                        "StringValue": "data source identifier"
                    }
                },
                {
                    "Key": "_data_source_sync_job_execution_id",
                    "Value": {
                        "StringValue": "sync job identifier"
                    }
                }
            ],
            "Blob": "document content",
            "ContentType": "content type",
            "Id": "document identifier",
            "Title": "document title"
        }
    ],
    "IndexId": "index identifier",
    "RoleArn": "IAM role ARN"
}
```

When you remove a document from the index using the `BatchDeleteDocument` operation, you need to specify the following two fields in the `DataSourceSyncJobMetricTarget` parameter:
+ `DataSourceId` – The identifier of the data source\. This is returned when you create the data source with the console or the `CreateDataSource` operation\.
+ `DataSourceSyncJobId` – The identifier of the sync run\. This is returned when you start the index synchronization with the `StartDataSourceSyncJob` operation\.

The following is the JSON required to delete a document from the index using the `BatchDeleteDocument` operation\.

```
{
    "DataSourceSyncJobMetricTarget": {
        "DataSourceId": "data source identifier",
        "DataSourceSyncJobId": "sync job identifier"
    },
    "DocumentIdList": [
        "document identifier"
    ],
    "IndexId": "index identifier"
}
```

## Viewing metrics<a name="custom-metrics"></a>

After a sync job is finished, you can use the [ ListDataSourceSyncJobs ](API_ListDataSourceSyncJobs.md) operation to get the metrics associated with the sync job\. Use this to monitor your custom data source syncs\.

If you submit the same document multiple times, either as part of the `BatchPutDocument` operation, the `BatchDeleteDocument` operation, or if the document is submitted for both addition and deletion, the document is only counted once in the metrics\.
+ `DocumentsAdded` – The number of documents submitted with a `BatchPutDocument` operation associated with this sync job added to the index for the first time\. If a document is submitted for addition more than once in a sync, the document is only counted once in the metrics\.
+ `DocumentsDeleted` – The number of documents submitted with a `BatchDeleteDocument` operation associated with this sync job deleted from the index\. If a document is submitted for deletion more than once in a sync, the document is only counted once in the metrics\.
+ `DocumentsFailed` – The number of documents associated with this sync job that failed indexing\. These are documents that were accepted by Amazon Kendra for indexing but could not be indexed or deleted\. If a document is not accepted by Amazon Kendra, the identifier for the document is returned in the `FailedDocuments` response property of the `BatchPutDocument` and `BatchDeleteDocument` operations 
+ `DocumentsModified` – The number of modified documents submitted withe a `BatchPutDocument` operation associated with this sync job that were modified in the Amazon Kendra index\.

Amazon Kendra also emits Amazon CloudWatch metrics while indexing documents\. For more information, see [Metrics for indexed documents](cloudwatch-metrics.md#cloudwatch-metrics-id)\.

Amazon Kendra doesn't return the `DocumentsScanned` metric for custom data sources\. It also emit the CloudWatch metrics listed in [Metrics for Amazon Kendra data sources](cloudwatch-metrics.md#cloudwatch-metrics-data-source)\.