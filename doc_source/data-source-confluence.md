--------

--------

# Confluence<a name="data-source-confluence"></a>

Confluence is a collaborative work\-management tool designed for sharing, storing, and working on project planning, software development, and product management\. You can use Amazon Kendra to index your Confluence spaces, pages \(including nested pages\), blogs, and comments and attachments to indexed pages and blogs\.

Amazon Kendra supports both Confluence Server and Confluence Cloud\.

**Note**  
By default, Amazon Kendra doesn't index Confluence archives and personal spaces\. You can choose to index them when you create the data source\. If you don't want Amazon Kendra to index a space, mark it private in Confluence\.

You can connect Amazon Kendra to your Confluence data source using either the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API, or the [ConfluenceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConfluenceConfiguration.html) API\.

Amazon Kendra has two versions of the Confluence connector\. Supported features of each version include:

**Confluence Connector v1\.0 / [ConfluenceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ConfluenceConfiguration.html) API**
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ \(For Confluence Server only\) Virtual private cloud \(VPC\)

**Confluence Connector v2\.0 / [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API**
+ Field mappings
+ User context filtering
+ Virtual private cloud \(VPC\)
+ Sync all documents/Sync only new, modified, or deleted documents
+ Inclusion/exclusion patterns

**Note**  
Support for Confluence Connector v1\.0 / ConfluenceConfiguration API is scheduled to end by June 2023\. We recommend using Confluence Connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Confluence data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Confluence Connector v1\.0](data-source-v1-confluence.md)
+ [Confluence Connector v2\.0](data-source-v2-confluence.md)