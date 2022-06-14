--------

--------

# Using a Jira data source<a name="data-source-jira"></a>

You can use your Jira documents as a data source for Amazon Kendra\. To use Jira in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index, and then select **Data sources** from the navigation menu to add Jira\.

When you connect to Jira to index your documents, you specify the Jira account URL\. You can find your Jira account URL in the URL of your profile page for Jira desktop\. For example, *company\.atlassian\.net*\. You can specify what type of content to crawl in your Jira index\. You can specify from the following types of content: statuses, additional elements, and issue types\. You can specify regular expression patterns to include or exclude attached files in your Jira data source\. 

Create an index before you create the Jira data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Jira, you specify the connection and other information in the console or by using the [JiraConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_JiraConfiguration.html) object\. You provide the URL of the Jira account that you want to index\.

Before you can index your documents and messages from your Jira data source, you must specify which Jira Project IDs to crawl\. If you leave a Jira account URL, the content is still searchable in Amazon Kendra, just as it's still searchable in Jira\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Jira data source\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Jira data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Jira data source\. See [Authentication](#jira-authentication)\.

Amazon Kendra crawls user information from Jira projects\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Jira data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-jira)\.

You also can add the following optional information:
+ Whether Amazon Kendra should use the Jira change log mechanism to determine if content needs to be updated in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it may take Amazon Kendra less time to scan the documents in the Jira data source than to process the change log\. If you are syncing your Jira data source with your index for the first time, all documents are scanned\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any attached file name or type that does not match the pattern is not indexed\. If you specify an inclusion and exclusion pattern, files that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Jira fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="jira-authentication"></a>

The authentication credentials to access your Jira account must include your API token\. You create the token in Jira\. You store your Jira credentials, the secret, in AWS Secrets Manager\. The credentials are your Jira username and Jira API token\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. You can also store the credentials in an existing secret\. If you are using the API to create your data source, you must provide the ARN of an existing secret\.

The credentials are stored as a JSON string in Secrets Manager\.

```
{ 
        "jiraId": "Jira username",
        "jiraCredential": "Jira API token"
}
```

**To create a Jira API token**

1. Log into [id\.atlassian\.com/manage/api\-tokens](https://id.atlassian.com/manage/api-tokens)\.

1. Select **Create API token**\.

1. In the dialogue box, enter a memorable and concise **Label** for your token and click **Create**\.

1. Use **Copy to Clipboard** and paste the token into the Jira API token field on the Jira account user page\.

1. Copy the Jira API token\. You'll need it when you create the secret for the Jira data source in Secrets Manager\.

**Note**  
For security reasons, it isn't possible to view the API token once you close out the creation dialogue box\. If necessary, create a new token\.
Store the token securely, as you would for any password\.