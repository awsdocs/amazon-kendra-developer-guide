--------

--------

# ConfluenceSpaceConfiguration<a name="API_ConfluenceSpaceConfiguration"></a>

Configuration information for indexing Confluence spaces\.

## Contents<a name="API_ConfluenceSpaceConfiguration_Contents"></a>

 ** CrawlArchivedSpaces **   <a name="Kendra-Type-ConfluenceSpaceConfiguration-CrawlArchivedSpaces"></a>
 `TRUE` to index archived spaces\.  
Type: Boolean  
Required: No

 ** CrawlPersonalSpaces **   <a name="Kendra-Type-ConfluenceSpaceConfiguration-CrawlPersonalSpaces"></a>
 `TRUE` to index personal spaces\. You can add restrictions to items in personal spaces\. If personal spaces are indexed, queries without user context information may return restricted items from a personal space in their results\. For more information, see [Filtering on user context](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.  
Type: Boolean  
Required: No

 ** ExcludeSpaces **   <a name="Kendra-Type-ConfluenceSpaceConfiguration-ExcludeSpaces"></a>
A list of space keys of Confluence spaces\. If you include a key, the blogs, documents, and attachments in the space are not indexed\. If a space is in both the `ExcludeSpaces` and the `IncludeSpaces` list, the space is excluded\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^\P{C}*$`   
Required: No

 ** IncludeSpaces **   <a name="Kendra-Type-ConfluenceSpaceConfiguration-IncludeSpaces"></a>
A list of space keys for Confluence spaces\. If you include a key, the blogs, documents, and attachments in the space are indexed\. Spaces that aren't in the list aren't indexed\. A space in the list must exist\. Otherwise, Amazon Kendra logs an error when the data source is synchronized\. If a space is in both the `IncludeSpaces` and the `ExcludeSpaces` list, the space is excluded\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `^\P{C}*$`   
Required: No

 ** SpaceFieldMappings **   <a name="Kendra-Type-ConfluenceSpaceConfiguration-SpaceFieldMappings"></a>
Maps attributes or field names of Confluence spaces to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Confluence fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Confluence data source field names must exist in your Confluence custom metadata\.  
If you specify the `SpaceFieldMappings` parameter, you must specify at least one field mapping\.  
Type: Array of [ConfluenceSpaceToIndexFieldMapping](API_ConfluenceSpaceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Required: No

## See Also<a name="API_ConfluenceSpaceConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluenceSpaceConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluenceSpaceConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluenceSpaceConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluenceSpaceConfiguration) 