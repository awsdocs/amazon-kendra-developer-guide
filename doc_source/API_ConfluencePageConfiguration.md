--------

--------

# ConfluencePageConfiguration<a name="API_ConfluencePageConfiguration"></a>

Configuration of the page settings for the Confluence data source\.

## Contents<a name="API_ConfluencePageConfiguration_Contents"></a>

 ** PageFieldMappings **   <a name="Kendra-Type-ConfluencePageConfiguration-PageFieldMappings"></a>
Maps attributes or field names of Confluence pages to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Confluence fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Confluence data source field names must exist in your Confluence custom metadata\.  
If you specify the `PageFieldMappings` parameter, you must specify at least one field mapping\.  
Type: Array of [ConfluencePageToIndexFieldMapping](API_ConfluencePageToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 12 items\.  
Required: No

## See Also<a name="API_ConfluencePageConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluencePageConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluencePageConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluencePageConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluencePageConfiguration) 