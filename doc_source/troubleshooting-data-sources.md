--------

--------

# Troubleshooting data sources<a name="troubleshooting-data-sources"></a>

This section can help you fix issues with Amazon Kendra data sources\.

## My documents were not indexed<a name="troubleshooting-data-sources-not-indexed"></a>

When you synchronize your Kendra index with a data source, you may run into issues that prevent the documents from being indexed\. Indexing is a two step process\. First, there is the data source level process of crawling the data source to find the new and updated documents to index, and to find any documents to remove from the index\. Second, there is the document level process where each document is accessed and indexed\. 

An error can occur in either of these steps\. Data source level errors are reported in the console in the **Sync run history** section of the data source details page\. The status of the synchronization job can be **Succeeded**, **Incomplete**, or **Failed**\. You can also see the number of documents indexed and deleted during the job\. If the status is **Failed**, a message is shown in the **Details** column\.

Document level errors are reported in Amazon CloudWatch Logs\. You can see the errors using the CloudWatch console\.

## My synchronization job failed<a name="troubleshooting-data-sources-failed"></a>

A synchronization job typically fails when there is a configuration error in the index or the data source\. The error message in the Details column of the data source gives information about what went wrong\. The problem is usually that the index or the data source does not have the proper IAM permissions\. The error message describes the permissions that are missing\. Here are some of the error messages that you can receive:

`Failed to create log group for job. Please make sure that the IAM role provided has sufficient permissions.`

If your index role does not have permission to use CloudWatch, the data source will not be able to create a CloudWatch log\. If you get this error you need to add CloudWatch permissions to the index role\.

`Failed to access S3 file prefix (bucket name) while trying to crawl your metadata files. Please make sure the IAM Role (role ARN) provided has sufficient permissions. `

When you are using an Amazon S3 data source, Kendra must have permission to access the bucket that contains the documents\. You need to add permission for Kendra to read the bucket to the data source IAM role\.

`The provided IAM Role (role ARN) could not be assumed. Please make sure Amazon Kendra is a trusted entity that is allowed to assume the role.`

Kendra needs permission to assume the index and data source IAM roles\. You need to add a trust policy to the roles with permission for the `sts:AssumeRole` action\.

For the IAM polices that Kendra needs to index a data source, see [IAM access roles for Amazon Kendra](iam-roles.md)\.

## My synchronization job is incomplete<a name="troubleshooting-data-sources-sync-job-incomplete"></a>

Jobs are generally incomplete when they have completed the data source level process but have had some error during the document level process\. When a job is incomplete, some of the documents may have been successfully indexed\. For an Amazon S3 data source, an incomplete job is typically caused by:\.
+ The metadata for one or more documents was invalid\.
+ When there are documents to submit for indexing, at least one document was not submitted\.
+ When there are documents to submit for deleting from the index, at least one document was not submitted\.

To troubleshoot an incomplete synchronization job, look first to your CloudWatch logs\. 

1. From the details column, choose **View details in CloudWatch**\. 

1. Review the error messages to see what caused the document to fail\.

## My synchronization job succeeded but there are no indexed documents<a name="troubleshooting-data-sources-succeeded-no-indexed-docs"></a>

Occasionally you will have a index synchronization job run that is marked as **Succeeded** but there are no new or updated documents indexed when you expect there to be\. Here are some reasons:
+ Check CloudWatch `DocumentsSubmittedForIndexingFailed` metric to see if there were any documents that failed to synchronize\. Check your CloudWatch logs for details\.
+ For an Amazon S3 data source, you may have given Kendra the wrong bucket name or prefix\. Make sure that the bucket that Kendra is using is the one that contains the documents to index\.
+ If you are re\-indexing a document that failed to be indexed in an earlier job, Kendra won't index it unless you make a change to the document or its associated metadata file\.