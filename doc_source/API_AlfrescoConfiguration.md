--------

--------

# AlfrescoConfiguration<a name="API_AlfrescoConfiguration"></a>

Provides the configuration information to connect to Alfresco as your data source\.

## Contents<a name="API_AlfrescoConfiguration_Contents"></a>

 ** BlogFieldMappings **   <a name="Kendra-Type-AlfrescoConfiguration-BlogFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Alfresco blogs to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Alfresco fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Alfresco data source field names must exist in your Alfresco custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** CrawlComments **   <a name="Kendra-Type-AlfrescoConfiguration-CrawlComments"></a>
 `TRUE` to index comments of blogs and other content\.  
Type: Boolean  
Required: No

 ** CrawlSystemFolders **   <a name="Kendra-Type-AlfrescoConfiguration-CrawlSystemFolders"></a>
 `TRUE` to index shared files\.  
Type: Boolean  
Required: No

 ** DocumentLibraryFieldMappings **   <a name="Kendra-Type-AlfrescoConfiguration-DocumentLibraryFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Alfresco document libraries to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Alfresco fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Alfresco data source field names must exist in your Alfresco custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** EntityFilter **   <a name="Kendra-Type-AlfrescoConfiguration-EntityFilter"></a>
Specify whether to index document libraries, wikis, or blogs\. You can specify one or more of these options\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 3 items\.  
Valid Values:` wiki | blog | documentLibrary`   
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-AlfrescoConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain files in your Alfresco data source\. Files that match the patterns are excluded from the index\. Files that don't match the patterns are included in the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-AlfrescoConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain files in your Alfresco data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-AlfrescoConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Alfresco data source\. The secret must contain a JSON structure with the following keys:  
+ username—The user name of the Alfresco account\.
+ password—The password of the Alfresco account\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** SiteId **   <a name="Kendra-Type-AlfrescoConfiguration-SiteId"></a>
The identifier of the Alfresco site\. For example, *my\-site*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Pattern: `^[A-Za-z0-9-]+$`   
Required: Yes

 ** SiteUrl **   <a name="Kendra-Type-AlfrescoConfiguration-SiteUrl"></a>
The URL of the Alfresco site\. For example, *https://hostname:8080*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^https:\/\/[a-zA-Z0-9_\-\.]+$`   
Required: Yes

 ** SslCertificateS3Path **   <a name="Kendra-Type-AlfrescoConfiguration-SslCertificateS3Path"></a>
The path to the SSL certificate stored in an Amazon S3 bucket\. You use this to connect to Alfresco\.  
Type: [S3Path](API_S3Path.md) object  
Required: Yes

 ** VpcConfiguration **   <a name="Kendra-Type-AlfrescoConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud to connect to your Alfresco\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

 ** WikiFieldMappings **   <a name="Kendra-Type-AlfrescoConfiguration-WikiFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of Alfresco wikis to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Alfresco fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Alfresco data source field names must exist in your Alfresco custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

## See Also<a name="API_AlfrescoConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/AlfrescoConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/AlfrescoConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/AlfrescoConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/AlfrescoConfiguration) 