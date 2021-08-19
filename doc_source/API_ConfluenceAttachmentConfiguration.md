--------

--------

# ConfluenceAttachmentConfiguration<a name="API_ConfluenceAttachmentConfiguration"></a>

Specifies the attachment settings for the Confluence data source\. Attachment settings are optional, if you don't specify settings attachments, Amazon Kendra won't index them\.

## Contents<a name="API_ConfluenceAttachmentConfiguration_Contents"></a>

 **AttachmentFieldMappings**   <a name="Kendra-Type-ConfluenceAttachmentConfiguration-AttachmentFieldMappings"></a>
Defines how attachment metadata fields should be mapped to index fields\. Before you can map a field, you must first create an index field with a matching type using the console or the `UpdateIndex` operation\.  
If you specify the `AttachentFieldMappings` parameter, you must specify at least one field mapping\.  
Type: Array of [ConfluenceAttachmentToIndexFieldMapping](API_ConfluenceAttachmentToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 11 items\.  
Required: No

 **CrawlAttachments**   <a name="Kendra-Type-ConfluenceAttachmentConfiguration-CrawlAttachments"></a>
Indicates whether Amazon Kendra indexes attachments to the pages and blogs in the Confluence data source\.   
Type: Boolean  
Required: No

## See Also<a name="API_ConfluenceAttachmentConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 