--------

--------

# Troubleshooting data sources<a name="troubleshooting-data-sources"></a>

This section can help you fix issues with Amazon Kendra data sources\.

## My documents were not indexed<a name="troubleshooting-data-sources-not-indexed"></a>

When you synchronize your Kendra index with a data source, you may run into issues that prevent the documents from being indexed\. Indexing is a two\-step process\. First, the data source is checked for new and updated documents to index, and to find documents to remove from the index\. Second, at the document level, each document is accessed and indexed\. 

An error can occur in either of these steps\. Data source level errors are reported in the console in the **Sync run history** section of the data source details page\. The status of the synchronization job can be **Succeeded**, **Incomplete**, or **Failed**\. You can also see the number of documents indexed and deleted during the job\. If the status is **Failed**, a message is shown in the **Details** column\.

Document level errors are reported in Amazon CloudWatch Logs\. You can see the errors using the CloudWatch console\.

## My synchronization job failed<a name="troubleshooting-data-sources-failed"></a>

A synchronization job typically fails when there is a configuration error in the index or the data source\. The error message in the Details column of the data source gives information about what went wrong\. The problem is usually that the index or the data source does not have the proper IAM permissions\. The error message describes the missing permissions \. Here are some of the error messages that you can receive:

`Failed to create log group for job. Please make sure that the IAM role provided has sufficient permissions.`

If your index role does not have permission to use CloudWatch, the data source will not be able to create a CloudWatch log\. If you get this error, you must add CloudWatch permissions to the index role\.

`Failed to access S3 file prefix (bucket name) while trying to crawl your metadata files. Please make sure the IAM Role (role ARN) provided has sufficient permissions. `

When you are using an Amazon S3 data source, Kendra must have permission to access the bucket that contains the documents\. You need to add permission for Kendra to read the bucket to the data source IAM role\.

`The provided IAM Role (role ARN) could not be assumed. Please make sure Amazon Kendra is a trusted entity that is allowed to assume the role.`

Kendra needs permission to assume the index and data source IAM roles\. You need to add a trust policy to the roles with permission for the `sts:AssumeRole` action\.

For the IAM policies that Kendra needs to index a data source, see [IAM access roles for Amazon Kendra](iam-roles.md)\.

## My synchronization job is incomplete<a name="troubleshooting-data-sources-sync-job-incomplete"></a>

Jobs are generally incomplete when they have completed the data source level process but have some error during the document level process\. When a job is incomplete, some of the documents may still have been successfully indexed\. For an Amazon S3 data source, an incomplete job is typically caused by:
+ The metadata for one or more documents was invalid\.
+ When documents are submitted for indexing but at least one document was not submitted\.
+ When documents are submitted for deleting from the index but at least one document was not submitted\.

To troubleshoot an incomplete synchronization job, look first to your CloudWatch logs\. 

1. From the details column, choose **View details in CloudWatch**\. 

1. Review the error messages to see what caused the document to fail\.

## My synchronization job succeeded but there are no indexed documents<a name="troubleshooting-data-sources-succeeded-no-indexed-docs"></a>

Occasionally, an index synchronization job run will be marked as **Succeeded** but there are no new or updated documents indexed when you expect them\. Possible reasons include:
+ Check CloudWatch `DocumentsSubmittedForIndexingFailed` metric to see if any documents failed to synchronize\. Check your CloudWatch logs for details\.
+ For an Amazon S3 data source, you may have given Kendra the wrong bucket name or prefix\. Make sure that the bucket that Kendra is using is the one that contains the documents to index\.
+ When re\-indexing a document that failed to be indexed in an earlier job, Kendra won't index it unless you've changed the document or its associated metadata file\.

## I am running into file format issues while syncing my data source<a name="troubleshooting-data-sources-file-format-issues"></a>

If you run into file format issues while adding files to your data source or syncing your data source, make sure that your document types are Kendra supported\. For a list of document types supported by Amazon Kendra see [Types of documents](https://docs.aws.amazon.com/kendra/latest/dg/index-document-types.html)\.

If you are using the `BatchPutDocument` API with plain text files, specify `PLAIN_TEXT` as content type\.

## How much time does syncing a data source take?<a name="troubleshooting-data-sources-sync-time"></a>

If there are no updates to documents, sync time for a Amazon Kendra index increases in linear proportion to the number of documents\. For example, 1,000 documents without any updates would take about five minutes to sync and 2,000 documents without any updates will take about 10 minutes\. If there are any updates to the documents, then the sync time will increase based on the number of documents updated\.

## What is the charge for syncing a data source?<a name="troubleshooting-data-sources-sync-charge"></a>

When you sync your index, it takes two minutes to warm up and activate Amazon EC2 to establish the necessary connections\. You are not charged during this process\. Your usage meter begins only after the sync job starts\. For more information on Kendra pricing, see [http://aws.amazon.com/https://aws.amazon.com/kendra/pricing/](http://aws.amazon.com/https://aws.amazon.com/kendra/pricing/)\.

## I am getting an Amazon EC2 authorization error<a name="troubleshooting-data-sources-ec2-error"></a>

If an Amazon EC2 unauthorized operation error occurs during a sync for a virtual private cloud \(VPC\) data source, it's likely that your VPC IAM role lacks required permissions\. Please check that the IAM role you use for your data source has the attached permissions\. For more information, see [Virtual private cloud \(VPC\) IAM role](iam-roles.md#iam-roles-vpc)\.

## I am unable to use search index links to open my Amazon S3 objects<a name="troubleshooting-data-unable-to-open-s3-links"></a>

Your Kendra index can only access files that an Amazon S3 data source grants it permissions to access\. For example, Kendra cannot modify the Amazon S3 permissions that determine if an object is meant to be public or encrypted\. Kendra also does not have the default permissions to create or return a signed link for Amazon S3 objects\. If you want to enable signed linking for Amazon S3 objects in a Kendra index, you have two options:
+ You can use sign your index query results with the source uri object before returning the result to the search page\. For a step\-by\-step walkthrough of this process, see [https://docs.aws.amazon.com/https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html](https://docs.aws.amazon.com/https://docs.aws.amazon.com/AmazonS3/latest/userguide/ShareObjectPreSignedURL.html)\.
+ You can override the Amazon S3 object metadata source uri and make your service available through an CloudFront content delivery network \(CDN\) connected to an Amazon S3 bucket\. Or, you can use an API Gateway proxy endpoint that returns a presigned URL and redirect to it\.

## I am getting an AccessDenied When Using SSL Certificate File error message<a name="troubleshooting-data-sources-ssl-certificate-access-denied"></a>

If you are getting an access denied error when using an SSL certificate with your data source, make sure that your IAM role has the permission to access the SSL certificate file in its specified location\. If the certificate is encrypted with an AWS KMS key, your IAM role should also have permission to decrypt using the AWS KMS key\. For more information, see [https://docs.aws.amazon.com/https://docs.aws.amazon.com/kms/latest/developerguide/control-access.html](https://docs.aws.amazon.com/https://docs.aws.amazon.com/kms/latest/developerguide/control-access.html)\.

## I am getting an authorization error when using a SharePoint data source<a name="troubleshooting-data-sources-sharepoint-authorization-error"></a>

If you are getting an authorization error while syncing your index with a SharePoint data source, confirm that you have a Site Admin role assigned to you in SharePoint\.

## My index does not crawl documents from my Confluence data source<a name="troubleshooting-data-sources-confluence-document-crawling"></a>

If your Kendra index is not crawling documents from your Confluence data source during the syncing process, confirm that you are part of Administrator Groups in Confluence\.