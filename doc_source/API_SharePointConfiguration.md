--------

--------

# SharePointConfiguration<a name="API_SharePointConfiguration"></a>

Provides configuration information for connecting to a Microsoft SharePoint data source\.

## Contents<a name="API_SharePointConfiguration_Contents"></a>

<<<<<<< HEAD
 ** CrawlAttachments **   <a name="Kendra-Type-SharePointConfiguration-CrawlAttachments"></a>
=======
 **CrawlAttachments**   <a name="Kendra-Type-SharePointConfiguration-CrawlAttachments"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
 `TRUE` to include attachments to documents stored in your Microsoft SharePoint site in the index; otherwise, `FALSE`\.  
Type: Boolean  
Required: No

<<<<<<< HEAD
 ** DisableLocalGroups **   <a name="Kendra-Type-SharePointConfiguration-DisableLocalGroups"></a>
=======
 **DisableLocalGroups**   <a name="Kendra-Type-SharePointConfiguration-DisableLocalGroups"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A Boolean value that specifies whether local groups are disabled \(`True`\) or enabled \(`False`\)\.   
Type: Boolean  
Required: No

<<<<<<< HEAD
 ** DocumentTitleFieldName **   <a name="Kendra-Type-SharePointConfiguration-DocumentTitleFieldName"></a>
=======
 **DocumentTitleFieldName**   <a name="Kendra-Type-SharePointConfiguration-DocumentTitleFieldName"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Microsoft SharePoint attribute field that contains the title of the document\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^[a-zA-Z][a-zA-Z0-9_.]*$`   
Required: No

<<<<<<< HEAD
 ** ExclusionPatterns **   <a name="Kendra-Type-SharePointConfiguration-ExclusionPatterns"></a>
=======
 **ExclusionPatterns**   <a name="Kendra-Type-SharePointConfiguration-ExclusionPatterns"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A list of regular expression patterns\. Documents that match the patterns are excluded from the index\. Documents that don't match the patterns are included in the index\. If a document matches both an exclusion pattern and an inclusion pattern, the document is not included in the index\.  
The regex is applied to the display URL of the SharePoint document\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

<<<<<<< HEAD
 ** FieldMappings **   <a name="Kendra-Type-SharePointConfiguration-FieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map Microsoft SharePoint attributes to custom fields in the Amazon Kendra index\. You must first create the index fields using the `UpdateIndex` operation before you map SharePoint attributes\. For more information, see [Mapping Data Source Fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.  
Type: Array of [ DataSourceToIndexFieldMapping ](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-SharePointConfiguration-InclusionPatterns"></a>
=======
 **FieldMappings**   <a name="Kendra-Type-SharePointConfiguration-FieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map Microsoft SharePoint attributes to custom fields in the Amazon Kendra index\. You must first create the index fields using the `UpdateIndex` operation before you map SharePoint attributes\. For more information, see [Mapping Data Source Fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 **InclusionPatterns**   <a name="Kendra-Type-SharePointConfiguration-InclusionPatterns"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
A list of regular expression patterns\. Documents that match the patterns are included in the index\. Documents that don't match the patterns are excluded from the index\. If a document matches both an inclusion pattern and an exclusion pattern, the document is not included in the index\.  
The regex is applied to the display URL of the SharePoint document\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

<<<<<<< HEAD
 ** SecretArn **   <a name="Kendra-Type-SharePointConfiguration-SecretArn"></a>
=======
 **SecretArn**   <a name="Kendra-Type-SharePointConfiguration-SecretArn"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The Amazon Resource Name \(ARN\) of credentials stored in AWS Secrets Manager\. The credentials should be a user/password pair\. If you use SharePoint Server, you also need to provide the sever domain name as part of the credentials\. For more information, see [Using a Microsoft SharePoint Data Source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-sharepoint.html)\. For more information about AWS Secrets Manager, see [ What Is AWS Secrets Manager ](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the * AWS Secrets Manager * user guide\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

<<<<<<< HEAD
 ** SharePointVersion **   <a name="Kendra-Type-SharePointConfiguration-SharePointVersion"></a>
=======
 **SharePointVersion**   <a name="Kendra-Type-SharePointConfiguration-SharePointVersion"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The version of Microsoft SharePoint that you are using as a data source\.  
Type: String  
Valid Values:` SHAREPOINT_2013 | SHAREPOINT_2016 | SHAREPOINT_ONLINE`   
Required: Yes

<<<<<<< HEAD
 ** SslCertificateS3Path **   <a name="Kendra-Type-SharePointConfiguration-SslCertificateS3Path"></a>
Information required to find a specific file in an Amazon S3 bucket\.  
Type: [ S3Path ](API_S3Path.md) object  
Required: No

 ** Urls **   <a name="Kendra-Type-SharePointConfiguration-Urls"></a>
=======
 **SslCertificateS3Path**   <a name="Kendra-Type-SharePointConfiguration-SslCertificateS3Path"></a>
Information required to find a specific file in an Amazon S3 bucket\.  
Type: [S3Path](API_S3Path.md) object  
Required: No

 **Urls**   <a name="Kendra-Type-SharePointConfiguration-Urls"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
The URLs of the Microsoft SharePoint site that contains the documents that should be indexed\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^(https?|ftp|file):\/\/([^\s]*)`   
Required: Yes

<<<<<<< HEAD
 ** UseChangeLog **   <a name="Kendra-Type-SharePointConfiguration-UseChangeLog"></a>
=======
 **UseChangeLog**   <a name="Kendra-Type-SharePointConfiguration-UseChangeLog"></a>
>>>>>>> parent of 2b1c178 (updating tutorial)
Set to `TRUE` to use the Microsoft SharePoint change log to determine the documents that need to be updated in the index\. Depending on the size of the SharePoint change log, it may take longer for Amazon Kendra to use the change log than it takes it to determine the changed documents using the Amazon Kendra document crawler\.  
Type: Boolean  
Required: No

<<<<<<< HEAD
 ** VpcConfiguration **   <a name="Kendra-Type-SharePointConfiguration-VpcConfiguration"></a>
Provides information for connecting to an Amazon VPC\.  
Type: [ DataSourceVpcConfiguration ](API_DataSourceVpcConfiguration.md) object  
=======
 **VpcConfiguration**   <a name="Kendra-Type-SharePointConfiguration-VpcConfiguration"></a>
Provides information for connecting to an Amazon VPC\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
>>>>>>> parent of 2b1c178 (updating tutorial)
Required: No

## See Also<a name="API_SharePointConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/SharePointConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/SharePointConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/SharePointConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/SharePointConfiguration) 