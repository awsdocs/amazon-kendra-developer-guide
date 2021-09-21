--------

--------

# SalesforceStandardObjectAttachmentConfiguration<a name="API_SalesforceStandardObjectAttachmentConfiguration"></a>

Provides configuration information for processing attachments to Salesforce standard objects\. 

## Contents<a name="API_SalesforceStandardObjectAttachmentConfiguration_Contents"></a>

<<<<<<< HEAD
 ** DocumentTitleFieldName **   <a name="Kendra-Type-SalesforceStandardObjectAttachmentConfiguration-DocumentTitleFieldName"></a>
=======
 **DocumentTitleFieldName**   <a name="Kendra-Type-SalesforceStandardObjectAttachmentConfiguration-DocumentTitleFieldName"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The name of the field used for the document title\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_.]*$`   
Required: No

<<<<<<< HEAD
 ** FieldMappings **   <a name="Kendra-Type-SalesforceStandardObjectAttachmentConfiguration-FieldMappings"></a>
One or more objects that map fields in attachments to Amazon Kendra index fields\.  
Type: Array of [ DataSourceToIndexFieldMapping ](API_DataSourceToIndexFieldMapping.md) objects  
=======
 **FieldMappings**   <a name="Kendra-Type-SalesforceStandardObjectAttachmentConfiguration-FieldMappings"></a>
One or more objects that map fields in attachments to Amazon Kendra index fields\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
>>>>>>> parent of 2b1c178 (updating tutorial)
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

## See Also<a name="API_SalesforceStandardObjectAttachmentConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/SalesforceStandardObjectAttachmentConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/SalesforceStandardObjectAttachmentConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/SalesforceStandardObjectAttachmentConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/SalesforceStandardObjectAttachmentConfiguration) 