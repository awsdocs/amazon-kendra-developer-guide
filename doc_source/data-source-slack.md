--------

--------

# Using a Slack data source<a name="data-source-slack"></a>

You can use your Slack workspace team as a data source for Amazon Kendra\. To use Slack in the console, go to the [Amazon Kendra console](https://console.aws.amazon.com/kendra/), select your index and then select **Data sources** from the navigation menu to add Slack\.

When you connect to Slack to index your channels and messages, you specify the Slack workspace team ID\. For example, *T0123456789*\. You can find your team ID in the URL of the main page of your Slack workspace\. When you log in to Slack via a browser, you are directed to the URL of the main page\. For example, *https://app\.slack\.com/client/**T0123456789**/\.\.\.*

You can specify regular expression patterns to include or exclude attached files in your Slack workspace team\. You can specify whether to index specific public channels or private channels\. You can specify whether to include bot messages and archived messages\. If you use a bot token as part of your Slack authentication credentials, you must add the bot token to the channel you want to index\. You cannot index direct messages and group messages using a bot token\.

You must create an index before you create the Slack data source\. For more information, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\. You provide the ID of the index when you create the data source\.

To connect to Slack, you specify the connection and other information in the console or by using the [SlackConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SlackConfiguration.html) object\. You provide the team ID of the Slack workspace that you want to index\.

Before you can index your channels and messages from your Slack workspace team, you must specify whether to include public channels, private channels, group messages, and direct messages\. You must also set the crawl date for when you want to start crawling data from Slack\. If you leave a Slack channel, the channel content is still searchable in Amazon Kendra, like it is still searchable in Slack\.

You also must provide the Amazon Resource Name \(ARN\) of an IAM role that gives permission to access your Slack workspace team\. You provide the ARN of an IAM role using the [CreateDataSource](https://docs.aws.amazon.com/kendra/latest/dg/API_CreateDataSource.html) API\. For more information on permissions, see [IAM roles for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

Amazon Kendra requires authentication credentials to access your Slack workspace team\. See [Authentication](#slack-authentication)\.

Amazon Kendra also crawls user information from the Slack instance\. This is useful for user context filtering, where search results are filtered based on the user or their group access to documents\. For more information, see [User context filtering for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html#context-filter-slack)\.

You also can add the following optional information:
+ Whether Amazon Kendra should use the Slack change log mechanism to determine if content must be updated in the index\. Use the change log if you don't want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Slack workspace than to process the change log\. If you are syncing your Slack data source with your index for the first time, all documents are scanned\.
+ Whether to look back beyond the last time you synchronized your data\. Change log updates your index only if new Slack content was added since the last time you synced your data\. To capture recently updated or deleted messages that date back before you last synced your data, enter the number of hours you want change log to look back from your last sync\. You can look back up to 7 days or 168 hours\.
+ Inclusion or exclusion pattern: If you specify an inclusion pattern, any attached file name or type that doesn't match the pattern isn't indexed\. If you specify an inclusion and exclusion pattern, attached files that match the exclusion pattern are not indexed even if they match the inclusion pattern\.
+ Field mappings that map your Slack fields to Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

## Authentication<a name="slack-authentication"></a>

The authentication credentials to access your Slack workspace team must include your Slack bot or user token\. You create the token in Slack\. You store your Slack credentials in an AWS Secrets Manager secret\. If you are using the Amazon Kendra console to create your data source, you can create the secret while creating the data source\. Or you can use an existing Secrets Manager secret\. If you are using the API to create your data source, you must provide the Amazon Resource Name \(ARN\) of an existing secret\.

The credentials are stored as a JSON string in the Secrets Manager secret\.

```
{ 
        "slackToken" : "token"
}
```

**To create a token in Slack**

1. Log in to the Slack desktop application\.

1. Select your workspace name dropdown at the top of the side menu, then select **Settings & administration**\.

1. Select **Manage apps**, then select **Build**\.

1. Select **Create New App**, then select **From scratch**\.

1. Enter a name for your app\. For example, *kendra\_slack\_app*\.

1. Choose a workspace for your app\.

1. Select **Create App**\.

1. If you do not see the name of your app at the top of the side menu, select your app's name on the main page\.

1. Select **OAuth & Permissions**, then scroll down to the **Scopes** section\.

1. Select **OAuth & Permissions**, then scroll down to the **Scopes** section\.

1. Choose the following permissions:
   + channels:history
   + channels:read
   + groups:history
   + groups:read
   + im:history
   + im:read
   + mpim:history
   + mpim:read
   + team:read
   + users\.profile:read
   + users:read
   + emoji:read
   + files:read
   + usergroups:read

   If you are updating your permissions for an existing app, select **Re\-install to workspace**\.

1. Scroll down to **Install to Workspace section**, then select **Allow**\.

1. Copy the **User OAuth Token** or the **Bot User OAuth Token**\. You'll need the token when you create the Secrets Manager secret for the Slack data source\. You can only use one token of your choice—the user token or the bot token you created\. If you use the bot token, you cannot index direct messages and group messages\.