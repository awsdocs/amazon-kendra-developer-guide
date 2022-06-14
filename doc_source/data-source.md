--------

--------

# Creating a data source<a name="data-source"></a>

You can create a data source to connect to your documents stored in Microsoft SharePoint, Google Drive, and other providers\. When you create a data source, you give Amazon Kendra the location of documents that it indexes\. Unlike adding documents directly to an index, you can periodically scan the data source to update the index\.

For example, say that you have a repository of tax instruction stored in an S3 bucket\. From time to time, existing documents are changed and new documents are added to the repository\. If you add the repository to Amazon Kendra as a data source, you can keep your index up to date by periodically updating your index\.

You can update the index manually using console or the [StartDataSourceSyncJob](API_StartDataSourceSyncJob.md) API, or you can set up a schedule to update the index\. 

An index can have more than one data source\. Each data source can have its own update schedule\. For example, you might update the index of your working documents daily, or even hourly, while updating your archived documents manually whenever the archive changes\.

If you want to alter your document metadata or attributes and content during the document ingestion process, see [Amazon Kendra Custom Document Enrichment](https://docs.aws.amazon.com/kendra/latest/dg/custom-document-enrichment.html)\.

Note, each document ID must be unique per index\. You cannot create a data source to index your documents with their unique IDs and then use the `BatchPutDocument` API to index the same documents, or vice versa\. You can delete a data source and then use the `BatchPutDocument` API to index the same documents, or vice versa\.

## Setting an update schedule<a name="cron"></a>

Configure your data source to periodically update with the console or by using the `Schedule` parameter when you create or update a data source\. The content of the parameter is a string that holds either a `cron`\-format schedule string or an empty string to indicate that the index is updated on demand\. For the format of a cron expression, see [Schedule Expressions for Rules](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html) in the *Amazon CloudWatch Events User Guide*\. Amazon Kendra supports only cron expressions\. It doesn't support rate expressions\.

## Setting a language<a name="language"></a>

You can index all your documents in a data source in a supported language\. You specify the language code for all your documents in your data source when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html)\. If a document doesn't have a language code specified in a metadata field, the document is indexed using the language code that's specified for all documents at the data source level\. If you don't specify a language, Amazon Kendra indexes documents in a data source in English by default\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.

You index all your documents in a data source in a supported language using the console\. Go to **Data sources** and edit your data source or **Add data source** if you're adding a new data source\. On the **Specify data source details** page, choose a language from the dropdown **Language**\. You select **Update** or continue to enter the configuration information to connect to your data source\.