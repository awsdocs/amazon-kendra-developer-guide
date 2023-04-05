--------

--------

# ServiceNow<a name="data-source-servicenow"></a>

ServiceNow provides a cloud\-based service management system to create and manage organization\-level workflows, such as IT services, ticketing systems, and support\. You can use Amazon Kendra to index your ServiceNow catalogs, knowledge articles, incidents, and their attachments\.

You can connect Amazon Kendra to your ServiceNow data source using either the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API, or the [ServiceNowConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ServiceNowConfiguration.html) API\.

Amazon Kendra has two versions of the ServiceNow connector\. Supported features of each version include:

**ServiceNow connector v1\.0 / [ServiceNowConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_ServiceNowConfiguration.html) API**
+ Field mappings
+ ServiceNow instance versions: London, Others
+ Inclusion/exclusion patterns: Service catalogs, knowledge articles, attachments

**ServiceNow connector v2\.0 / [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API**
+ Field mappings
+ User context filtering
+ Virtual private cloud \(VPC\)
+ Sync all documents/Sync only new, modified, deleted documents
+ ServiceNow instance versions: Rome, Sandiego, Tokyo, Others
+ Inclusion/exclusion patterns: Service catalogs, knowledge articles, incidents, attachments

**Note**  
Support for ServiceNow connector v1\.0 / ServiceNowConfiguration API is scheduled to end by June 2023\. We recommend using ServiceNow connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra ServiceNow data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [ServiceNow connector v1\.0](data-source-v1-servicenow.md)
+ [ServiceNow connector v2\.0](data-source-v2-servicenow.md)
+ [Specifying documents to index with a query](servicenow-query.md)