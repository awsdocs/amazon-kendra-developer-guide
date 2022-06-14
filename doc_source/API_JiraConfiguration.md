--------

--------

# JiraConfiguration<a name="API_JiraConfiguration"></a>

Provides the configuration information to connect to Jira as your data source\.

## Contents<a name="API_JiraConfiguration_Contents"></a>

 ** AttachmentFieldMappings **   <a name="Kendra-Type-JiraConfiguration-AttachmentFieldMappings"></a>
A list of DataSourceToIndexFieldMapping objects that map attributes or field names of Jira attachments to Amazon Kendra index field names\. To create custom fields, use the UpdateIndex API before you map to Jira fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Jira data source field names must exist in your Jira custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** CommentFieldMappings **   <a name="Kendra-Type-JiraConfiguration-CommentFieldMappings"></a>
A list of DataSourceToIndexFieldMapping objects that map attributes or field names of Jira comments to Amazon Kendra index field names\. To create custom fields, use the UpdateIndex API before you map to Jira fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Jira data source field names must exist in your Jira custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-JiraConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain file paths, file names, and file types in your Jira data source\. Files that match the patterns are excluded from the index\. Files that don’t match the patterns are included in the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-JiraConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain file paths, file names, and file types in your Jira data source\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion pattern and an exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** IssueFieldMappings **   <a name="Kendra-Type-JiraConfiguration-IssueFieldMappings"></a>
A list of DataSourceToIndexFieldMapping objects that map attributes or field names of Jira issues to Amazon Kendra index field names\. To create custom fields, use the UpdateIndex API before you map to Jira fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Jira data source field names must exist in your Jira custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** IssueSubEntityFilter **   <a name="Kendra-Type-JiraConfiguration-IssueSubEntityFilter"></a>
Specify whether to crawl comments, attachments, and work logs\. You can specify one or more of these options\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 3 items\.  
Valid Values:` COMMENTS | ATTACHMENTS | WORKLOGS`   
Required: No

 ** IssueType **   <a name="Kendra-Type-JiraConfiguration-IssueType"></a>
Specify which issue types to crawl in your Jira data source\. You can specify one or more of these options to crawl\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** JiraAccountUrl **   <a name="Kendra-Type-JiraConfiguration-JiraAccountUrl"></a>
The URL of the Jira account\. For example, *company\.atlassian\.net* or *https://jira\.company\.com*\. You can find your Jira account URL in the URL of your profile page for Jira desktop\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^https:\/\/[a-zA-Z0-9_\-\.]+(\.atlassian\.net\/)$`   
Required: Yes

 ** Project **   <a name="Kendra-Type-JiraConfiguration-Project"></a>
Specify which projects to crawl in your Jira data source\. You can specify one or more Jira project IDs\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** ProjectFieldMappings **   <a name="Kendra-Type-JiraConfiguration-ProjectFieldMappings"></a>
A list of DataSourceToIndexFieldMapping objects that map attributes or field names of Jira projects to Amazon Kendra index field names\. To create custom fields, use the UpdateIndex API before you map to Jira fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Jira data source field names must exist in your Jira custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-JiraConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of a secret in AWS Secrets Manager contains the key\-value pairs required to connect to your Jira data source\. The secret must contain a JSON structure with the following keys:  
+ jiraId—The Jira username\.
+ jiraCredentials—The Jira API token\. For more information on creating an API token in Jira, see [ Authentication for a Jira data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-jira.html#jira-authentication)\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** Status **   <a name="Kendra-Type-JiraConfiguration-Status"></a>
Specify which statuses to crawl in your Jira data source\. You can specify one or more of these options to crawl\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** UseChangeLog **   <a name="Kendra-Type-JiraConfiguration-UseChangeLog"></a>
 `TRUE` to use the Jira change log to determine which documents require updating in the index\. Depending on the change log's size, it may take longer for Amazon Kendra to use the change log than to scan all of your documents in Jira\.  
Type: Boolean  
Required: No

 ** VpcConfiguration **   <a name="Kendra-Type-JiraConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud to connect to your Jira\. Your Jira account must reside inside your VPC\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

 ** WorkLogFieldMappings **   <a name="Kendra-Type-JiraConfiguration-WorkLogFieldMappings"></a>
A list of DataSourceToIndexFieldMapping objects that map attributes or field names of Jira work logs to Amazon Kendra index field names\. To create custom fields, use the UpdateIndex API before you map to Jira fields\. For more information, see [ Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Jira data source field names must exist in your Jira custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

## See Also<a name="API_JiraConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/JiraConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/JiraConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/JiraConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/JiraConfiguration) 