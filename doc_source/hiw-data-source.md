--------

--------

# Data sources<a name="hiw-data-source"></a>

A data source is a data repository or location that Amazon Kendra connects to and indexes your documents or content\. For example, you can configure Amazon Kendra to connect to Microsoft SharePoint to crawl and index your documents stored in this source\. You can also index web pages by providing the URLs for Amazon Kendra to crawl\. You can automatically synchronize a data source with an Amazon Kendra index so that added, updated, or deleted documents in the data source are also added, updated, or deleted in the index\.

Supported data sources are:
+ [Alfresco](https://docs.aws.amazon.com/kendra/latest/dg/data-source-alfresco.html)
+ [Amazon S3 buckets](https://docs.aws.amazon.com/kendra/latest/dg/data-source-s3.html)
+ Amazon RDS for MySQL, Amazon RDS for PostgreSQL, Amazon Aurora MySQL, Amazon Aurora PostgreSQL [databases](https://docs.aws.amazon.com/kendra/latest/dg/data-source-database.html)
+ [Amazon FSx](https://docs.aws.amazon.com/kendra/latest/dg/data-source-fsx.html)
+ [Amazon Kendra Web Crawler](https://docs.aws.amazon.com/kendra/latest/dg/data-source-web-crawler.html)
+ [Amazon WorkDocs](https://docs.aws.amazon.com/kendra/latest/dg/data-source-workdocs.html)
+ [Box](https://docs.aws.amazon.com/kendra/latest/dg/data-source-box.html)
+ [Confluence](https://docs.aws.amazon.com/kendra/latest/dg/data-source-confluence.html)
+ [Custom data sources](https://docs.aws.amazon.com/kendra/latest/dg/data-source-custom.html)
+ [Dropbox](https://docs.aws.amazon.com/kendra/latest/dg/data-source-dropbox.html)
+ [GitHub](https://docs.aws.amazon.com/kendra/latest/dg/data-source-github.html)
+ [Google Workspace Drives](https://docs.aws.amazon.com/kendra/latest/dg/data-source-google-drive.html)
+ [Jira](https://docs.aws.amazon.com/kendra/latest/dg/data-source-jira.html)
+ [Microsoft Exchange](https://docs.aws.amazon.com/kendra/latest/dg/data-source-exchange.html)
+ [Microsoft OneDrive](https://docs.aws.amazon.com/kendra/latest/dg/data-source-onedrive.html)
+ [Microsoft SharePoint](https://docs.aws.amazon.com/kendra/latest/dg/data-source-sharepoint.html)
+ [Microsoft Teams](https://docs.aws.amazon.com/kendra/latest/dg/data-source-teams.html)
+ [Microsoft Yammer](https://docs.aws.amazon.com/kendra/latest/dg/data-source-yammer.html)
+ [Quip](https://docs.aws.amazon.com/kendra/latest/dg/data-source-quip.html)
+ [Salesforce](https://docs.aws.amazon.com/kendra/latest/dg/data-source-salesforce.html)
+ [ServiceNow](https://docs.aws.amazon.com/kendra/latest/dg/data-source-servicenow.html)
+ [SharePoint](https://docs.aws.amazon.com/kendra/latest/dg/data-source-sharepoint.html)
+ [Slack](https://docs.aws.amazon.com/kendra/latest/dg/data-source-slack.html)
+ [Zendesk](https://docs.aws.amazon.com/kendra/latest/dg/data-source-zendesk.html)

For a list of document types supported by Amazon Kendra see [Types of documents](https://docs.aws.amazon.com/kendra/latest/dg/index-document-types.html)\.

**Note**  
To create an index, you don't need a data source\. You can add documents directly to an index\. For more information, see [Adding documents directly to an index](in-adding-documents.md)\.

**To index documents using a data source\.**

1. [Create an index](create-index.md)\.

1. [Create a data source](data-source.md)\.

 For a walkthrough with the Amazon Kendra console or with the AWS CLI, see [Getting started](getting-started.md)\.