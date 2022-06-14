--------

--------

# Using an Amazon WorkDocs data source<a name="data-source-workdocs"></a>

You can use your Amazon WorkDocs as a data source for Amazon Kendra\. To use Amazon WorkDocs in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Amazon WorkDocs\.

Amazon WorkDocs connector is available in Oregon, North Virginia, Sydney, Singapore and Ireland regions\.

When you connect to Amazon WorkDocs to index your documents, you specify the directory ID that corresponds with your Amazon WorkDocs site repository\. You can specify regular expression patterns to include or exclude specific documents in your name of provider\.

You must create an index before you create the Amazon WorkDocs data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Amazon WorkDocs, you specify the connection and other information in the console or by using the [WorkDocsConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_WorkDocsConfiguration.html) object\. You provide the directory ID, which is the organization ID, of the Amazon WorkDocs site you want to index\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Amazon WorkDocs\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Amazon WorkDocs data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra also crawls user and group information from the Amazon WorkDocs instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Amazon WorkDocs data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-workdocs)\.

You also can add the following optional information:
+ Whether Amazon Kendra should index the contents of comments of your documents\. Each comment is indexed as a separate document\.
+ Whether Amazon Kendra should use the Amazon WorkDocs change log mechanism to determine if a document must be updated in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Amazon WorkDocs than to process the change log\. If you are syncing your Amazon WorkDocs data source with your index for the first time, all documents are scanned\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any document with a file name or file type that doesn't match the pattern is not indexed\. If you specify an inclusion and exclusion pattern, documents that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Amazon WorkDocs fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.