--------

--------

# Google Drive<a name="data-source-google-drive"></a>

Google Drive is a cloud\-based file storage service\. You can use Amazon Kendra to index documents stored in shared drives, My Drives, and Shared with me folders in your Google Drive data source\. You can index both Google Workspace documents as well as documents listed in [Types of documentation](https://docs.aws.amazon.com/kendra/latest/dg/index-document-types.html)\. You can also use inclusion and exclusion filters to index content by file name, file type, and file path\.

You can connect Amazon Kendra to your Google Drive data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), the [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API, or the [GoogleDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GoogleDriveConfiguration.html) API\.

Amazon Kendra has two versions of the Google Drive connector\. Supported features of each version include:

**Google Drive connector v1\.0 / [GoogleDriveConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_GoogleDriveConfiguration.html) API**
+ Field mappings
+ Inclusion/exclusion filters

**Google Drive connector v2\.0 / [TemplateConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_TemplateConfiguration.html) API**
+ User context filtering
+ Virtual private cloud \(VPC\)
+ Inclusion/exclusion filters
+ Sync all documents/Sync only new, modified, or deleted documents

**Note**  
Support for Google Drive connector v1\.0 / GoogleDriveConfiguration API is scheduled to end by June 2023\. We recommend using Google Drive connector v2\.0 / TemplateConfiguration API\.

For troubleshooting your Amazon Kendra Google Drive data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Google Drive connector v1\.0](data-source-v1-google-drive.md)
+ [Google Drive connector v2\.0](data-source-v2-google-drive.md)