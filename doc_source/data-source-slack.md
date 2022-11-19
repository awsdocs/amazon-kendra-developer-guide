--------

--------

# Using a Slack data source<a name="data-source-slack"></a>

Slack is an enterprise communications app that lets users send messages and attachments through various public and private channels\. If you are a Slack user, you can use Amazon Kendra to index your Slack public and private channels, bot and archive messages, files and attachments, direct and group messages\. You can also choose specific content to filter\.

You can connect Amazon Kendra to your Slack data source using the [Amazon Kendra console](https://console.aws.amazon.com/kendra/) and the [SlackConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SlackConfiguration.html) API\.

For troubleshooting your Amazon Kendra Slack data source connector, see [Troubleshooting data sources](troubleshooting-data-sources.md)\.

**Topics**
+ [Supported features](#supported-features-slack)
+ [Prerequisites](#prerequisites-slack)
+ [Connecting Amazon Kendra to your Slack data source](#data-source-procedure-slack)
+ [Learn more](#slack-learn-more)

## Supported features<a name="supported-features-slack"></a>
+ Change log
+ Field mappings
+ User context filtering
+ Inclusion/exclusion filters
+ Virtual private cloud \(VPC\)

## Prerequisites<a name="prerequisites-slack"></a>

Before you can use Amazon Kendra to index your Slack data source, you must meet the following requirements:
+ You have created an Amazon Kendra index\. You must create an index before you create the data source\. You need the index id to connect your data source\. For more information on how to create an Amazon Kendra index, see [Creating an index](https://docs.aws.amazon.com/kendra/latest/dg/create-index.html)\.
+ You have an IAM role for your data source\. Amazon Kendra uses this role to access the AWS resources required to create the Amazon Kendra resource\. You provide the Amazon Resource Name \(ARN\) of the IAM role with the policy attached when you connect your data source to Amazon Kendra\. If you are using the API, you must create an IAM role before you connect your datasource\. If you use the AWS console, you can choose to use an existing IAM role or create a new one when you configure your Amazon Kendra connector\. For more information on using an IAM role for your Slack data source, see [IAM roles for data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ You have a Slack account in which you have created either a Slack Bot User OAuth token or Slack User OAuth token\. You can choose either token to connect Amazon Kendra to your Slack data source\.
**Note**  
If you use the bot token, you cannot index direct messages and group messages\. If you use a bot token as part of your Slack authentication credentials, you must add the bot token to the channel you want to index\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ You have noted your Slack workspace team ID from your Slack workspace main page URL\. For example, *https://app\.slack\.com/client/T0123456789/\.\.\. * where *T0123456789* is the team ID\.
+ You have added the following permissions to your Slack account:
  + channels:history
  + channels:read
  + groups:history
  + groups:read
  + im:history
  + mpim:history
  + mpim:read
  + team:read
  + users\.profile:read
  + users:read
  + emoji:read
  + files:read
  + usergroups:read

  You can find more information on how to configure your Slack account on the [Slack Developer Documentation](https://api.slack.com/docs) page\.
+ You have an AWS Secrets Manager secret containing the authentication credentials you are using to connect your Slack data source with your Amazon Kendra index\. If you are using the console to create your data source, you can create the secret there, or you can use an existing Secrets Manager secret\. If you are using the API, you must provide the Amazon Resource Name \(ARN\) of an existing secret\. It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\.
+ \(Optional\) If you want to map attributes or custom index fields from your Slack data source to your Amazon Kendra index, you must make sure that these attributes and custom fields already exist in your data source file system custom metadata\.

## Connecting Amazon Kendra to your Slack data source<a name="data-source-procedure-slack"></a>

To connect Amazon Kendra to your Slack data source you must provide details of your Slack credentials so that Amazon Kendra can access your data\. If you have not yet configured Slack for Amazon Kendra see [Prerequisites](#prerequisites-slack)\.

### <a name="slack-adding-procedure"></a>

------
#### [ Console ]

**To connect Amazon Kendra to Slack** 

1. Sign in to the Amazon Kendra at [AWS Console](https://console.aws.amazon.com/kendra/)\.

1. From the left navigation pane, choose **Indexes** and then choose the index you want to connect from the list of indexes\.

1. On the **Getting started** page, choose **Add data sources**\.
**Note**  
You can choose to configure or edit your **User access control** settings under **Index settings**\. 

1. On the **Add data source** page, choose **Slack**, and then choose **Add connector**\.

1. On the **Specify data source details** page, enter the following information:

   1. **Data source name**—Enter a name for your data source\. You can include hyphens but not spaces\.

   1. \(Optional\)** Description**—Enter an optional description for your data source\.

   1. **Default language**—A language to filter your documents for the index\. Unless you specify otherwise, the language defaults to English\. Language specified in metadata overrides selected language\.

   1. **Add new tag**—Tags to search and filter your resources or track your AWS costs\.

   1. Choose **Next**\.

1. On the **Define access and security** page, enter the following information:

   1. **Slack workspace team ID**—The team ID of your Slack workspace\.

   1. **AWS Secrets Manager secret**—Choose an existing secret or create a new Secrets Manager secret to store your Slack authentication credentials\. If you choose to create a new secret an AWS Secrets Manager secret window opens\.

      1. Enter following information in the **Create an AWS Secrets Manager secret window**:

         1. **Secret name**—A name for your secret\. The prefix ‘AmazonKendra\-Slack\-’ is automatically added to your secret name\.

         1. For **Slack token**—Enter the authentication credential values you generated and downloaded from your Slack account\. 

      1. Choose **Save**\.

   1. **Virtual Private Cloud \(VPC\)**—You can choose to use a VPC\. If so, you must add **Subnets** and **VPC security groups**\.

   1. **IAM role**—Choose an existing IAM role or create a new IAM role to access your repository credentials and index content\.
**Note**  
IAM roles used for indexes cannot be used for data sources\. If you are unsure if an existing role is used for an index or FAQ, choose **Create a new role** to avoid errors\.

   1. Choose **Next**\.

1. On the **Configure sync settings** page, enter the following information:

   1. **Select type of content to crawl**—The Slack entities or content types you want to crawl\.

   1. **Change log**—Select to update your index instead of syncing all your files\.

   1. **Regex patterns**—Regular expression patterns to include or exclude certain files\. You can add up to 100 patterns\.

   1. **Select crawl start date**—What date Amazon Kendra will start crawling your data from\.

   1. **Frequency**—How often Amazon Kendra will sync with your data source\.

   1. Choose **Next**\.

1. On the **Set field mappings** page, enter the following information:

   1. For **Slack field mappings**—Select from the Amazon Kendra generated default data source fields you want to map to your index\. 

   1.  **Add field**—To add custom data source fields to create an index field name to map to and the field data type\.

   1. Choose **Next**\.

1. On the **Review and create** page, check that the information you have entered is correct and then select **Add data source**\. Your data source will appear on the **Data sources** page once it is added successfully\.

------
#### [ SlackConfiguration API ]

**To connect Amazon Kendra to Slack**

You must specify the following using [SlackConfiguration](https://docs.aws.amazon.com/kendra/latest/dg/API_SlackConfiguration.html) API:
+ **Slack workspace team ID**—The Slack team ID you copied from your Slack main page URL\.
+ **List of entities to index**—Whether Amazon Kendra should index your public and private channels, and your group and direct messages\.
+ **Crawl date**—The date to start crawling your data from your Slack workspace team\. The date must follow this format: yyyy\-mm\-dd\.
+ **Secret Amazon Resource Name \(ARN\)**—You must provide the Amazon Resource Name \(ARN\) of a Secrets Manager secret that contains the authentication credentials you created in your Slack account\. You provide the ARN using the `CreateDataSource` API\. The secret is stored in a JSON structure with the following keys: 

  ```
  {
      "slackToken": "token"
  }
  ```
**Note**  
It is recommended that you regularly refresh or rotate your credentials and secret, and only provide the necessary level of access for your own security\. For more information on permissions, see [IAM roles for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.
+ **IAM role**—You must provide an IAM role with permissions to access your Secrets Manager secret and to call the required public APIs for the Slack connector and Amazon Kendra\. For more information, see [IAM roles for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/iam-roles.html#iam-roles-ds)\.

You can also add the following optional features:
+  **Virtual Private Cloud \(VPC\)**—You can choose to specify `VpcConfiguration` when you call `CreateDataSource`\. See [Configuring Amazon Kendra to use a VPC](vpc-configuration.md)\.
+  **Change log**—Whether Amazon Kendra should use the Slack data source change log mechanism to determine if a document must be added, updated, or deleted in the index\.
**Note**  
Use the change log if you don’t want Amazon Kendra to scan all of the documents\. If your change log is large, it might take Amazon Kendra less time to scan the documents in the Slack data source than to process the change log\. If you are syncing your Slack data source with your index for the first time, all documents are scanned\. 
+  **Inclusion and exclusion filters**—You can specify whether to include public and private channels, group and private messages, and bot and archived messages\. You can also specify regular expression patterns to include or exclude public and private channels, group and private messages, and bot and archived messages\.If you use a bot token as part of your Slack authentication credentials, you must add the bot token to the channel you want to index\. You cannot index direct messages and group messages using a bot token\.
**Note**  
If you specify an inclusion filter, only content that matches the inclusion filter is indexed\. Any document that doesn’t match the inclusion filter isn’t indexed\. If you specify an inclusion and exclusion filter, documents that match the exclusion filter are not indexed, even if they match the inclusion filter\.
+  **Context filtering**—You can choose to filter a user’s results based on their user or group access to documents\. For more information, see [User context filtering for Slack data sources](https://docs.aws.amazon.com/kendra/latest/dg/user-context-filter.html)\.
+  **Field mappings**—You can choose to map your Slack data source fields to your Amazon Kendra index fields\. For more information, see [Mapping data source fields](https://docs.aws.amazon.com/kendra/latest/dg/field-mapping.html)\.

------

## Learn more<a name="slack-learn-more"></a>

To learn more about integrating Amazon Kendra with your Slack data source, see:
+ [Unravel the knowledge in Slack workspaces with intelligent search using the Amazon Kendra Slack connector](https://aws.amazon.com/blogs/machine-learning/unravel-the-knowledge-in-slack-workspaces-with-intelligent-search-using-the-amazon-kendra-slack-connector/)