--------

--------

# Adding documents from a data source<a name="data-source"></a>

When you create a data source, you give Amazon Kendra the location of documents that it should index\. Unlike adding documents directly to an index, you can periodically scan the data source to update the index\. 

For example, say that you have a repository of tax instruction stored in an Amazon S3 bucket\. Existing documents are changed and new documents are added to the repository from time to time\. If you add the repository to Amazon Kendra as a data source, you can keep your index up to date by periodically updating your index\.

You can update the index manually using console or the [ StartDataSourceSyncJob ](API_StartDataSourceSyncJob.md) operation, or you can set up a schedule to update the index\. 

An index can have more than one data source\. Each data source can have its own update schedule\. For example, you might update the index of your working documents daily, or even hourly, while updating your archived documents manually whenever the archive changes\.

## Setting an update schedule<a name="cron"></a>

Configure your data source to periodically update with the console or by using the `Schedule` parameter when you create or update a data source\. The content of the parameter is a string that holds either a `cron`\-format schedule string or an empty string to indicate that the index should be updated on demand\. For the format of a cron expression, see [Schedule Expressions for Rules](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html) in the *Amazon CloudWatch Events User Guide*\. Amazon Kendra supports only cron expressions\. It does not support rate expressions\.

## Setting a language<a name="language"></a>

You can index all your documents in a data source in a supported language\. You specify the language code for all your documents in your data source when you call [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_DeleteDataSource.html)\. If a document does not have a language code specified in a metadata field, the document is indexed using the language code specified for all documents at the data source level\. If you do not specify a language, Amazon Kendra indexes documents in a data source in English by default\. For more information on supported languages, including their codes, see [Adding documents in languages other than English](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages.html)\.

You index all your documents in a data source in a supported language using the console\. Go to **Data sources** or **Add data sources** if you are adding a new data source\. On the **Specify data source details** page, choose a language from the dropdown **Language**\. You select **Update** or continue to enter the configuration information to connect to your data source\.

**Topics**
+  [Using an Amazon S3 data source](data-source-s3.md) 
+  [Using an Atlassian Confluence data source](data-source-confluence.md) 
+  [Using a custom data source](data-source-custom.md) 
+  [Using a database data source](data-source-database.md) 
+  [Using a Google Workspace Drive data source](data-source-google-drive.md) 
+  [Using a Microsoft OneDrive data source](data-source-onedrive.md) 
+  [Using a Salesforce data source](data-source-salesforce.md) 
+  [Using a ServiceNow data source](data-source-servicenow.md) 
+  [Using a Microsoft SharePoint data source](data-source-sharepoint.md) 
+  [Using a web crawler data source](data-source-web-crawler.md) 