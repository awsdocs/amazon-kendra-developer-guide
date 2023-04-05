--------

--------

# Microsoft SharePoint<a name="data-source-sharepoint"></a>

SharePoint is a collaborative website building service that you can use to customize web content and create pages, sites, document libraries, and lists\. You can use Amazon Kendra to index your SharePoint data source\.

Amazon Kendra currently supports SharePoint Online and SharePoint Server \(versions 2013, 2016, 2019, and Subscription Edition\)\.

You can connect Amazon Kendra to your SharePoint data source using either the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API, or the [SharePointConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SharePointConfiguration.html) API\.

Amazon Kendra has two versions of the SharePoint connector\. SharePoint Connector v2\.0 is the new and updated version of Amazon Kendra SharePoint connector v1\.0\. Supported features of each version include:

**SharePoint Connector v1\.0 / [SharePointConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SharePointConfiguration.html) API**
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

**SharePoint Connector v2\.0 / [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API**
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)
+ Sync all documents/Sync only new or modified documents/Sync only new, modified, or deleted documents

**Note**  
Support for SharePoint Connector v1\.0 / SharePointConfiguration API is scheduled to end by June 2023\. We recommend using SharePoint Connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra SharePoint data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [SharePoint connector v1\.0](data-source-v1-sharepoint.md)
+ [SharePoint connector v2\.0](data-source-v2-sharepoint.md)