--------

--------

# ConfluenceAttachmentConfiguration<a name="API_ConfluenceAttachmentConfiguration"></a>

Configuration of attachment settings for the Confluence data source\. Attachment settings are optional, if you don't specify settings attachments, Amazon Kendra won't index them\.

## Contents<a name="API_ConfluenceAttachmentConfiguration_Contents"></a>

 ** AttachmentFieldMappings **   <a name="Kendra-Type-ConfluenceAttachmentConfiguration-AttachmentFieldMappings"></a>
Maps attributes or field names of Confluence attachments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Confluence fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Confluence data source field names must exist in your Confluence custom metadata\.  
If you specify the `AttachentFieldMappings` parameter, you must specify at least one field mapping\.  
Type: Array of [ConfluenceAttachmentToIndexFieldMapping](API_ConfluenceAttachmentToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 11 items\.  
Required: No

 ** CrawlAttachments **   <a name="Kendra-Type-ConfluenceAttachmentConfiguration-CrawlAttachments"></a>
 `TRUE` to index attachments of pages and blogs in Confluence\.  
Type: Boolean  
Required: No

## See Also<a name="API_ConfluenceAttachmentConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluenceAttachmentConfiguration) 