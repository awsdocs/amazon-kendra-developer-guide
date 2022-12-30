--------

--------

# Enriching your documents during ingestion<a name="custom-document-enrichment"></a>

You can alter your content and document metadata fields or attributes during the document ingestion process\. With Amazon Kendra's *Custom Document Enrichment* feature, you can create, modify, or delete document attributes and content when you ingest your documents into Amazon Kendra\. This means you can manipulate and ingest your data as you need\.

This feature gives you control over how your documents are treated and ingested into Amazon Kendra\. For example, you can scrub personally identifiable information in the document metadata while ingesting your documents into Amazon Kendra\.

Another way that you can use this feature is to invoke a Lambda function in AWS Lambda to run Optical Character Recognition \(OCR\) on images, translation on text, and other tasks for preparing the data for search or analysis\. For example, you can invoke a function to run OCR on images\. The function could interpret text from images and treat each image as a textual document\. A company that receives mailed\-in customer surveys and stores these surveys as images could ingest these images as textual documents into Amazon Kendra\. The company can then search for valuable customer survey information in Amazon Kendra\.

You can use basic operations to apply as a first parse of your data, and then use a Lambda function to apply more complex operations on your data\. For example, you could use a basic operation to simply remove all values in the document metadata field 'Customer\_ID', and then apply a Lambda function to extract text from images of the text in the documents\.

## How Custom Document Enrichment works<a name="how-custom-document-enrichment-works"></a>

The overall process of Custom Document Enrichment is as follows:

1. You configure Custom Document Enrichment when you create or update your data source, or index your documents directly into Amazon Kendra\.

1. Amazon Kendra applies inline configurations or basic logic to alter your data\. For more information, see [Basic operations to change metadata](#basic-data-maniplation)\.

1. If you choose to configure advanced data manipulation, Amazon Kendra can apply this on your original, raw documents or on the structured, parsed documents\. For more information, see [Lambda functions: extract and change metadata or content](#advanced-data-manipulation)\.

1. Your altered documents are ingested into Amazon Kendra\.

At any point in this process, if your configuration is not valid, Amazon Kendra throws an error\.

When you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html), [UpdateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_UpdateDataSource.html), or [BatchPutDocument](https://docs.aws.amazon.com/kendra/latest/dg/API_BatchPutDocument.html) APIs, you provide your Custom Document Enrichment configuration\. If you call `BatchPutDocument`, you must configure Custom Document Enrichment with each request\. If you use the console, you select your index and then select **Document enrichments** to configure Custom Document Enrichment\.

If you use **Document enrichments** in the console, you can choose to only configure basic operations or only Lambda functions or both, like you can using the API\. You can select **Next** in the console steps to choose not to configure basic operations and only Lambda functions, including whether to apply to the original \(pre\-extraction\) or structured \(post\-extraction\) data\. You can only save your configurations by completing all the steps in the console\. Your document configurations are not saved if you don't complete all the steps\.

## Basic operations to change metadata<a name="basic-data-maniplation"></a>

You can manipulate your document fields and content using basic logic\. This includes removing values in a field, modifying values in a field using a condition, or creating a field\. For advanced manipulations that go beyond what you can manipulate using basic logic, invoke a Lambda function\. For more information, see [Lambda functions: extract and change metadata or content](#advanced-data-manipulation)\.

To apply basic logic, you specify the target field you want to manipulate using the [DocumentAttributeTarget](https://docs.aws.amazon.com/kendra/latest/dg/API_DocumentAttributeTarget.html) object\. You provide the attribute key\. For example, the key 'Department' is a field or attribute that holds all the department names associated with the documents\. You can also specify a value to use in the target field if a certain condition is met\. You set the condition using the [DocumentAttributeCondition](https://docs.aws.amazon.com/kendra/latest/dg/API_DocumentAttributeCondition.html) object\. For example, if the 'Source\_URI' field contains 'financial' in its URI value, then prefill the target field 'Department' with the target value 'Finance' for the document\. You can also delete the values of the target document attribute\.

To apply basic logic using the console, select your index and then select **Document enrichments** in the navigation menu\. Go to **Configure basic operations** to apply basic manipulations to your document fields and content\.

The following is an example of using basic logic to remove all customer identification numbers in the document field called 'Customer\_ID'\.

Data before basic manipulation applied\.


| **Document\_ID** | **Body\_Text** | **Customer\_ID** | 
| --- | --- | --- | 
| 1 | Lorem Ipsum\. | CID1234 | 
| 2 | Lorem Ipsum\. | CID1235 | 
| 3 | Lorem Ipsum\. | CID1236 | 

Data after basic manipulation applied\.


| **Document\_ID** | **Body\_Text** | **Customer\_ID** | 
| --- | --- | --- | 
| 1 | Lorem Ipsum\. |   | 
| 2 | Lorem Ipsum\. |   | 
| 3 | Lorem Ipsum\. |   | 

The following is an example of using basic logic to create a field called 'Department' and prefill this field with the department names based on information from the 'Source\_URI' field\. This uses the condition that if the 'Source\_URI' field contains 'financial' in its URI value, then prefill the target field 'Department' with the target value 'Finance' for the document\.

Data before basic manipulation applied\.


| **Document\_ID** | **Body\_Text** | **Source\_URI** | 
| --- | --- | --- | 
| 1 | Lorem Ipsum\. | financial/1 | 
| 2 | Lorem Ipsum\. | financial/2 | 
| 3 | Lorem Ipsum\. | financial/3 | 

Data after basic manipulation applied\.


| **Document\_ID** | **Body\_Text** | **Source\_URI** | **Department** | 
| --- | --- | --- | --- | 
| 1 | Lorem Ipsum\. | financial/1 | Finance | 
| 2 | Lorem Ipsum\. | financial/2 | Finance | 
| 3 | Lorem Ipsum\. | financial/3 | Finance | 

**Note**  
Amazon Kendra can't create a target document field if it isn't already created as an index field\. After you create your index field, you can create a document field using `DocumentAttributeTarget`\. Amazon Kendra then maps your newly created document metadata field to your index field\.

The following code is an example of configuring basic data manipulation to remove customer identification numbers associated with the documents\.

------
#### [ Console ]

**To configure basic data manipulation to remove customer identification numbers**

1. In the left navigation pane, under **Indexes**, select **Document enrichments** and then select **Add document enrichment**\.

1. On the **Configure basic operations** page, choose from the dropdown your data source that you want to alter document fields and content\. Then choose from the dropdown the document field name 'Customer\_ID', select from the dropdown the index field name 'Customer\_ID', and select from the dropdown the target action **Delete**\. Then select **Add basic operation**\.

------
#### [ CLI ]

**To configure basic data manipulation to remove customer identification numbers**

```
aws kendra create-data-source \
 --name data-source-name \
 --index-id index-id \
 --role-arn arn:aws:iam::account-id:role/role-name \
 --type S3 \
 --configuration '{"S3Configuration":{"BucketName":"S3-bucket-name"}}' \
 --custom-document-enrichment-configuration '{"InlineConfigurations":[{"Target":{"TargetDocumentAttributeKey":"Customer_ID", "TargetDocumentAttributeValueDeletion": true}}]}'
```

------
#### [ Python ]

**To configure basic data manipulation to remove customer identification numbers**

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Create a data source with customizations")

# Provide the name of the data source
name = "data-source-name"
# Provide the index ID for the data source
index_id = "index-id"
# Provide the IAM role ARN required for data sources
role_arn = "arn:aws:iam::${account-id}:role/${role-name}"
# Provide the data source connection information
data_source_type = "S3"
S3_bucket_name = "S3-bucket-name"
# Configure the data source with Custom Document Enrichment
configuration = {"S3Configuration":
        {
            "BucketName": S3_bucket_name
        }
    }
custom_document_enrichment_configuration = {"InlineConfigurations":[
        {
            "Target":{"TargetDocumentAttributeKey":"Customer_ID",
                       "TargetDocumentAttributeValueDeletion": True}
        }]
    }

try:
    data_source_response = kendra.create_data_source(
        Name = name,
        IndexId = index_id,
        RoleArn = role_arn,
        Type = data_source_type
        Configuration = configuration
        CustomDocumentEnrichmentConfiguration = custom_document_enrichment_configuration
    )

    pprint.pprint(data_source_response)

    data_source_id = data_source_response["Id"]

    print("Wait for Amazon Kendra to create the data source with your customizations.")

    while True:
        # Get the details of the data source, such as the status
        data_source_description = kendra.describe_data_source(
            Id = data_source_id,
            IndexId = index_id
        )
        status = data_source_description["Status"]
        print(" Creating data source. Status: "+status)
        time.sleep(60)
        if status != "CREATING":
            break

    print("Synchronize the data source.")

    sync_response = kendra.start_data_source_sync_job(
        Id = data_source_id,
        IndexId = index_id
    )

    pprint.pprint(sync_response)

    print("Wait for the data source to sync with the index.")

    while True:

        jobs = kendra.list_data_source_sync_jobs(
            Id= data_source_id,
            IndexId= index_id
        )

        # For this example, there should be one job
        status = jobs["History"][0]["Status"]

        print(" Syncing data source. Status: "+status)
        time.sleep(60)
        if status != "SYNCING":
            break

except  ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

**To configure basic data manipulation to remove customer identification numbers**

```
package com.amazonaws.kendra;

import java.util.concurrent.TimeUnit;
import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.CreateDataSourceRequest;
import software.amazon.awssdk.services.kendra.model.CreateDataSourceResponse;
import software.amazon.awssdk.services.kendra.model.CreateIndexRequest;
import software.amazon.awssdk.services.kendra.model.CreateIndexResponse;
import software.amazon.awssdk.services.kendra.model.DataSourceConfiguration;
import software.amazon.awssdk.services.kendra.model.DataSourceStatus;
import software.amazon.awssdk.services.kendra.model.DataSourceSyncJob;
import software.amazon.awssdk.services.kendra.model.DataSourceSyncJobStatus;
import software.amazon.awssdk.services.kendra.model.DataSourceType;
import software.amazon.awssdk.services.kendra.model.DescribeDataSourceRequest;
import software.amazon.awssdk.services.kendra.model.DescribeDataSourceResponse;
import software.amazon.awssdk.services.kendra.model.DescribeIndexRequest;
import software.amazon.awssdk.services.kendra.model.DescribeIndexResponse;
import software.amazon.awssdk.services.kendra.model.IndexStatus;
import software.amazon.awssdk.services.kendra.model.ListDataSourceSyncJobsRequest;
import software.amazon.awssdk.services.kendra.model.ListDataSourceSyncJobsResponse;
import software.amazon.awssdk.services.kendra.model.S3DataSourceConfiguration;
import software.amazon.awssdk.services.kendra.model.StartDataSourceSyncJobRequest;
import software.amazon.awssdk.services.kendra.model.StartDataSourceSyncJobResponse;

public class CreateDataSourceWithCustomizationsExample {

    public static void main(String[] args) throws InterruptedException {
        System.out.println("Create a data source with customizations");
        
        String dataSourceName = "data-source-name";
        String indexId = "index-id";
        String dataSourceRoleArn = "arn:aws:iam::account-id:role/role-name";
        String s3BucketName = "S3-bucket-name"

        KendraClient kendra = KendraClient.builder().build();
        
        CreateDataSourceRequest createDataSourceRequest = CreateDataSourceRequest
            .builder()
            .name(dataSourceName)
            .description(experienceDescription)
            .roleArn(experienceRoleArn)
            .type(DataSourceType.S3)
            .configuration(
                DataSourceConfiguration
                    .builder()
                    .s3Configuration(
                        S3DataSourceConfiguration
                            .builder()
                            .bucketName(s3BucketName)
                            .build()
                    ).build()
            )
            .customDocumentEnrichmentConfiguration(
                CustomDocumentEnrichmentConfiguration
                    .builder()
                    .inlineConfigurations(Arrays.asList(
                        InlineCustomDocumentEnrichmentConfiguration
                            .builder()
                            .target(
                                DocumentAttributeTarget
                                    .builder()
                                    .targetDocumentAttributeKey("Customer_ID")
                                    .targetDocumentAttributeValueDeletion(true)
                                    .build())
                            .build()
                    )).build();
        
        CreateDataSourceResponse createDataSourceResponse = kendra.createDataSource(createDataSourceRequest);
        System.out.println(String.format("Response of creating data source: %s", createDataSourceResponse));

        String dataSourceId = createDataSourceResponse.id();
        System.out.println(String.format("Waiting for Kendra to create the data source %s", dataSourceId));
        DescribeDataSourceRequest describeDataSourceRequest = DescribeDataSourceRequest
            .builder()
            .indexId(indexId)
            .id(dataSourceId)
            .build();

        while (true) {
            DescribeDataSourceResponse describeDataSourceResponse = kendra.describeDataSource(describeDataSourceRequest);

            DataSourceStatus status = describeDataSourceResponse.status();
            System.out.println(String.format("Creating data source. Status: %s", status));
            TimeUnit.SECONDS.sleep(60);
            if (status != DataSourceStatus.CREATING) {
                break;
            }
        }

        System.out.println(String.format("Synchronize the data source %s", dataSourceId));
        StartDataSourceSyncJobRequest startDataSourceSyncJobRequest = StartDataSourceSyncJobRequest
            .builder()
            .indexId(indexId)
            .id(dataSourceId)
            .build();
        StartDataSourceSyncJobResponse startDataSourceSyncJobResponse = kendra.startDataSourceSyncJob(startDataSourceSyncJobRequest);
        System.out.println(String.format("Waiting for the data source to sync with the index %s for execution ID %s", indexId, startDataSourceSyncJobResponse.executionId()));

        // For this example, there should be one job
        ListDataSourceSyncJobsRequest listDataSourceSyncJobsRequest = ListDataSourceSyncJobsRequest
            .builder()
            .indexId(indexId)
            .id(dataSourceId)
            .build();

        while (true) {
            ListDataSourceSyncJobsResponse listDataSourceSyncJobsResponse = kendra.listDataSourceSyncJobs(listDataSourceSyncJobsRequest);
            DataSourceSyncJob job = listDataSourceSyncJobsResponse.history().get(0);
            System.out.println(String.format("Syncing data source. Status: %s", job.status()));

            TimeUnit.SECONDS.sleep(60);
            if (job.status() != DataSourceSyncJobStatus.SYNCING) {
                break;
            }

        }

        System.out.println("Data source creation with customizations is complete");
    }
}
```

------

## Lambda functions: extract and change metadata or content<a name="advanced-data-manipulation"></a>

You can manipulate your document fields and content using Lambda functions\. This is useful if you want to go beyond basic logic and apply advanced data manipulations\. For example, using Optical Character Recognition \(OCR\), which interprets text from images, and treats each image as a textual document\. Or, retrieving the current date\-time in a certain time zone and inserting the date\-time where there's an empty value for a date field\.

You can apply basic logic first and then use a Lambda function to further manipulate your data, or vice versa\. You can also choose to only apply a Lambda function\.

Amazon Kendra can invoke a Lambda function to apply advanced data manipulations during the ingestion process as part of your [CustomDocumentEnrichmentConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CustomDocumentEnrichmentConfiguration.html)\. You specify a role that includes permission to execute the Lambda function and access your Amazon S3 bucket to store the output of your data manipulations—see [IAM access roles](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html)\.

Amazon Kendra can apply a Lambda function on your original, raw documents or on the structured, parsed documents\. You can configure a Lambda function that takes your original or raw data and applies your data manipulations using [PreExtractionHookConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CustomDocumentEnrichmentConfiguration.html)\. You can also configure a Lambda function that takes your structured documents and applies your data manipulations using [PostExtractionHookConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_CustomDocumentEnrichmentConfiguration.html)\. Amazon Kendra extracts the document metadata and text to structure your documents\. Your Lambda functions must follow the mandatory request and response structures\. For more information, see [Data contracts for Lambda functions](#cde-data-contracts-lambda)\.

To configure a Lambda function in the console, select your index and then select **Document enrichments** in the navigation menu\. Go to **Configure Lambda functions** to configure a Lambda function\.

You can configure only one Lambda function for `PreExtractionHookConfiguration` and and only one Lambda function for `PostExtractionHookConfiguration`\. However, your Lambda function can invoke other functions that it requires\. You can configure both `PreExtractionHookConfiguration` and `PostExtractionHookConfiguration` or either one\. Your Lambda function for `PreExtractionHookConfiguration` must not exceed a run time of 5 minutes and your Lambda function for `PostExtractionHookConfiguration` must not exceed a run time of 1 minute\. Configuring Custom Document Enrichment naturally takes longer to ingest your documents into Amazon Kendra than if you were to not configure this\.

You can configure Amazon Kendra to invoke a Lambda function only if a condition is met\. For example, you can specify a condition that if there are empty date\-time values, then Amazon Kendra should invoke a function that inserts the current date\-time\.

The following is an example of using a Lambda function to run OCR to interpret text from images and store this text in a field called 'Document\_Image\_Text'\.

Data before advanced manipulation applied\.


| **Document\_ID** | **Document\_Image** | 
| --- | --- | 
| 1 | image\_1\.png | 
| 2 | image\_2\.png | 
| 3 | image\_3\.png | 

Data after advanced manipulation applied\.


| **Document\_ID** | **Document\_Image** | **Document\_Image\_Text** | 
| --- | --- | --- | 
| 1 | image\_1\.png | Mailed survey response | 
| 2 | image\_2\.png | Mailed survey response | 
| 3 | image\_3\.png | Mailed survey response | 

The following is an example of using a Lambda function to insert the current date\-time for empty date values\. This uses the condition that if a date field value is 'null', then replace this with the current date\-time\.

Data before advanced manipulation applied\.


| **Document\_ID** | **Body\_Text** | **Last\_Updated** | 
| --- | --- | --- | 
| 1 | Lorem Ipsum\. | January 1, 2020 | 
| 2 | Lorem Ipsum\. |   | 
| 3 | Lorem Ipsum\. | July 1, 2020 | 

Data after advanced manipulation applied\.


| **Document\_ID** | **Body\_Text** | **Last\_Updated** | 
| --- | --- | --- | 
| 1 | Lorem Ipsum\. | January 1, 2020 | 
| 2 | Lorem Ipsum\. | December 1, 2021 | 
| 3 | Lorem Ipsum\. | July 1, 2020 | 

The following code is an example of configuring a Lambda function for advanced data manipulation on the raw, original data\.

------
#### [ Console ]

**To configure a Lambda function for advanced data manipulation on the raw, original data**

1. In the left navigation pane, under **Indexes**, select **Document enrichments** and then select **Add document enrichment**\.

1. On the **Configure Lambda functions** page, in the **Lambda for pre\-extraction** section, select from the dropdowns your Lambda function ARN and your Amazon S3 bucket\. Add your IAM access role by selecting the option to create a new role from the dropdown\. This creates the required Amazon Kendra permissions to create the document enrichment\.

------
#### [ CLI ]

**To configure a Lambda function for advanced data manipulation on the raw, original data**

```
aws kendra create-data-source \
 --name data-source-name \
 --index-id index-id \
 --role-arn arn:aws:iam::account-id:role/role-name \
 --type S3 \
 --configuration '{"S3Configuration":{"BucketName":"S3-bucket-name"}}' \
 --custom-document-enrichment-configuration '{"PreExtractionHookConfiguration":{"LambdaArn":"arn:aws:iam::account-id:function/function-name", "S3Bucket":"S3-bucket-name"}, "RoleArn": "arn:aws:iam:account-id:role/cde-role-name"}'
```

------
#### [ Python ]

**To configure a Lambda function for advanced data manipulation on the raw, original data**

```
import boto3
from botocore.exceptions import ClientError
import pprint
import time

kendra = boto3.client("kendra")

print("Create a data source with customizations.")

# Provide the name of the data source
name = "data-source-name"
# Provide the index ID for the data source
index_id = "index-id"
# Provide the IAM role ARN required for data sources
role_arn = "arn:aws:iam::${account-id}:role/${role-name}"
# Provide the data source connection information
data_source_type = "S3"
S3_bucket_name = "S3-bucket-name"
# Configure the data source with Custom Document Enrichment
configuration = {"S3Configuration":
        {
            "BucketName": S3_bucket_name
        }
    }
custom_document_enrichment_configuration = {"PreExtractionHookConfiguration":
        {
            "LambdaArn":"arn:aws:iam::account-id:function/function-name",
            "S3Bucket":"S3-bucket-name"
        }
    "RoleArn":"arn:aws:iam::account-id:role/cde-role-name"
    }

try:
    data_source_response = kendra.create_data_source(
        Name = name,
        IndexId = index_id,
        RoleArn = role_arn,
        Type = data_source_type
        Configuration = configuration
        CustomDocumentEnrichmentConfiguration = custom_document_enrichment_configuration
    )

    pprint.pprint(data_source_response)

    data_source_id = data_source_response["Id"]

    print("Wait for Amazon Kendra to create the data source with your customizations.")

    while True:
        # Get the details of the data source, such as the status
        data_source_description = kendra.describe_data_source(
            Id = data_source_id,
            IndexId = index_id
        )
        status = data_source_description["Status"]
        print(" Creating data source. Status: "+status)
        time.sleep(60)
        if status != "CREATING":
            break

    print("Synchronize the data source.")

    sync_response = kendra.start_data_source_sync_job(
        Id = data_source_id,
        IndexId = index_id
    )

    pprint.pprint(sync_response)

    print("Wait for the data source to sync with the index.")

    while True:

        jobs = kendra.list_data_source_sync_jobs(
            Id = data_source_id,
            IndexId = index_id
        )

        # For this example, there should be one job
        status = jobs["History"][0]["Status"]

        print(" Syncing data source. Status: "+status)
        time.sleep(60)
        if status != "SYNCING":
            break

except  ClientError as e:
        print("%s" % e)

print("Program ends.")
```

------
#### [ Java ]

**To configure a Lambda function for advanced data manipulation on the raw, original data**

```
package com.amazonaws.kendra;

import java.util.concurrent.TimeUnit;
import software.amazon.awssdk.services.kendra.KendraClient;
import software.amazon.awssdk.services.kendra.model.CreateDataSourceRequest;
import software.amazon.awssdk.services.kendra.model.CreateDataSourceResponse;
import software.amazon.awssdk.services.kendra.model.CreateIndexRequest;
import software.amazon.awssdk.services.kendra.model.CreateIndexResponse;
import software.amazon.awssdk.services.kendra.model.DataSourceConfiguration;
import software.amazon.awssdk.services.kendra.model.DataSourceStatus;
import software.amazon.awssdk.services.kendra.model.DataSourceSyncJob;
import software.amazon.awssdk.services.kendra.model.DataSourceSyncJobStatus;
import software.amazon.awssdk.services.kendra.model.DataSourceType;
import software.amazon.awssdk.services.kendra.model.DescribeDataSourceRequest;
import software.amazon.awssdk.services.kendra.model.DescribeDataSourceResponse;
import software.amazon.awssdk.services.kendra.model.DescribeIndexRequest;
import software.amazon.awssdk.services.kendra.model.DescribeIndexResponse;
import software.amazon.awssdk.services.kendra.model.IndexStatus;
import software.amazon.awssdk.services.kendra.model.ListDataSourceSyncJobsRequest;
import software.amazon.awssdk.services.kendra.model.ListDataSourceSyncJobsResponse;
import software.amazon.awssdk.services.kendra.model.S3DataSourceConfiguration;
import software.amazon.awssdk.services.kendra.model.StartDataSourceSyncJobRequest;
import software.amazon.awssdk.services.kendra.model.StartDataSourceSyncJobResponse;


public class CreateDataSourceWithCustomizationsExample {

    public static void main(String[] args) throws InterruptedException {
        System.out.println("Create a data source with customizations");
        
        String dataSourceName = "data-source-name";
        String indexId = "index-id";
        String dataSourceRoleArn = "arn:aws:iam::account-id:role/role-name";
        String s3BucketName = "S3-bucket-name"

        KendraClient kendra = KendraClient.builder().build();
        
        CreateDataSourceRequest createDataSourceRequest = CreateDataSourceRequest
            .builder()
            .name(dataSourceName)
            .description(experienceDescription)
            .roleArn(experienceRoleArn)
            .type(DataSourceType.S3)
            .configuration(
                DataSourceConfiguration
                    .builder()
                    .s3Configuration(
                        S3DataSourceConfiguration
                            .builder()
                            .bucketName(s3BucketName)
                            .build()
                    ).build()
            )
            .customDocumentEnrichmentConfiguration(
                CustomDocumentEnrichmentConfiguration
                    .builder()
                    .preExtractionHookConfiguration(
                        HookConfiguration
                            .builder()
                            .lambdaArn("arn:aws:iam::account-id:function/function-name")
                            .s3Bucket("S3-bucket-name")
                            .build())
                    .roleArn("arn:aws:iam::account-id:role/cde-role-name")
                    .build();
        
        CreateDataSourceResponse createDataSourceResponse = kendra.createDataSource(createDataSourceRequest);
        System.out.println(String.format("Response of creating data source: %s", createDataSourceResponse));

        String dataSourceId = createDataSourceResponse.id();
        System.out.println(String.format("Waiting for Kendra to create the data source %s", dataSourceId));
        DescribeDataSourceRequest describeDataSourceRequest = DescribeDataSourceRequest
            .builder()
            .indexId(indexId)
            .id(dataSourceId)
            .build();

        while (true) {
            DescribeDataSourceResponse describeDataSourceResponse = kendra.describeDataSource(describeDataSourceRequest);

            DataSourceStatus status = describeDataSourceResponse.status();
            System.out.println(String.format("Creating data source. Status: %s", status));
            TimeUnit.SECONDS.sleep(60);
            if (status != DataSourceStatus.CREATING) {
                break;
            }
        }

        System.out.println(String.format("Synchronize the data source %s", dataSourceId));
        StartDataSourceSyncJobRequest startDataSourceSyncJobRequest = StartDataSourceSyncJobRequest
            .builder()
            .indexId(indexId)
            .id(dataSourceId)
            .build();
        StartDataSourceSyncJobResponse startDataSourceSyncJobResponse = kendra.startDataSourceSyncJob(startDataSourceSyncJobRequest);
        System.out.println(String.format("Waiting for the data source to sync with the index %s for execution ID %s", indexId, startDataSourceSyncJobResponse.executionId()));

        // For this example, there should be one job
        ListDataSourceSyncJobsRequest listDataSourceSyncJobsRequest = ListDataSourceSyncJobsRequest
            .builder()
            .indexId(indexId)
            .id(dataSourceId)
            .build();

        while (true) {
            ListDataSourceSyncJobsResponse listDataSourceSyncJobsResponse = kendra.listDataSourceSyncJobs(listDataSourceSyncJobsRequest);
            DataSourceSyncJob job = listDataSourceSyncJobsResponse.history().get(0);
            System.out.println(String.format("Syncing data source. Status: %s", job.status()));

            TimeUnit.SECONDS.sleep(60);
            if (job.status() != DataSourceSyncJobStatus.SYNCING) {
                break;
            }

        }

        System.out.println("Data source creation with customizations is complete");
    }
}
```

------

## Data contracts for Lambda functions<a name="cde-data-contracts-lambda"></a>

Your Lambda functions for advanced data manipulation interact with Amazon Kendra data contracts\. The contracts are the mandatory request and response structures of your Lambda functions\. If your Lambda functions don't follow these structures, then Amazon Kendra throws an error\.

Your Lambda function for `PreExtractionHookConfiguration` should expect the following request structure:

```
{
    "version": <str>,
    "dataBlobStringEncodedInBase64": <str>, //In the case of a data blob
    "s3Bucket": <str>, //In the case of an S3 bucket
    "s3ObjectKey": <str>, //In the case of an S3 bucket
    "metadata": <Metadata>
}
```

The `metadata` structure, which includes the `CustomerDocumentAttribute` structure, is as follows:

```
{
    "attributes": [<CustomerDocumentAttribute<]
}

CustomerDocumentAttribute
{
    "name": <str>,
    "value": <CustomerDocumentAttributeValue>
}

CustomerDocumentAttributeValue
{
    "stringValue": <str>,
    "integerValue": <int>,
    "longValue": <long>,
    "stringListValue": list<str>,
    "dateValue": <str>
}
```

Your Lambda function for `PreExtractionHookConfiguration` must adhere to the following response structure:

```
{
    "version": <str>,
    "dataBlobStringEncodedInBase64": <str>, //In the case of a data blob
    "s3ObjectKey": <str>, //In the case of an S3 bucket
    "metadataUpdates": [<CustomDocumentAttribute>]
}
```

Your Lambda function for `PostExtractionHookConfiguration` should expect the following request structure:

```
{
    "version": <str>,
    "s3Bucket": <str>,
    "s3ObjectKey": <str>,
    "metadata": <Metadata>
}
```

Your Lambda function for `PostExtractionHookConfiguration` must adhere to the following response structure:

```
PostExtractionHookConfiguration Lambda Response
{
    "version": <str>,
    "s3ObjectKey": <str>,
    "metadataUpdates": [<CustomDocumentAttribute>]
}
```

Your altered document is uploaded to your Amazon S3 bucket\. The altered document must follow the format shown in [Structured document format](#structured-document-format)\.

### Structured document format<a name="structured-document-format"></a>

Amazon Kendra uploads your structured document to the given Amazon S3 bucket\. The structured document follows this format:

```
Kendra document

{
   "textContent": <TextContent>
}

TextContent
{
  "documentBodyText": <str>
}
```

### Example of a Lambda function that adheres to data contracts<a name="example-lambda-function-advanced-manipulation"></a>

The following Python code is an example of a Lambda function that applies advanced manipulation of the metadata fields `_authors`, `_document_title`, and the body content on the raw or original documents\.

**In the case of the body content residing in an Amazon S3 bucket**

```
import json
import boto3
     
s3 = boto3.client("s3")

# Lambda function for advanced data manipulation    
def lambda_handler(event, context):
    # Get the value of "S3Bucket" key name or item from the given event input
    s3_bucket = event.get("s3Bucket")
    # Get the value of "S3ObjectKey" key name or item from the given event input
    s3_object_key = event.get("s3ObjectKey")
    
    content_object_before_CDE = s3.get_object(Bucket = s3_bucket, Key = s3_object_key)
    content_before_CDE = content_object_before_CDE["Body"].read().decode("utf-8");
    content_after_CDE = "CDEInvolved " + content_before_CDE
    
    # Get the value of "metadata" key name or item from the given event input
    metadata = event.get("metadata")
    # Get the document "attributes" from the metadata 
    document_attributes = metadata.get("attributes")
    
    s3.put_object(Bucket = s3_bucket, Key = "dummy_updated_kendra_document", Body=json.dumps(content_after_CDE))
    return {
        "version": "v0",
        "s3ObjectKey": "dummy_updated_kendra_document",
        "metadataUpdates": [
            {"name":"_document_title", "value":{"stringValue":"title_from_pre_extraction_lambda"}},
            {"name":"_authors", "value":{"stringListValue":["author1", "author2"]}}
        ]
    }
```

**In the case of the body content residing in a data blob**

```
import json
import boto3
import base64

# Lambda function for advanced data manipulation
def lambda_handler(event, context):
    
    # Get the value of "dataBlobStringEncodedInBase64" key name or item from the given event input 
    data_blob_string_encoded_in_base64 = event.get("dataBlobStringEncodedInBase64")
    # Decode the data blob string in UTF-8
    data_blob_string = base64.b64decode(data_blob_string_encoded_in_base64).decode("utf-8")
    # Get the value of "metadata" key name or item from the given event input    
    metadata = event.get("metadata")
    # Get the document "attributes" from the metadata
    document_attributes = metadata.get("attributes")
    
    new_data_blob = "This should be the modified data in the document by pre processing lambda ".encode("utf-8")
    return {
        "version": "v0",
        "dataBlobStringEncodedInBase64": base64.b64encode(new_data_blob).decode("utf-8"),
        "metadataUpdates": [
            {"name":"_document_title", "value":{"stringValue":"title_from_pre_extraction_lambda"}},
            {"name":"_authors", "value":{"stringListValue":["author1", "author2"]}}
        ]
    }
```

The following Python code is an example of a Lambda function that applies advanced manipulation of the metadata fields `_authors`, `_document_title`, and the body content on the structured or parsed documents\.

```
import json
import boto3
import time

s3 = boto3.client("s3")

# Lambda function for advanced data manipulation
def lambda_handler(event, context):
    
    # Get the value of "S3Bucket" key name or item from the given event input
    s3_bucket = event.get("s3Bucket")
    # Get the value of "S3ObjectKey" key name or item from the given event input
    s3_key = event.get("s3ObjectKey")
    # Get the value of "metadata" key name or item from the given event input
    metadata = event.get("metadata")
    # Get the document "attributes" from the metadata 
    document_attributes = metadata.get("attributes")
    
    kendra_document_object = s3.get_object(Bucket = s3_bucket, Key = s3_key)
    kendra_document_string = kendra_document_object['Body'].read().decode('utf-8')
    kendra_document = json.loads(kendra_document_string)
    kendra_document["textContent"]["documentBodyText"] = "Changing document body to a short sentence."
    
    s3.put_object(Bucket = s3_bucket, Key = "dummy_updated_kendra_document", Body=json.dumps(kendra_document))

    return {
        "version" : "v0",
        "s3ObjectKey": "dummy_updated_kendra_document",
        "metadataUpdates": [
            {"name": "_document_title", "value":{"stringValue": "title_from_post_extraction_lambda"}},
            {"name": "_authors", "value":{"stringListValue":["author1", "author2"]}}
        ]
    }
```