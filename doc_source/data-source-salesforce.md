--------

--------

# Salesforce<a name="data-source-salesforce"></a>

Salesforce is a customer relationship management \(CRM\) tool for managing support, sales, and marketing teams\. You can use Amazon Kendra to index your Salesforce standard objects and even custom objects\. 

You can connect Amazon Kendra to your Salesforce data source using either the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API, or the [SalesforceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SalesforceConfiguration.html) API\.

Amazon Kendra has two versions of the Salesforce connector\. Supported features of each version include:

**Salesforce connector v1\.0 / [SalesforceConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SalesforceConfiguration.html) API**
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters

**Salesforce connector v2\.0 / [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API**
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Entity attachment support
+ Identity crawling
+ VPC support
+ Sync all documents/Sync only new, modified, or deleted documents

**Note**  
Support for Salesforce connector v1\.0 / SalesforceConfiguration API is scheduled to end by June 2023\. We recommend using Salesforce connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Salesforce data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Salesforce connector v1\.0](data-source-v1-salesforce.md)
+ [Salesforce connector v2\.0](data-source-v2-salesforce.md)