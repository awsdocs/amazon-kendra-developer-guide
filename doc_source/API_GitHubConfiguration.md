--------

--------

# GitHubConfiguration<a name="API_GitHubConfiguration"></a>

Provides the configuration information to connect to GitHub as your data source\.

## Contents<a name="API_GitHubConfiguration_Contents"></a>

 ** ExclusionFileNamePatterns **   <a name="Kendra-Type-GitHubConfiguration-ExclusionFileNamePatterns"></a>
A list of regular expression patterns to exclude certain file names in your GitHub repository or repositories\. File names that match the patterns are excluded from the index\. File names that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** ExclusionFileTypePatterns **   <a name="Kendra-Type-GitHubConfiguration-ExclusionFileTypePatterns"></a>
A list of regular expression patterns to exclude certain file types in your GitHub repository or repositories\. File types that match the patterns are excluded from the index\. File types that don't match the patterns are included in the index\. If a file matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** ExclusionFolderNamePatterns **   <a name="Kendra-Type-GitHubConfiguration-ExclusionFolderNamePatterns"></a>
A list of regular expression patterns to exclude certain folder names in your GitHub repository or repositories\. Folder names that match the patterns are excluded from the index\. Folder names that don't match the patterns are included in the index\. If a folder matches both an exclusion and inclusion pattern, the exclusion pattern takes precedence and the folder isn't included in the index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** GitHubCommitConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubCommitConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub commits to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubDocumentCrawlProperties **   <a name="Kendra-Type-GitHubConfiguration-GitHubDocumentCrawlProperties"></a>
Configuration information to include certain types of GitHub content\. You can configure to index repository files only, or also include issues and pull requests, comments, and comment attachments\.  
Type: [GitHubDocumentCrawlProperties](API_GitHubDocumentCrawlProperties.md) object  
Required: No

 ** GitHubIssueAttachmentConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubIssueAttachmentConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub issue attachments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubIssueCommentConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubIssueCommentConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub issue comments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubIssueDocumentConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubIssueDocumentConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub issues to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubPullRequestCommentConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubPullRequestCommentConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub pull request comments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubPullRequestDocumentAttachmentConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubPullRequestDocumentAttachmentConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub pull request attachments to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubPullRequestDocumentConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubPullRequestDocumentConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map attributes or field names of GitHub pull requests to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** GitHubRepositoryConfigurationFieldMappings **   <a name="Kendra-Type-GitHubConfiguration-GitHubRepositoryConfigurationFieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map GitHub repository attributes or field names to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to GitHub fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The GitHub data source field names must exist in your GitHub custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** InclusionFileNamePatterns **   <a name="Kendra-Type-GitHubConfiguration-InclusionFileNamePatterns"></a>
A list of regular expression patterns to include certain file names in your GitHub repository or repositories\. File names that match the patterns are included in the index\. File names that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** InclusionFileTypePatterns **   <a name="Kendra-Type-GitHubConfiguration-InclusionFileTypePatterns"></a>
A list of regular expression patterns to include certain file types in your GitHub repository or repositories\. File types that match the patterns are included in the index\. File types that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** InclusionFolderNamePatterns **   <a name="Kendra-Type-GitHubConfiguration-InclusionFolderNamePatterns"></a>
A list of regular expression patterns to include certain folder names in your GitHub repository or repositories\. Folder names that match the patterns are included in the index\. Folder names that don't match the patterns are excluded from the index\. If a folder matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the folder isn't included in the index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** OnPremiseConfiguration **   <a name="Kendra-Type-GitHubConfiguration-OnPremiseConfiguration"></a>
Configuration information to connect to GitHub Enterprise Server \(on premises\)\.  
Type: [OnPremiseConfiguration](API_OnPremiseConfiguration.md) object  
Required: No

 ** RepositoryFilter **   <a name="Kendra-Type-GitHubConfiguration-RepositoryFilter"></a>
A list of names of the specific repositories you want to index\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `^[A-Za-z0-9_.-]+$`   
Required: No

 ** SaaSConfiguration **   <a name="Kendra-Type-GitHubConfiguration-SaaSConfiguration"></a>
Configuration information to connect to GitHub Enterprise Cloud \(SaaS\)\.  
Type: [SaaSConfiguration](API_SaaSConfiguration.md) object  
Required: No

 ** SecretArn **   <a name="Kendra-Type-GitHubConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your GitHub\. The secret must contain a JSON structure with the following keys:  
+ personalToken—The access token created in GitHub\. For more information on creating a token in GitHub, see [Authentication for a GitHub data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-github.html#github-authentication)\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** Type **   <a name="Kendra-Type-GitHubConfiguration-Type"></a>
The type of GitHub service you want to connect to—GitHub Enterprise Cloud \(SaaS\) or GitHub Enterprise Server \(on premises\)\.  
Type: String  
Valid Values:` SAAS | ON_PREMISE`   
Required: No

 ** UseChangeLog **   <a name="Kendra-Type-GitHubConfiguration-UseChangeLog"></a>
 `TRUE` to use the GitHub change log to determine which documents require updating in the index\. Depending on the GitHub change log's size, it may take longer for Amazon Kendra to use the change log than to scan all of your documents in GitHub\.  
Type: Boolean  
Required: No

 ** VpcConfiguration **   <a name="Kendra-Type-GitHubConfiguration-VpcConfiguration"></a>
Configuration information of an Amazon Virtual Private Cloud to connect to your GitHub\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

## See Also<a name="API_GitHubConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/GitHubConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/GitHubConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/GitHubConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/GitHubConfiguration) 