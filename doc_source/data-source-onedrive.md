--------

--------

# Microsoft OneDrive<a name="data-source-onedrive"></a>

Microsoft OneDrive is cloud\-based storage service that you can use to store, share, and host your content\. You can use Amazon Kendra to index your OneDrive data source\.

You can connect Amazon Kendra to your OneDrive data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_OneDriveConfiguration.html) API\.

Amazon Kendra has two versions of the OneDrive connector\. Supported features of each version include:

**Microsoft OneDrive connector v1\.0 / [OneDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_OneDriveConfiguration.html) API**
+ Field mappings
+ Inclusion/exclusion filters

**Microsoft OneDrive connector v2\.0 / [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API**
+ User context filtering
+ Inclusion/exclusion filters
+ Identity crawler functionality
+ Sync all documents/Sync only new, modified, deleted documents

**Note**  
Support for OneDrive connector v1\.0 / OneDriveConfiguration API is scheduled to end by June 2023\. We recommend using OneDrive connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra OneDrive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Microsoft OneDrive connector v1\.0](data-source-v1-onedrive.md)
+ [Microsoft OneDrive connector v2\.0](data-source-v2-onedrive.md)