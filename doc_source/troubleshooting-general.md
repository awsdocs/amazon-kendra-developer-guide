--------

--------

# Troubleshooting general issues<a name="troubleshooting-general"></a>

Kendra uses CloudWatch metrics and logs to provide insight into synchronizing your data sources\. You can use the metrics and logs to determine what went wrong with a synchronization run and how to fix it\. 

For general troubleshooting, start with your CloudWatch metrics\. 
+ Check the `DocumentsCrawled` metric to see how many documents your data source checked\. For an Amazon S3 bucket, if the number is less than you expect, check that your data source is pointing to the right bucket\.
+ Check the `DocumentsSkippedNoChange` metric to see how many documents were skipped because they haven't changed since the last synchronization\. If the number does not match what you expect, check that your repository was updated correctly\. 
+ Check the `DocumentsSkippedInvalidMetadata` metric to see how many documents had invalid metadata\. Check your CloudWatch logs to see the specific errors that occurred\.
+ Check the `DocumentsSubmittedForIndexingFailed` metric to see how many documents were sent from the data source to the index but failed to be indexed\. For example, if you use a metadata attribute in an Amazon S3 data source that hasn't been defined as a custom index field, the document will not be indexed\. Check your CloudWatch logs to see the specific errors that occurred\.
+ Check the `DocumentsSubmittedForDeletionFailed` metric to see how many documents that the data source attempted to remove from the index failed to be deleted from the index\. Check your CloudWatch logs to see the specific errors that occurred\.

You can look at the CloudWatch logs for a particular synchronization run to get details of the errors that occurred during the run\. For more information about CloudWatch logs with Kendra, see [Monitoring Amazon Kendra with Amazon CloudWatch Logs](cloudwatch-logs.md)\.