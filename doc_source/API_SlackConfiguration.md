--------

--------

# SlackConfiguration<a name="API_SlackConfiguration"></a>

Provides the configuration information to connect to Slack as your data source\.

## Contents<a name="API_SlackConfiguration_Contents"></a>

 ** CrawlBotMessage **   <a name="Kendra-Type-SlackConfiguration-CrawlBotMessage"></a>
 `TRUE` to index bot messages from your Slack workspace team\.  
Type: Boolean  
Required: No

 ** ExcludeArchived **   <a name="Kendra-Type-SlackConfiguration-ExcludeArchived"></a>
 `TRUE` to exclude archived messages to index from your Slack workspace team\.  
Type: Boolean  
Required: No

 ** ExclusionPatterns **   <a name="Kendra-Type-SlackConfiguration-ExclusionPatterns"></a>
A list of regular expression patterns to exclude certain attached files in your Slack workspace team\. Files that match the patterns are excluded from the index\. Files that don’t match the patterns are included in the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** FieldMappings **   <a name="Kendra-Type-SlackConfiguration-FieldMappings"></a>
A list of `DataSourceToIndexFieldMapping` objects that map Slack data source attributes or field names to Amazon Kendra index field names\. To create custom fields, use the `UpdateIndex` API before you map to Slack fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\. The Slack data source field names must exist in your Slack custom metadata\.  
Type: Array of [DataSourceToIndexFieldMapping](API_DataSourceToIndexFieldMapping.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 100 items\.  
Required: No

 ** InclusionPatterns **   <a name="Kendra-Type-SlackConfiguration-InclusionPatterns"></a>
A list of regular expression patterns to include certain attached files in your Slack workspace team\. Files that match the patterns are included in the index\. Files that don't match the patterns are excluded from the index\. If a file matches both an inclusion and exclusion pattern, the exclusion pattern takes precedence and the file isn't included in the index\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 150\.  
Required: No

 ** LookBackPeriod **   <a name="Kendra-Type-SlackConfiguration-LookBackPeriod"></a>
The number of hours for change log to look back from when you last synchronized your data\. You can look back up to 7 days or 168 hours\.  
Change log updates your index only if new content was added since you last synced your data\. Updated or deleted content from before you last synced does not get updated in your index\. To capture updated or deleted content before you last synced, set the `LookBackPeriod` to the number of hours you want change log to look back\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 168\.  
Required: No

 ** PrivateChannelFilter **   <a name="Kendra-Type-SlackConfiguration-PrivateChannelFilter"></a>
The list of private channel names from your Slack workspace team\. You use this if you want to index specific private channels, not all private channels\. You can also use regular expression patterns to filter private channels\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** PublicChannelFilter **   <a name="Kendra-Type-SlackConfiguration-PublicChannelFilter"></a>
The list of public channel names to index from your Slack workspace team\. You use this if you want to index specific public channels, not all public channels\. You can also use regular expression patterns to filter public channels\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 ** SecretArn **   <a name="Kendra-Type-SlackConfiguration-SecretArn"></a>
The Amazon Resource Name \(ARN\) of an AWS Secrets Manager secret that contains the key\-value pairs required to connect to your Slack workspace team\. The secret must contain a JSON structure with the following keys:  
+ slackToken—The user or bot token created in Slack\. For more information on creating a token in Slack, see [Authentication for a Slack data source](https://docs.aws.amazon.com/kendra/latest/dg/data-source-slack.html#slack-authentication)\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1284\.  
Pattern: `arn:[a-z0-9-\.]{1,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[a-z0-9-\.]{0,63}:[^/].{0,1023}`   
Required: Yes

 ** SinceCrawlDate **   <a name="Kendra-Type-SlackConfiguration-SinceCrawlDate"></a>
The date to start crawling your data from your Slack workspace team\. The date must follow this format: `yyyy-mm-dd`\.  
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `(20\d{2})-(0?[1-9]|1[0-2])-(0?[1-9]|1\d|2\d|3[01])`   
Required: Yes

 ** SlackEntityList **   <a name="Kendra-Type-SlackConfiguration-SlackEntityList"></a>
Specify whether to index public channels, private channels, group messages, and direct messages\. You can specify one or more of these options\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 4 items\.  
Valid Values:` PUBLIC_CHANNEL | PRIVATE_CHANNEL | GROUP_MESSAGE | DIRECT_MESSAGE`   
Required: Yes

 ** TeamId **   <a name="Kendra-Type-SlackConfiguration-TeamId"></a>
The identifier of the team in the Slack workspace\. For example, *T0123456789*\.  
You can find your team ID in the URL of the main page of your Slack workspace\. When you log in to Slack via a browser, you are directed to the URL of the main page\. For example, *https://app\.slack\.com/client/**T0123456789**/\.\.\.*\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[A-Z0-9]*`   
Required: Yes

 ** UseChangeLog **   <a name="Kendra-Type-SlackConfiguration-UseChangeLog"></a>
 `TRUE` to use the Slack change log to determine which documents require updating in the index\. Depending on the Slack change log's size, it may take longer for Amazon Kendra to use the change log than to scan all of your documents in Slack\.  
Type: Boolean  
Required: No

 ** VpcConfiguration **   <a name="Kendra-Type-SlackConfiguration-VpcConfiguration"></a>
Configuration information for an Amazon Virtual Private Cloud to connect to your Slack\. For more information, see [Configuring a VPC](https://docs.aws.amazon.com/kendra/latest/dg/vpc-configuration.html)\.  
Type: [DataSourceVpcConfiguration](API_DataSourceVpcConfiguration.md) object  
Required: No

## See Also<a name="API_SlackConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/kendra-2019-02-03/SlackConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/kendra-2019-02-03/SlackConfiguration) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/kendra-2019-02-03/SlackConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/kendra-2019-02-03/SlackConfiguration) 