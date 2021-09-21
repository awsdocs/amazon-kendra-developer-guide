--------

--------

# S3DataSourceConfiguration<a name="API_S3DataSourceConfiguration"></a>

Provides configuration information for a data source to index documents in an Amazon S3 bucket\.

## Contents<a name="API_S3DataSourceConfiguration_Contents"></a>

 ** AccessControlListConfiguration **   <a name="Kendra-Type-S3DataSourceConfiguration-AccessControlListConfiguration"></a>
Provides the path to the S3 bucket that contains the user context filtering files for the data source\. For the format of the file, see [Access control for S3 data sources](https://docs.aws.amazon.com/kendra/latest/dg/s3-acl.html)\.  
Type: [ AccessControlListConfiguration ](API_AccessControlListConfiguration.md) object  
Required: No

 ** BucketName **   <a name="Kendra-Type-S3DataSourceConfiguration-BucketName"></a>
The name of the bucket that contains the documents\.  
Type: String  
Length Constraints: Minimum length of 3\. Maximum length of 63\.  
Pattern: `[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]`   
Required: Yes

 ** DocumentsMetadataConfiguration **   <a name="Kendra-Type-S3DataSourceConfiguration-DocumentsMetadataConfiguration"></a>
Document metadata files that contain information such as the document access control information, source URI, document author, and custom attributes\. Each metadata file contains metadata about a single document\.  
Type: [ DocumentsMetadataConfiguration ](API_DocumentsMetadataConfiguration.md) object  
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-S3DataSourceConfiguration-ExclusionPatterns"></a>
A list of glob patterns for documents that should not be indexed\. If a document that matches an inclusion prefix or inclusion pattern also matches an exclusion pattern, the document is not indexed\.  
Some [examples](https://docs.aws.amazon.com/cli/latest/reference/s3/#use-of-exclude-and-include-filters) are:  
+  *\*\.png , \*\.jpg* will exclude all PNG and JPEG image files in a directory \(files with the extensions \.png and \.jpg\)\.
+  *\*internal\** will exclude all files in a directory that contain 'internal' in the file name, such as 'internal', 'internal\_only', 'company\_internal'\.
+  *\*\*/\*internal\** will exclude all internal\-related files in a directory and its subdirectories\.
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-S3DataSourceConfiguration-InclusionPatterns"></a>
A list of glob patterns for documents that should be indexed\. If a document that matches an inclusion pattern also matches an exclusion pattern, the document is not indexed\.  
Some [examples](https://docs.aws.amazon.com/cli/latest/reference/s3/#use-of-exclude-and-include-filters) are:  
+  *\*\.txt* will include all text files in a directory \(files with the extension \.txt\)\.
+  *\*\*/\*\.txt* will include all text files in a directory and its subdirectories\.
+  *\*tax\** will include all files in a directory that contain 'tax' in the file name, such as 'tax', 'taxes', 'income\_tax'\.
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** InclusionPrefixes **   <a name="Kendra-Type-S3DataSourceConfiguration-InclusionPrefixes"></a>
A list of S3 prefixes for the documents that should be included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

## See Also<a name="API_S3DataSourceConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/S3DataSourceConfiguration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/S3DataSourceConfiguration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/S3DataSourceConfiguration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/S3DataSourceConfiguration) 