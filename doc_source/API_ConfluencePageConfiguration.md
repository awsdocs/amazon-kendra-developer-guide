--------

--------

# ConfluencePageConfiguration<a name="API_ConfluencePageConfiguration"></a>

Specifies the page settings for the Confluence data source\.

## Contents<a name="API_ConfluencePageConfiguration_Contents"></a>

 ** PageFieldMappings **   <a name="Kendra-Type-ConfluencePageConfiguration-PageFieldMappings"></a>
Defines how page metadata fields should be mapped to index fields\. Before you can map a field, you must first create an index field with a matching type using the console or the `UpdateIndex` operation\.  
If you specify the `PageFieldMappings` parameter, you must specify at least one field mapping\.  
Type: Array of [ ConfluencePageToIndexFieldMapping ](API_ConfluencePageToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 12 items\.  
Required: No

## See Also<a name="API_ConfluencePageConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluencePageConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluencePageConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluencePageConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluencePageConfiguration) 