--------

--------

# WorkDocsConfiguration<a name="API_WorkDocsConfiguration"></a>

Provides the configuration information to connect to Amazon WorkDocs as your data source\.

Amazon WorkDocs connector is available in Oregon, North Virginia, Sydney, Singapore and Ireland regions\.

## Contents<a name="API_WorkDocsConfiguration_Contents"></a>

 **CrawlComments**   <a name="Kendra-Type-WorkDocsConfiguration-CrawlComments"></a>
 `TRUE` to include comments on documents in your index\. Including comments in your index means each comment is a document that can be searched on\.  
The default is set to `FALSE`\.  
Type: Boolean  
Required: No

 **ExclusionPatterns**   <a name="Kendra-Type-WorkDocsConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain files in your Amazon WorkDocs site repository\. Files that match the patterns are excluded from the index\. Files that don’t match the patterns are included in the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence and the file isn’t included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 **FieldMappings**   <a name="Kendra-Type-WorkDocsConfiguration-FieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map Amazon WorkDocs field names to custom index field names in Amazon Kendra\. You must first create the custom index fields using the `UpdateIndex` operation before you map to Amazon WorkDocs fields\. For more information, see [Mapping Data Source Fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Amazon WorkDocs data source field names need to exist in your Amazon WorkDocs custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 **InclusionPatterns**   <a name="Kendra-Type-WorkDocsConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain files in your Amazon WorkDocs site repository\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence and the file isn’t included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 **OrganizationId**   <a name="Kendra-Type-WorkDocsConfiguration-OrganizationId"></a>
The identifier of the directory corresponding to your Amazon WorkDocs site repository\.  
You can find the organization ID in the [AWS Directory Service](https://console.aws.amazon.com/directoryservicev2/) by going to **Active Directory**, then **Directories**\. Your Amazon WorkDocs site directory has an ID, which is the organization ID\. You can also set up a new Amazon WorkDocs directory in the AWS Directory Service console and enable a Amazon WorkDocs site for the directory in the Amazon WorkDocs console\.  
Type: String  
Length Constraints: Fixed length of 12\.  
Pattern: `d-[0-9a-fA-F]{10}`   
Required: Yes

 **UseChangeLog**   <a name="Kendra-Type-WorkDocsConfiguration-UseChangeLog"></a>
 `TRUE` to use the change logs to update documents in your index instead of scanning all documents\.  
If you are syncing your Amazon WorkDocs data source with your index for the first time, all documents are scanned\. After your first sync, you can use the change logs to update your documents in your index for future syncs\.  
The default is set to `FALSE`\.  
Type: Boolean  
Required: No

## See Also<a name="API_WorkDocsConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/WorkDocsConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/WorkDocsConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/WorkDocsConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/WorkDocsConfiguration) 