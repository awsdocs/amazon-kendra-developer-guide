--------

--------

# Data sources<a name="hiw-data-source"></a>

A *data source* is a location, such as an Amazon Simple Storage Service \(Amazon S3\) bucket, where you store the documents for indexing\. You can automatically synchronize data sources with an Amazon Kendra index so that new, updated, or deleted documents in the data source are also added, updated, or deleted in the index for searching on\.

Supported data sources are:
+ Amazon S3 buckets
+ Confluence instances
+ Google Workspace Drives
+ Amazon RDS for MySQL and Amazon RDS for PostgreSQL databases
+ Confluence cloud and Confluence server
+ Custom data sources
+ Microsoft OneDrive for Business
<<<<<<< HEAD
+ Microsoft SharePoint online and SharePoint server \(versions 2013 and 2016
+ Salesforce sites
+ ServiceNow instances
+ Amazon Kendra web crawler
+ Amazon WorkDocs
=======
+ Microsoft SharePoint
+ Salesforce sites
+ ServiceNow instances
+ Amazon Kendra web crawler
>>>>>>> parent of 2b1c178 (updating tutorial)

Supported document formats are: plain text, Microsoft Word, Microsoft PowerPoint, HTML, and PDF\. For more information, see [Types of documents](index-document-types.md)\.

**Note**  
To create an index, you don't need a data source\. You can add documents directly to an index\. For more information, see [Adding documents directly to an index](in-adding-documents.md)\.

**To index documents using a data source\.**

1. [Create an index](create-index.md)\.

1. [Create a data source](data-source.md)\.

 For a walkthrough with the Amazon Kendra console or with the AWS CLI, see [Getting started](getting-started.md)\.