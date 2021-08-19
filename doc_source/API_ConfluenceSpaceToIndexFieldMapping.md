--------

--------

# ConfluenceSpaceToIndexFieldMapping<a name="API_ConfluenceSpaceToIndexFieldMapping"></a>

Defines the mapping between a field in the Confluence data source to a Amazon Kendra index field\.

You must first create the index field using the `UpdateIndex` operation\. 

## Contents<a name="API_ConfluenceSpaceToIndexFieldMapping_Contents"></a>

 **DataSourceFieldName**   <a name="Kendra-Type-ConfluenceSpaceToIndexFieldMapping-DataSourceFieldName"></a>
The name of the field in the data source\.   
Type: String  
Valid Values:` DISPLAY_URL | ITEM_TYPE | SPACE_KEY | URL`   
Required: No

 **DateFieldFormat**   <a name="Kendra-Type-ConfluenceSpaceToIndexFieldMapping-DateFieldFormat"></a>
The format for date fields in the data source\. If the field specified in `DataSourceFieldName` is a date field you must specify the date format\. If the field is not a date field, an exception is thrown\.  
Type: String  
Length Constraints: Minimum length of 4\. Maximum length of 40\.  
Pattern: `^(?!\s).*(?<!\s)$`   
Required: No

 **IndexFieldName**   <a name="Kendra-Type-ConfluenceSpaceToIndexFieldMapping-IndexFieldName"></a>
The name of the index field to map to the Confluence data source field\. The index field type must match the Confluence field type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 30\.  
Pattern: `^\P{C}*$`   
Required: No

## See Also<a name="API_ConfluenceSpaceToIndexFieldMapping_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/ConfluenceSpaceToIndexFieldMapping) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/ConfluenceSpaceToIndexFieldMapping) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/ConfluenceSpaceToIndexFieldMapping) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/ConfluenceSpaceToIndexFieldMapping) 